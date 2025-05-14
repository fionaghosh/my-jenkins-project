pipeline {
  agent any

  stages {
    // Stage 1: Build
    stage('Build') {
      steps {
        // Compile & package with Maven
        sh 'mvn clean package'
      }
    }

    // Stage 2: Unit and Integration Tests
    stage('Unit & Integration Tests') {
      steps {
        // Run unit tests via Surefire
        sh 'mvn test'
        // Run integration tests via Failsafe (assumes you’ve defined an "integration" profile)
        sh 'mvn verify -Pintegration'
      }
    }

    // Stage 3: Code Analysis
    stage('Code Analysis') {
      steps {
        // Run SonarQube analysis (requires a SonarQube server configured in Jenkins)
        withSonarQubeEnv('MySonarQubeServer') {
          sh 'sonar-scanner -Dsonar.projectKey=my-jenkins-project'
        }
      }
    }

    // Stage 4: Security Scan
    stage('Security Scan') {
      steps {
        // OWASP Dependency-Check Maven plugin
        sh 'mvn org.owasp:dependency-check-maven:check'
      }
    }

    // Stage 5: Deploy to Staging
    stage('Deploy to Staging') {
      steps {
        // Push & create a deployment via AWS CLI (CodeDeploy)
        sh '''
          aws deploy push \
            --application-name MyApp \
            --s3-location s3://my-bucket/my-app.zip \
            --ignore-hidden-files

          aws deploy create-deployment \
            --application-name MyApp \
            --deployment-group-name staging \
            --s3-location bucket=my-bucket,key=my-app.zip,bundleType=zip
        '''
      }
    }

    // Stage 6: Integration Tests on Staging
    stage('Integration Tests on Staging') {
      steps {
        // Run Postman collections against staging via Newman
        sh 'newman run tests/postman_collection.json -e tests/env/staging.json'
      }
    }

    // Stage 7: Deploy to Production
    stage('Deploy to Production') {
      steps {
        // Similar AWS CodeDeploy call, targeting the production group
        sh '''
          aws deploy create-deployment \
            --application-name MyApp \
            --deployment-group-name production \
            --s3-location bucket=my-bucket,key=my-app.zip,bundleType=zip
        '''
      }
    }
  }
}

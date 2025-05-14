pipeline {
  agent any

  stages {
    stage('Stage 1: Build') {
      steps {
        echo 'Build – Compile and package the code using Maven'
      }
    }

    stage('Stage 2: Unit and Integration Tests') {
      steps {
        echo 'Unit and Integration Tests – Run unit tests with JUnit (Surefire) and integration tests with Maven Failsafe'
      }
    }

    stage('Stage 3: Code Analysis') {
      steps {
        echo 'Code Analysis – Perform static code analysis using SonarQube scanner'
      }
    }

    stage('Stage 4: Security Scan') {
      steps {
        echo 'Security Scan – Identify vulnerabilities with OWASP Dependency-Check'
      }
    }

    stage('Stage 5: Deploy to Staging') {
      steps {
        echo 'Deploy to Staging – Deploy the application to a staging AWS EC2 instance via CodeDeploy'
      }
    }

    stage('Stage 6: Integration Tests on Staging') {
      steps {
        echo 'Integration Tests on Staging – Execute end-to-end tests using Newman (Postman CLI)'
      }
    }

    stage('Stage 7: Deploy to Production') {
      steps {
        echo 'Deploy to Production – Deploy the validated artifact to production AWS EC2 via CodeDeploy'
      }
    }
  }
}

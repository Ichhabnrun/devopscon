pipeline {
  agent any
  stages {
    stage('error') {
      steps {
        echo 'Loum Build gestartet...'
        script {
          node {
            def mvnHome
            stage('Preparation') { // for display purposes
            // Get some code from a GitHub repository
            git 'https://github.com/Ichhabnrun/devopscon.git'
            // Get the Maven tool.
            // ** NOTE: This 'M3' Maven tool must be configured
            // **       in the global configuration.
            mvnHome = tool 'Maven'
          }
          stage('Build') {
            // Run the maven build
            if (isUnix()) {
              sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
            } else {
              bat(/"${mvnHome}\bin\mvn" clean install -Pci/)
            }
          }
          stage('Results') {
            junit '**/target/surefire-reports/TEST-*.xml'
            archive 'target/*.jar'
          }
        }
      }

    }
  }
}
}
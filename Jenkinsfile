pipeline {
  agent any
  stages {
    stage('OWASP Check') {
      steps {
        dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'Default'
      }
    }
  }
  post {
    always {
      dependencyCheckPublisher pattern: 'dependency-check-report.xml'
    }
  }
}

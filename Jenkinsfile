pipeline {
  agent {
    docker {
      image 'composer:latest'
    }
  }
  stages {
    stage('OWASP Check') {
      steps {
        dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'Default'
      }
    }
    stage('Build') {
      steps {
        sh 'composer install'
      }
    }
    stage('Test') {
      steps {
        sh './vendor/bin/phpunit --log-junit logs/unitreport.xml -c tests/phpunit.xml tests'
      }
    }
  }
  
  post {
    always {
      dependencyCheckPublisher pattern: 'dependency-check-report.xml'
      junit testResults: 'logs/unitreport.xml'
    }
  }
}

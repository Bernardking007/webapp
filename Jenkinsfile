pipeline {
    agent any
    tools {
        maven 'mymaven'
    }

    stages {
        stage('clone') {
            steps {
                git url: 'https://github.com/Bernardking007/webapp.git'
            }
        }
        stage('compile') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('code_review') {
            steps {
                sh 'mvn -P metrics pmd:pmd'
            }
        }
        stage('unit_test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('metric_check') {
            steps{
                sh 'mvn cobertura:cobertura -D cobertura.report.format=xml'
            }
        }
      stage ('Check-Git-Secrets') {
      steps {
        sh 'rm trufflehog || true'
        sh 'docker run gesellix/trufflehog --json https://github.com/Bernardking007/webapp.git > trufflehog'
        sh 'cat trufflehog'
      }
    }   
  stage ('Source Composition Analysis') {
      steps {
         sh 'rm owasp* || true'
         sh 'wget "https://raw.githubusercontent.com/Bernardking007/webapp/master/Owasp-dependency-check" '
         sh 'chmod +x owasp-dependency-check.sh'
         sh 'bash owasp-dependency-check.sh'  
        }
    }    
        stage('package') {
            steps{
                sh 'mvn package'
            }
        }
    }
}

 

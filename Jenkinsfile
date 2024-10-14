pipeline {
    agent any

    tools {
        maven 'M2_HOME'
    }

    environment {
        APP_ENV = "DEV"
    }

    stages {
        stage('Code Checkout') {
            steps {
                git branch: 'master', 
                    url: 'https://github.com/ahmedlaifia/atelier-jenkinsfile2'
            }
        }

        stage('Code Build') {
            steps {
                sh 'mvn install -Dmaven.test.skip=true'
            }
        }
    }
    stage('MVN SONARQUBE') {
    steps {
        withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
            sh 'mvn sonar:sonar -Dsonar.login=$SONAR_TOKEN -Dmaven.test.skip=true'
        }
    }
}


    post {
        always {
            echo "======always======"
        }
        success {
            echo "=====pipeline executed successfully ====="
        }
        failure {
            echo "======pipeline execution failed======"
        }
    }
}

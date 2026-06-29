pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
        jdk 'JDK21'
    }

    environment {
        APP_NAME = 'hello-world'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/lantranlan007/hello-world.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('List Target') {
            steps {
                bat 'dir target'
            }
        }

        stage('Run JAR') {
            steps {
                bat '''
                    echo Starting application...
                    start "" java -jar target\\hello-world.jar
                    timeout /t 5 /nobreak
                    echo App started
                '''
            }
        }

        stage('Check Process') {
            steps {
                bat 'tasklist | findstr java'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
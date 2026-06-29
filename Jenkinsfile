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
        bat 'for %%f in (target\\*.jar) do start "" java -jar "%%f"'
        sleep time: 5, unit: 'SECONDS'
        echo 'App started'
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
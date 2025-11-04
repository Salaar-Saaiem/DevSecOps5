pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'JDK17'
    }

    environment {
        TOMCAT_USER = 'admin'
        TOMCAT_PASS = 'SaaiemSalaar'
        TOMCAT_URL  = 'http://localhost:7080'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Salaar-Saaiem/maven-ci-demo.git'
            }
        }

        stage('Build WAR') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                bat '''
                curl -u %TOMCAT_USER%:%TOMCAT_PASS% ^
                -T target\\maven-ci-demo.war ^
                "%TOMCAT_URL%/manager/text/deploy?path=/maven-ci-demo&update=true"
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Application successfully deployed to Tomcat!'
        }
        failure {
            echo '❌ Build or deployment failed.'
        }
    }
}

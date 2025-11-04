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
                // ✅ Correct repo
                git 'https://github.com/Salaar-Saaiem/DevSecOps5.git'
            }
        }

        stage('Build WAR') {
            steps {
                // ✅ Build the WAR package
                bat 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                // ✅ Updated WAR filename and context path
                bat '''
                curl -u %TOMCAT_USER%:%TOMCAT_PASS% ^
                -T target\\DevSecOps5.war ^
                "%TOMCAT_URL%/manager/text/deploy?path=/DevSecOps5&update=true"
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

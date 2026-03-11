pipeline {

    agent any

    tools {
         maven 'Maven'
        jdk 'JDK17'
    }

    stages {

        stage('Checkout') {
            steps {
                
                git branch: 'master', url: 'https://github.com/Tushar3497/Jenkins_WebApp'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('Run JUnit Tests') {
            steps {
                bat 'mvn test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('admin') {
                    bat 'mvn clean verify sonar:sonar'
                }
            }
        }

        stage('Build with Maven') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                bat 'copy target\\*.war "D:\Program Files\Apache Software Foundation\Tomcat 10.1\webapps'
            }
        }

        stage('Start Tomcat Server') {
            steps {
                bat '"D:\Program Files\Apache Software Foundation\Tomcat 10.1\bin\startup.bat"'
            }
        }

    }
}
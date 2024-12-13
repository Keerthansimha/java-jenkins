pipeline {
    agent any

    tools {
        maven 'maven'
        jdk 'java'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    extensions: [], 
                    userRemoteConfigs: [[credentialsId: 'github-access', url: 'https://github.com/sreenivas449/java-hello-world-with-maven.git']]
                ])
            }
        }
        stage('Build') {
            steps {
                script {
                    // Automatically detect the OS and use the appropriate command
                    if (isUnix()) {
                        sh 'mvn package'
                    } else {
                        bat 'mvn package'
                    }
                }
            }
        }
    }
}

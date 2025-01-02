pipeline {
    agent {
        label 'maven-project' // Replace with your agent's label
}

    tools {
        maven 'maven'
        jdk 'java'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', 
                    branches: [[name: '*/main']], 
                    extensions: [], 
                    userRemoteConfigs: [[credentialsId: 'github-access', url: 'https://github.com/Keerthansimha/java-jenkins.git']]
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

        stage('Trigger Next Job') {
            steps {
                script {
                    // Trigger the next job (e.g., testing-pipeline)
                    build job: 'testing-pipeline', wait: true
                }
            }
        }
    }
}

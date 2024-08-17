pipeline {
    agent any
    tools {
      maven 'mvn3'
    }

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        
        stage('checkout') {
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/begging-pp0/jenkins-prj1.git']])
            }
        }
        
        stage('Build') {
            steps{
                echo 'Building Maven Project'
                sh 'mvn clean compile'
            }
        }
        
        stage('Test') {
            steps{
                echo 'Unit Test'
                sh 'mvn test'
                junit '**/target/surefire-reports/*.xml'
            }
        }
        
        stage('Install') {
            steps{
                echo 'Install the package *jar'
                sh 'mvn install'
            }
        }
        
        stage('Archive the artifact') {
            steps{
                archiveArtifacts artifacts: 'target/calculator-0.0.1-SNAPSHOT.jar', followSymlinks: false
            }
        }

        stage('Slack Notifications') {
            steps{
                slackSend channel: 'jenkins-prj1', failOnError: true, message: 'Here\'s the new build of the app Jenkins-prj1'
            }
        }
                
    }
}

pipeline {
    agent any
    tools {
        maven 'maven_3.8.8'
    }
    stages {
        stage('Code Compilation') {
            steps {
                echo 'code compilation is starting'
                sh "mvn clean compile"
                echo 'code compilation is completed'
            }
        }
        stage('Code Package') {
            steps {
                echo 'code packing is starting'
                sh "mvn clean package"
                echo 'code packing is completed'
            }
        }
    }
}




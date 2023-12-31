pipeline {
    agent any

    tools {
        maven 'maven_3.8.8'
    }

    stages {
        stage('Code Compilation') {
            steps {
                echo 'code compilation is starting'
                sh 'mvn clean compile'
				echo 'code compilation is completed'
            }
        }

        stage('Code Package') {
            steps {
                echo 'code packing is starting'
                sh 'mvn clean package'
				echo 'code packing is completed'
            }
        }
        stage('Building & Tag Docker Image') {
            steps {
                echo 'Starting Building Docker Image'
                sh 'docker build -t abhijit76/year2023 .'
                sh 'docker build -t year2023 .'
                echo 'Completed  Building Docker Image'
            }
        }
        stage('Docker Image Scanning') {
            steps {
                echo 'Docker Image Scanning Started'
                sh 'java -version'
                echo 'Docker Image Scanning Started'
            }
        }
        stage(' Docker push to Docker Hub') {
           steps {
              script {
                  withCredentials([string(credentialsId: 'dockerhubCred', variable: 'dockerhubCred')]){
                  echo "password/ ${dockerhubCred}"
	          sh 'docker login docker.io -u abhijit76 -p ${dockerhubCred}'
                  echo "Push Docker Image to DockerHub : In Progress"
                  sh 'docker push abhijit76/year2023:latest'
                  echo "Push Docker Image to DockerHub : In Progress"
                  sh 'whoami'
                  }

              }

           }
        }
        stage(' Docker Image Push to Amazon ECR') {
           steps {
              script {
                 withDockerRegistry([credentialsId:'ecr-credentials', url:"https://280993177205.dkr.ecr.ap-south-1.amazonaws.com"]){
                 sh """
                 echo "List the docker images present in local"
                 docker images
                 echo "Tagging the Docker Image: In Progress"
                 docker tag year2023:latest 280993177205.dkr.ecr.ap-south-1.amazonaws.com/year2023:latest
                 echo "Tagging the Docker Image: Completed"
                 echo "Push Docker Image to ECR : In Progress"
                 docker push 280993177205.dkr.ecr.ap-south-1.amazonaws.com/year2023:latest
                 echo "Push Docker Image to ECR : Completed"
                 """
                 }
              }
           }
        }
         stage('Delete the docker images after upload') {
            steps {
                sh'java--version'
                sh'java--version'
                 }
         }
    }
}

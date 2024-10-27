pipeline {
    agent any
    stages {
        stage('Checkout Code from GitHub') {
            steps {
                git url: 'https://github.com/Ascendionrohit/Banking-rohit/'
                echo 'GitHub URL checked out'
            }
        }
        stage('Compile Code') {
            steps {
                echo 'Starting code compilation'
                sh 'mvn compile'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Run QA Checkstyle') {
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('Package Application') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t banking-rohit .'
            }
        }
        stage('Expose Port') {
            steps {
                sh 'docker run -d -p 8081:8081 banking-rohit:latest'
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerlogin', passwordVariable: 'docker_pass', usernameVariable: 'docker_user')])  {
                    sh "docker login -u $docker_user -p $docker_pass"
                }
                sh "docker tag banking-rohit:latest sainirohit82733/banking-rohit:latest"
                sh "docker push sainirohit82733/banking-rohit:latest"
            }
        }
    }
}

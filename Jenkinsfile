pipeline{
    agent any
    stages{
        stage('checkout the code from github'){
            steps{
                 git url: 'https://github.com/Ascendionrohit/Banking-rohit/'
                 echo 'github url checkout'
            }
        }
        stage('codecompile with rohit'){
            steps{
                echo 'starting compiling'
                sh 'mvn compile'
            }
        }
        stage('codetesting with rohit'){
            steps{
                sh 'mvn test'
            }
        }
        stage('qa with rohit'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('package with rohit'){
            steps{
                sh 'mvn package'
            }
        }
        stage('run dockerfile'){
          steps{
               sh 'docker build -t myimg .'
           }
         }
        stage('port expose'){
            steps{
                sh 'docker run -dt -p 8091:8091 --name c000 myimg'
            }
        }   
    }
}

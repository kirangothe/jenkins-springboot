pipeline {
    agent any 
    stages {
        stage('Compile and Clean') { 
            steps {

                sh "mvn clean compile"
            }
        }
        stage('Test') { 
            steps {
                sh "mvn test site"
            }
            
          /*   post {
                always {
                    junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'   
                }
            } */     
        }

        stage('deploy') { 
            steps {
                sh "mvn package"
            }
        }


        stage('Build Docker image'){
            steps {
                sh 'docker build -t kirangothe/springboot .'
            }
        }

     /*   stage('Docker Login'){
            
            steps {
                 withCredentials([string(credentialsId: 'DockerId', variable: 'Dockerpwd')]) {
                    sh "docker login -u kirangothe -p ${Dockerpwd}"
                }
            }                
        } */

        stage('Docker Push'){
            steps {
                sh 'docker push kirangothe/springboot'
            }
        }
        
        stage('Docker deploy'){
            steps {
                sh 'docker run -itd -p 8081:8080 kirangothe/springboot'
            }
        }

        
      /*  stage('Archving') { 
            steps {
                 archiveArtifacts '**/target/*.jar'
            }
        } */
    }
}

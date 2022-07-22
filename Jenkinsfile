pipeline {
    //agent { label 'docker-maven-slave' } 
    agent any
    triggers {
          pollSCM('4 4 4 * *')
    }
    environment {
          VER_NUM = "1.0.${BUILD_NUMBER}";
          REL_NUM = "1.0.${BUILD_NUMBER}.RELEASE";
     }
    tools{
          maven 'maven'
     }
    stages {
           stage ('Git Checkout') {
                 steps {
                     echo "Heloo!!!!";
                     git credentialsId: 'github-credentials' , url: 'https://github.com/sbathuru/angular-todo.git',  branch: 'master'   
                }
           }

          stage('Docker Build & Push') {    
                  steps {
                          script{        // To add Scripted Pipeline sentences into a Declarative
                                    try{
                                            sh "pwd"
                                             //sh "docker rm -f devops-devops-angularui || true"
                                             //sh "docker rmi bathurudocker/devops-devops-angularui || true"       //sh 'docker rmi $(docker images bathurudocker/devops-devops-angularui)''
                                          }catch(error){
                                          //  do nothing if there is an exception
                                          }
                            }

                          withCredentials([string(credentialsId: 'dockerHubPwd', variable: 'dockerpwd')]) {
                                 sh "docker login -u sbathuru -p ${dockerpwd}"
                         }
                          sh "docker build -t bathurudocker/angular-todo:${VER_NUM} ."
                          sh "docker image tag bathurudocker/angular-todo:${VER_NUM}  bathurudocker/devops-angularui:latest"
                          sh "docker push bathurudocker/angular-todo:${VER_NUM}" 
                         sh "pwd"
                         //sh "docker build -t bathurudocker/devops-angularui:latest ."
                          //sh "docker image tag bathurudocker/devops-angularui:latest  bathurudocker/devops-angularui:latest"
                          //sh "docker push bathurudocker/devops-angularui:latest" 
                          sh "docker rmi bathurudocker/angular-todo" 
                 } 
          }

     stage('Deploy Into DEV') {
       steps {   
           sh "pwd"
           sshagent(['aws-ap-south-pem']) {
               sh "ssh -o StrictHostKeyChecking=no ec2-user@docker.bathur.xyz  sudo docker rm -f devops-angularui || true"
               //sh "ssh -o StrictHostKeyChecking=no ec2-user@docker.bathur.xyz  sudo docker run  -d -p 80:80 --name devops-angularui bathurudocker/devops-angularui:${VER_NUM}"
                sh "ssh -o StrictHostKeyChecking=no ec2-user@docker.bathur.xyz  sudo docker run  -d -p 80:80 --name devops-angularui bathurudocker/devops-angularui:latest"
          }
       }
     }     
    }

    post { success { echo 'Pipeline Sucessfully Finished' }
           failure { echo 'Pipeline Failure' }
           always {
                    mail bcc: '', 
                    body: """ Hi Team, 
                          Your project got Build and Deployed successfully!!!

                          Please find the details as below,
	                        Job Name: ${env.JOB_NAME}
	                        Job URL : ${env.JOB_URL}
                          Build Number: ${env.BUILD_NUMBER} 
                          Build URL: ${env.BUILD_URL}

                          Thanks
                          DevOps Team""", 
                    cc: '', 
                    from: '', 
                    replyTo: '', 
                    subject: "Sucess !!! - ${env.JOB_NAME} - Build # ${env.BUILD_NUMBER}", 
                    to: 'srinivas.bathuru@gmail.com'
           } 
         }
         
}
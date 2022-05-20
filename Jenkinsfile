pipeline {
    agent any

        stages {
            stage('verifying git repo'){
                steps{
                    echo "welcome to jenkins practice"  
                    git branch: 'main', url: 'https://github.com/PrashanthgRebel/docker_nginx.git'
                }

            }
            stage('building nginx on docker'){
            	steps{

            		sh '''SSH_ARGS=\'-q -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null\'
                    sshpass -p \'9246\' ssh ${SSH_ARGS}  prashanth@172.29.87.227 "sudo docker build -t nginx_test /home/prashanth/Docker/docker_nginx/"
                    
                    '''
                    
            	}

            }

            stage('Removing old docker container'){
                steps{

                    sh '''SSH_ARGS=\'-q -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null\'
                    sshpass -p \'9246\' ssh ${SSH_ARGS}  prashanth@172.29.87.227 "sudo docker stop nginx_web && sudo docker rm nginx_web"

                    '''
                }
            }

            stage('Creating New nginx_web container'){
                steps{
                    sh '''SSH_ARGS=\'-q -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null\'
                    sshpass -p \'9246\' ssh ${SSH_ARGS}  prashanth@172.29.87.227 "sudo docker run -d --name nginx_web --privileged=true -p 900:80 nginx_test:latest  /usr/sbin/init"
                    '''

                }
            }
            
        	stage('starting nginx on nginx on nginx_web container '){
        		steps{
        			echo "starting  nginx service"
                    sh '''SSH_ARGS=\'-q -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null\'
                    sshpass -p \'9246\' ssh ${SSH_ARGS}  prashanth@172.29.87.227 "sudo docker exec -it nginx_web systemctl start nginx"

                    ''' 

        		}
        	}

            stage('Verifying website using curl'){
                steps{

                   sh '''SSH_ARGS=\'-q -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null\'
                    sshpass -p \'9246\' ssh ${SSH_ARGS}  prashanth@172.29.87.227 "sudo curl -I 172.29.87.227:900"

                    ''' 

                }
            }

        }
}

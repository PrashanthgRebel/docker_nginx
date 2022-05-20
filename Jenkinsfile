pipeline {
    agent any
        tools{
            maven 'maven3'
        }

        stages {
            stage('verifying git repo'){
                steps{
                    echo "welcome to jenkins practice"
                    git branch: 'main', url: 'https://github.com/PrashanthgRebel/docker_nginx.git'
                }

            }
            stage('build nginx on docker'){
            	steps{
            		echo "building nginx docker image"
            		sh '''SSH_ARGS=\'-q -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null\'
                    sshpass -p \'9246\' ssh ${SSH_ARGS}  prashanth@172.29.87.227 "sudo docker build -t nginx_test /home/prashanth/Docker/docker_nginx/"
                    sshpass -p \'9246\' ssh ${SSH_ARGS}  prashanth@172.29.87.227 "sudo docker stop nginx_web && sudo docker rm nginx_web"
                    sshpass -p \'9246\' ssh ${SSH_ARGS}  prashanth@172.29.87.227 "sudo docker run -d --name nginx_web --privileged=true -p 900:80 nginx_test:latest  /usr/sbin/init"
 

                    '''
                    echo "Build success"
            	}
            }
            
        	stage('starting nginx on nginx on nginx_web container '){
        		steps{
        			echo "starting  nginx service"
                    sh '''sshpass -p \'9246\' ssh ${SSH_ARGS}  prashanth@172.29.87.227 " sudo docker exec -it nginx_web systemctl start nginx"
 

                    '''

        		}
        	}

        }
}

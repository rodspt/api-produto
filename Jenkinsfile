pipeline { 
    agent any  

    stages { 
        stage ('Build Image') { 
            steps { 
                script {
                   dockerapp = docker.build("rodspt/sigabc-backend:${env.BUILD_ID}", '-f ./src/Dockerfile ./src') 
                }                
            }
        }


        stage ('Push Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub'){
                        dockerapp.withRegistry('', 'rodspt')
                        dockerapp.push('latest')
                        dockerapp.push(${env.BUILD_ID})
                    }
                }
            }    
        }

    }
}
pipeline { 
    agent any  

    environment {
      buildVersion =    env.BUILD_ID
      registryCredential = 'rodspt'
    }

    stages { 
        stage ('Build Image') { 
            steps { 
                script {
                   dockerapp = docker.build("rodspt/sigabc-backend:${buildVersion}", '-f ./src/Dockerfile ./src') 
                }                
            }
        }


        stage ('Push Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub'){
                        dockerapp.withRegistry('', registryCredential)
                        dockerapp.push('latest')
                        dockerapp.push(${buildVersion})
                    }
                }
            }    
        }

    }
}
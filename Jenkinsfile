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

    }
}
pipeline { 
    agent any  

    stages { 
        stage ('Build Image') { 
            steps { 
                 script {
                     dockerapp = docker.build("rodspt/api-produto", '-f ./src/Dockerfile ./src')   
                 } 
            }
        }

    }
}
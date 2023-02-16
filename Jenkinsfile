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
                    docker.withRegistry('https://registry.hub.docker.com', 'rodspt'){
                        dockerapp.push(env.BUILD_ID)
                        dockerapp.push('latest')
                    }
                }
            }    
        }

         stage ('Deploy Kubernetes') {
            environment {
                tag_version = "${env.BUILD_ID}"
            }
            steps {
                withKubeConfig([credentialsId: 'kubeconfig']) {
                     sh 'kubectl apply -f ./k8s/deployment.yaml'
                }
            }
        }

    }
}
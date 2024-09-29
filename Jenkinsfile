def containerName="docker-pipeline"
def tag="latest"
def httpPort="8090"

node {

    stage('Checkout') {
        checkout scm
    }

    stage('Build'){
        sh "mvn clean install"
    }

    stage("Image Prune"){
         sh "docker image prune -f"
    }

    stage('Image Build'){
        sh "docker build -t $containerName:$tag  -t $containerName --pull --no-cache ."
        echo "Image build complete"
    }

    stage('Push to Docker Registry'){

            echo "Image push complete"
        }
    }

    stage('Run App'){
        /*sh "docker rm $containerName -f"
        sh "docker pull $dockerHubUser/$containerName"
        sh "docker run -d --rm -p $httpPort:$httpPort --name $containerName $dockerHubUser/$containerName:$tag"
        echo "Application started on port: ${httpPort} (http)"
        */
        sh """
           kubectl get pods
           kubectl delete deployment kubernetes-bootcamp
           kubectl create deployment kubernetes-bootcamp --image=docker.io/anujsharma1990/docker-pipeline --port=8090
           kubectl get pods
        """
    }

}

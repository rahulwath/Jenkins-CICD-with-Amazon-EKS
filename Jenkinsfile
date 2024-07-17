node {

    stage("Git Clone"){

        git credentialsId: 'GIT_HUB_CREDENTIALS', url: 'https://github.com/rahulwath/Jenkins-CICD-with-Amazon-EKS.git', branch: 'main' 
    }

     stage("Build") {

       sh 'docker build . -t rahulwath/node-todo-test:latest'
       sh 'docker image list'

    }

    withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
        sh 'docker login -u rahulwath -p $PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push rahulwath/node-todo-test:latest'
    }

    stage("kubernetes deployment"){
        sh 'kubectl apply -f deployment.yml'
    }
}
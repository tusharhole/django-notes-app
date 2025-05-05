@Library ("Shared") _
pipeline{
    agent {label 'Advika'}
    stages{
     stage("Code"){
            steps{
                echo "this is clong the code"
              clone("https://github.com/tusharhole/django-notes-app.git", "main")
                echo "Code Cloned Successfully"
            }
        }
        stage("Build"){
            steps{
                echo "this is biulding the code"
                sh "whoami"
                sh "docker build -t notes-app:latest ."
            }
        }
        stage("test"){
            steps{
                echo "this is testing the code"
            }
        }
       stage("Pushing to DockerHub") {
    steps {
        echo "This is Pushing the image to Docker Hub"
        withCredentials([usernamePassword(
            credentialsId: 'dockerHubCred',
            usernameVariable: 'dockerHubUser',
            passwordVariable: 'dockerHubPass'
        )]) {
            sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
            sh "docker image tag notes-app:latest ${env.dockerHubUser}/notes-app:latest"
            sh "docker push ${env.dockerHubUser}/notes-app:latest"
        }
    }
}

        stage("Deploy"){
            steps{
                echo "this is deploying the code"
                sh "docker compose down && docker compose up -d "
            }
        }
    }
}


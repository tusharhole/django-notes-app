pipeline{
    agent{label 'prod-agent'}
    stages{
        stage('Project cloned'){
            steps{
                git url : 'https://github.com/tusharhole/django-notes-app.git', branch :'main'
            }
            
        }
        
         stage('Project Build'){
            steps{
                
                sh 'docker build . -t tusharh/note-app:latest'
            }
            
        }
        
         stage('Push to dockerhub'){
            steps{
                echo "pushing the iamge to dockerhub"
                withCredentials([usernamePassword(credentialsId: 'Dockerhub', passwordVariable: 'hole', usernameVariable: 'tushar')]) {
                    sh "docker login -u ${env.tushar} -p ${env.hole}"
                    sh "docker push tusharh/note-app:latest"
                    }
            }
            
        }
        stage('Deploy'){
            steps{
                echo "Deploying the conatiner"
                sh "docker-compose down && docker-compose up -d"
            }
            
        }
    }
}

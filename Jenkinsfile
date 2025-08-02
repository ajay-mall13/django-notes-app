pipeline {
    agent any;

    stages {
        stage("Code clone") {
            steps {
                git url : "https://github.com/ajay-mall13/django-notes-app.git" , branch : "master"
            }
        }

stage("Docker Build") {
    steps {
        sh "docker build -t notes-app ."
    }
}



        stage("test") {
            steps {
               echo "complete build"
            }
        }
        
        
    stage('Docker Push on dockerhub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhubcreds',
                    usernameVariable: 'dockerHubUser',
                    passwordVariable: 'dockerHubPass'
                )]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker image tag notes-app ${env.dockerHubUser}/notes-app:latest"
                    sh "docker push ${env.dockerHubUser}/notes-app:latest"
                }
            }
        }
        
stage("Docker deploy") {
    steps {
        sh """
        docker compose down || true
        docker rm -f db_cont django_cont nginx_cont || true
        docker compose up -d --force-recreate
        """
    }
}


    }
}

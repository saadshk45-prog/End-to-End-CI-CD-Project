pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Build started'
            }
        }

        stage('Test') {
            steps {
                bat '''
                    if exist index.html (
                        echo TEST PASSED
                    ) else (
                        echo TEST FAILED
                        exit /b 1
                    )
                '''
            }
        }

        stage('Docker Build') {
            steps {
                bat '''
                    set "PATH=C:\\Users\\Admin\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin;%PATH%"
                    docker build -t jenkins-final-cicd-project .
                '''
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                    set "PATH=C:\\Users\\Admin\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin;%PATH%"

                    docker stop jenkins-final-cicd-project-conatiner 2>nul
                    docker rm jenkins-final-cicd-project-conatiner 2>nul

                    docker run -d --name jenkins-final-cicd-project-conatiner -p 8084:80 jenkins-pipeline-lab5
                '''
            }
        }
    }
}

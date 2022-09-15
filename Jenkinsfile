pipeline {
    agent { label 'test' }
    
    stages {
        stage('Docker Version') {
            steps {
                sh "echo $USER"
                sh "docker version"
            }
        }
        stage('Delete workspace before build starts') {
            steps {
                echo 'Deleting workspace'
                deleteDir()
            }
        }
        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/KostyaDzju/SimpleWhaleDemo.git'
                sh "pwd"
                sh "ls -la"   
            }
            
        }
        stage('Test') {
            steps {
                dir('static') {
                    sh "ls -la"
                    sh "pwd"
                }
                sh "ls -la"
                sh "pwd"    
            }
            
        }
        stage('Build docker image') {
            steps {
                sh "docker build -t kostyadzju/image ."
            }
        }
        stage('Push dokcer image to DockerHub') {
            steps {
                withDockerRegistry(credentialsId: 'jenkinsbakavetstest', url: 'https://index.docker.io/v1/') {
                    sh '''
                        docker push kostyadzju/image
                    '''
                }
            }
        }
        stage('Delete local docker image') {
            steps {
                sh "docker rmi kostyadzju/image"
            }
        }
    }
}

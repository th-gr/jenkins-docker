pipeline {
    environment {
        registry =  'thomasgbz'
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
    agent any

    stages {
        stage('Git checkout') {
            steps {
                checkout scm
            }
        }

        stage ('Build image') {
            steps {
                dir ('app') {
                    script {
                        dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    }
                }
            }
        }

        stage('Publish Image') {
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                        dockerImage.push("latest")
                    }
                }
            }
        }

        // stage('Remove Unused docker images') {
        //     steps {
        //         sh "docker rmi $registry:$BUILD_NUMBER"
        //     }
        // }
    }
}
pipeline {
    agent any 
    tools {
        jdk "java17"
        maven "maven3"
    }
    stages {
        stage ("clone"){
            steps {
                git branch: 'main', url: 'https://github.com/adigopi49/vprofile-project.git'
            }
        }
        stage("build"){
            steps{
                sh "mvn clean package"
            }
        }
        stage("code analysis"){
            steps {
                sh "mvn sonar:sonar"
            }
        }
        stage("nexua-upload"){
            steps{
                sh "mvn deploy"
            }
        }
        stage ("docker-deploy"){
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker', toolName: 'docker') {
                        sh "docker build -t gopiadi/tom ."
                    }
                }
            }
        }
    }
}

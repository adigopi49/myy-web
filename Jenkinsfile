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
        stage("docker-build"){
            steps {
                script{
                    // This step should not normally be used in your script. Consult the inline help for details.
withDockerRegistry(credentialsId: 'docker', toolName: 'docker', url: 'https://hub.docker.com/') {
                        sh "docker build -t gopiadi/tom ."
                    }
                }
            }
        }
    }
}

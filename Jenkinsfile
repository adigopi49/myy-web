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
        stage ("tomcat"){
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://18.60.237.172:8082/manager/html')], contextPath: null, war: '**/*.war'
            }
        }
        stage ("docker-tag"){
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

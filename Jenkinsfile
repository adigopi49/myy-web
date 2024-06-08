pipeline {
    agent any 
    tools {
        jdk "java17"
        maven "maven3"
    }
    stages {
        stage ("clone"){
            steps {
                git 'https://github.com/adigopi49/myy-web.git'
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
    }
}

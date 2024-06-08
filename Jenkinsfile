pipeline {
    agent any 
    tools {
        jdk "java17"
        maven "maven3"
    }
    stages {
        stage ("clone"){
            steps {
                sh "echo 'hi'"
            }
        }
        stage("build"){
            steps{
                sh "mvn clean package"
            }
        }
    }
}

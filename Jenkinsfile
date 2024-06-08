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
    }
}

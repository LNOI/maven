pipeline {
    agent any
    environment {
        PATH = "/opt/maven/bin:$PATH"
        DOCKERHUB_CREDENTIALS=credentials('dockerhub')
    }
    stages {
        stage('Init') {
            steps {
                echo "Connect webhook1"
            }
        }
         stage('Sonacube'){
                                  steps{
                                       withSonarQubeEnv('sonarqube_server') {
                                       sh 'mvn sonar:sonar'
                                        }
                                  }
                            }

    }


}


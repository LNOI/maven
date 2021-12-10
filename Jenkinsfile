pipeline {
    agent any
    environment {
        PATH = "/opt/maven/bin:$PATH"
        DOCKERHUB_CREDENTIALS=credentials('dockerhub')
    }
    stages {
        stage('Init') {
            steps {
                echo "Connect webhook success"
            }
        }

//          stage('Code Security'){
//                         parallel{
//                             stage('OWASP Dependency-Check Vulnerabilities'){
//                                 steps{
//                                       sh 'mvn dependency-check:check'
//                                       dependencyCheckPublisher pattern: 'target/dependency-check-report.xml'
//                                 }
//                             }
//                             stage('Sonacube'){
//                                   steps{
//                                        withSonarQubeEnv('sonarqube_server') {
//                                        sh 'mvn sonar:sonar'
//                                         }
//                                   }
//                             }
//                         }
//          }

         stage('Build and push on Tomcat server local'){
                                 parallel{
                                     stage('Build') {
                                                 steps {
                                                     sh 'mvn clean install'
                                                 }
                                     }
                                      stage('Push file tomcat server') {
                                                 steps {
                                                    sh 'cp ./target/MyMaven.war /opt/tomcat/webapps/'
                                                 }
                                      }
                                 }
         }




    }


}


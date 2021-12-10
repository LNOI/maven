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
                                                    sh 'sudo  cp target/MyMaven.war /opt/tomcat/webapps/'
                                                 }
                                      }
                                 }
         }
         stage('DAST OWASP ZAP '){
                     steps{
                         sh 'echo "Check OWASP ZAP"'
                         sh 'sudo docker run --user $(id -u):$(id -g) -v $(pwd):/zap/wrk/:rw -t owasp/zap2docker-stable zap-baseline.py -t http://10.0.3.132:8081/MyMaven/ -g gen.cof  -r report.html'
                     }
         }




    }


}


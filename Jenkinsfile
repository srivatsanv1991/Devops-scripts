pipeline{
    def server = Artifactory.newServer url: 'http://localhost:8081/artifactory', username: 'jenkinsuser', password: 'password123'
    agent none
    stages{
        stage('Build'){
            agent {
                docker {
                    image 'maven:3-alpine'
                    args '-v /root/.m2:/root/.m2'
                }
            }
            steps {
                sh 'mvn install -e -DskipTests=true'
            }
        }

        stage('Sample'){
            steps{
                echo 'This is stage 2'
            }
        }

        stage('Build node'){
            agent{
                docker{
                    image 'node:7-alpine'
                }
            }
            steps {
                sh 'node --version'
            }
        }

        stage('Build java'){
            agent{
                docker{
                    image 'openjdk:8-jre'
                }
            }

            steps{
                sh 'java -version'
            }
        }
def uploadSpec = """{
  "files": [
    {
      "pattern": "target/*.jar",
      "target": "libs-release-local/MyTestApp/"
    }
 ]
}"""
server.upload(uploadSpec)
        }
}

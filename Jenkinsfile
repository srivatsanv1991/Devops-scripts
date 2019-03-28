pipeline{
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

        stage('public to jfrog'){
            agent any
            rtServer (
    id: "Artifactory-1",
    url: "http://localhost:8081/artifactory",
    // If you're using username and password:
    username: "jenkinsuser",
    password: "password123"
    // If you're using Credentials ID:
    
    // If Jenkins is configured to use an http proxy, you can bypass the proxy when using this Artifactory server:
    bypassProxy: true
    // Configure the connection timeout (in seconds).
    // The default value (if not configured) is 300 seconds:
    timeout = 3000
)
rtUpload (
    serverId: "Artifactory-1",
    spec:
        """{
          "files": [
            {
              "pattern": "target/*.jar",
              "target": "libs-release/myJavaProject/"
            }
         ]
        }"""
)

        }
        }
}

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
                sh 'npm install'
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
        }
}

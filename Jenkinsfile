pipeline{
    
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn install -e -DskipTests=true'
            }
        }

        stage('Sample'){
            steps{
                echo 'This is stage 2'
            }
        }

        
        stage('upload artifacts to jfrog'){
            agent any
            steps{
                script {
                    def server = Artifactory.newServer url: 'http://localhost:8081/artifactory/', username: 'jenkinsuser', password: 'password123'
                    def uploadSpec = """{
  "files": [
    {
      "pattern": "target/*.jar",
      "target": "libs-release/MyTestApp/test.jar"
    }
 ]
}"""
server.upload(uploadSpec)
                }
            }
        }

        }
}

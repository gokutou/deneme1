pipeline{
    agent any

    tools {
         maven '1'
         jdk '1'
    }

    stages{
        stage('checkout'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github access', url: 'https://github.com/sreenivas449/java-hello-world-with-maven.git']]])
            }
        }
        stage('get_version'){
            steps {
                script {
                    def version = sh(script: 'mvn help:evaluate -Dexpression=project.version -q -DforceStdout', returnStdout: true).trim()
                    def artifactId = sh(script: 'mvn help:evaluate -Dexpression=project.artifactId -q -DforceStdout', returnStdout: true).trim()

                    echo "Project Version: ${version}"
                    echo "Artifact ID: ${artifactId}"
                }

        }
        stage('build'){
            steps{
               bat 'mvn package'
            }
        }
    }
}

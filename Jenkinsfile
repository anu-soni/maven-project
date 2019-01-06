pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                echo 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                
                }
            }
        }
    }
}
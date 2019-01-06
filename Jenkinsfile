pipeline {
    agent any

    parameters {
		 string(name: 'tomcat_dev', defaultValue: '18.219.93.152', description: 'Staging Server')
         	 string(name: 'tomcat_prod', defaultValue: '3.17.59.240', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
	
        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        bat "echo y | pscp -i D:/devops/tomcat-demo.ppk D:/devops/jenkins/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat8/webapps"
                    }
                }
		    
		stage ("Deploy to Production"){
                    steps {
                        bat "echo y | pscp -i D:/devops/tomcat-demo.ppk D:/devops/jenkins/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat8/webapps"
                    }
                }
            }
        }
    }
}

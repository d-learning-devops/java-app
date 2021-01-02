pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
        stage('Build') {
            steps {
                git 'https://github.com/d-learning-devops/java-app.git'
                sh "mvn clean install"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'server/target/*.jar'
                }
            } 
        }
        stage('Deploy') {
        	steps {
        	   sh '''sudo /opt/tomcat/bin/shutdown.sh
                    sudo cp webapp/target/webapp.war /opt/tomcat/webapps/
                    sudo /opt/tomcat/bin/startup.sh'''
        	}
        }
	    stage('Sample') {
        	steps {
        	    echo 'Sample Stage'
        	}
	    }
    }
}

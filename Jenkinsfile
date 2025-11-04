pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
        jdk 'JDK17'
    }

    environment {
        DEPLOY_URL = 'http://localhost:8080/manager/text'
        DEPLOY_USER = 'chandu'
        DEPLOY_PASS = 'passwd'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Chandrakanth-Git-Hub/sample.git', branch: 'main'
                  }
    }

    stage('Build') {
            steps  {
                    sh 'mvn clean package'
	}
    }

    stage('Test') {
            steps {
                    sh 'mvn test'
       }
    }

    stage('Deploy to Tomcat') {
            steps {
    //                echo 'Deploying WAR file to Tomcat...'
    //                sh 'cp target/sample-app-1.0-SNAPSHOT.jar /opt/tomcat/webapps/'
	sh '''
        	docker build -t sampleapp:latest .
        	docker run -d -p 8081:8080 sampleapp:latest
        	'''
	    }	
        }
    }

    post {
    success {
        emailext(
            subject: "SUCCESS: ${currentBuild.fullDisplayName}",
            body: "Build SUCCESSFUL: ${env.BUILD_URL}",
            to: "chandubhavi123@gmail.com"
        )
    }
    failure {
        emailext(
            subject: "FAILURE: ${currentBuild.fullDisplayName}",
            body: "Build FAILED: ${env.BUILD_URL}",
            to: "chandubhavi123@gmail.com"
            )
        }
    } 
}

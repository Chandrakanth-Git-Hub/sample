pipeline {
    agent any

    environment {
        MAVEN_HOME = "/opt/apache-maven"
        PATH = "$MAVEN_HOME/bin:$PATH"
        DEPLOY_PATH = "/opt/tomcat/webapps"
                }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Chandrakanth-Git-Hub/sample.git', branch: 'main'
                  }
    }

    stage('Build') {
            steps  {
 //		dir('sample-app') {
                    sh 'mvn clean package'
   //         }
	}
    }

    stage('Test') {
            steps {
 //		dir('sample-app') {
                    sh 'mvn test'
   //       }
       }
    }

    stage('Deploy to Tomcat') {
            steps {
 //		dir('sample-app') {
                    echo 'Deploying WAR file to Tomcat...'
                    sh 'cp target/sample-app-1.0-SNAPSHOT.jar /opt/tomcat/webapps/'
   //             }
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

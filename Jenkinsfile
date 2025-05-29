pipeline {
    agent any

    environment {
        MAVEN_HOME = tool name: 'maven_3.9.7', type: 'maven'
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out code..."
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building with Maven..."
                sh 'mvn clean package'
            }
        }

        stage('Archive WAR') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        // Optional Deployment Stage (Requires configuration)
        // stage('Deploy to Tomcat') {
        //     steps {
        //         echo "Deploying WAR to Tomcat..."
        //         sh '''
        //         curl --upload-file target/sample-webapp.war \
        //              --user tomcat:yourpassword \
        //              http://localhost:8080/manager/text/deploy?path=/sample-webapp&update=true
        //         '''
        //     }
        // }
    }

    post {
        success {
            echo "Build succeeded!"
        }
        failure {
            echo "Build failed."
        }
    }
}

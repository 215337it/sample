pipeline {
    agent any
    tools {
        maven 'local_maven'  // Ensure Maven is configured in Jenkins tool settings
    }
    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package'  // Replace 'sh' with 'bat' for Windows
            }
            post {
                success {
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to tomcat server') {
            steps {
              deploy adapters: [tomcat9(credentialsId: 'Tomcat_Credentials', path: '', url: 'http://localhost:8090/manager/text/deploy')], contextPath: null, war: '**/*.war'
            }
        }
    }
}

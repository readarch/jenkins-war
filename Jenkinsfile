pipeline {
    agent any
    
    tools {
        maven 'mvn-3.8.7'
    }

    stages {
        stage ('Building ...') {
            steps {
                echo 'Maven cleaning and packaging ...'
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts ...'
                    archiveArtifacts artifacts: '**/target/*.war', followSymlinks: false
                }
            }
        }
        
        stage ('Deploying to Tomcat Server ...') {
            steps {
                echo 'Deploying adapters ...'
                deploy adapters: [tomcat9(credentialsId: 'tomcat_credential', path: '', url: 'http://localhost:8085/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}

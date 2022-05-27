pipeline {
    agent any
    
    stages {
        stage('Branch indexing: abort') {
            when {
                allOf {
                    triggeredBy cause: "BranchIndexingCause"
                    not { 
                        changeRequest() 
                    }
                }
            }
            steps {
                script {
                    echo "Branch discovered by branch indexing"
                    currentBuild.result = 'SUCCESS' 
                    error "Caught branch indexing..."
                }
            }
        }
        stage('Build Docker image') {
            steps {
                sh 'docker build -t docker-getting-started .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -dp 3000:3000 docker-getting-started'
            }
          }
    }
}

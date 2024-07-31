pipeline {
    agent any
    
    environment {
        AWS_DEFAULT_REGION = 'us-west-1'  // Set your desired region
        S3_BUCKET = 'my-jenkins-website'  // Your S3 bucket name
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Clone the repository containing the index.html file
                git branch: 'main', url: 'https://github.com/varush1709/Hospital_page_project.git'
            }
        }
        stage('Unzip') {
            steps {
                // Ensure the unzip command is available and unzip the file
                sh 'which unzip || sudo apt-get install unzip -y'
                sh 'unzip aws.zip -d website'
            }
        }
        
        stage('Upload to S3') {
            steps {
                // Install AWS CLI if not already installed
                sh 'which aws || pip install awscli'
                
                // Upload index.html to S3 bucket
                sh '''
                    aws s3 cp aws.html s3://${S3_BUCKET}/ --acl public-read
                '''
            }
        }
    }
    
    post {
        success {
            echo 'Website successfully deployed!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}


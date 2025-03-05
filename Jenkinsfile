pipeline {
    agent any
    
    environment {
        AWS_ACCESS_KEY_ID = credentials('AKIAR7HWYGMF7O3YXAK')  // Or set environment variables for your AWS credentials
        AWS_SECRET_ACCESS_KEY = credentials('OWo6qQuwy6zUc2CYhvhrF4HnyABZKjBclW7RYq5K')
        AWS_REGION = 'us-east-2'  // Adjust the region as needed
    }

    stages {
        stage('Git Checkout') {
            steps {
                // Pull your Git repository
                git 'https://github.com/Jenkins.git'
            }
        }
        
        stage('Launch EC2 Instance') {
            steps {
                script {
                    def instanceType = 't2.micro'  // Adjust instance type as needed
                    def amiId = 'ami-0fc82f4dabc05670b'  // Provide your desired AMI ID
                    
                    sh """
                        aws ec2 run-instances \
                            --image-id ${amiId} \
                            --instance-type ${instanceType} \
                            --count 1 \
                            --key-name your-key-pair \
                            --security-group-ids sg-xxxxxxxx \
                            --subnet-id subnet-xxxxxxxx \
                            --region ${AWS_REGION}
                    """
                }
            }
        }
    }
}


pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('AKIAR7HWYGMF7O3YXAK')
        AWS_SECRET_ACCESS_KEY = credentials('OWo6qQuwy6zUc2CYhvhrF4HnyABZKjBclW7RYq5K')
        AWS_REGION = 'us-east-2'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/Vpraveen229/Jenkins/blob/main/Jenkinsfile'
            }
        }

        stage('Create/Update Auto Scaling Group') {
            steps {
                script {
                    // Create or update your Auto Scaling Group configuration
                    sh """
                        aws autoscaling create-auto-scaling-group \
                            --auto-scaling-group-name my-auto-scaling-group \
                            --launch-configuration-name my-launch-config \
                            --min-size 1 \
                            --max-size 10 \
                            --desired-capacity 1 \
                            --availability-zones us-east-1a \
                            --vpc-zone-identifier subnet-066518d1d93ba9db1
                    """
                }
            }
        }
        
        stage('Apply Scaling Policies') {
            steps {
                script {
                    // Define or update scaling policies
                    sh """
                        aws autoscaling put-scaling-policy \
                            --auto-scaling-group-name my-auto-scaling-group \
                            --policy-name scale-up-policy \
                            --scaling-adjustment 1 \
                            --adjustment-type ChangeInCapacity
                    """
                    sh """
                        aws autoscaling put-scaling-policy \
                            --auto-scaling-group-name my-auto-scaling-group \
                            --policy-name scale-down-policy \
                            --scaling-adjustment -1 \
                            --adjustment-type ChangeInCapacity
                    """
                }
            }
        }
    }
}


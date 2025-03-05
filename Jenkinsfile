pipeline {
    agent any
    environment {
        AWS_REGION = 'us-east-1'
        AMI_ID = 'ami-12345678'
        INSTANCE_TYPE = 't2.micro'
        KEY_NAME = 'my-key'
        SECURITY_GROUP = 'sg-12345678'
        SUBNET_ID = 'subnet-12345678'
        GIT_REPO = 'https://github.com/your-username/your-repo.git'
    }
    stages {
        stage('Clone Git Repository') {
            steps {
                script {
                    sh "rm -rf myrepo && git clone ${GIT_REPO} myrepo"
                }
            }
        }
        stage('Launch EC2 Instance') {
            steps {
                script {
                    def launchCommand = """
                    aws ec2 run-instances --image-id ${AMI_ID} --count 1 --instance-type ${INSTANCE_TYPE} \
                    --key-name ${KEY_NAME} --security-group-ids ${SECURITY_GROUP} \
                    --subnet-id ${SUBNET_ID} --region ${AWS_REGION} \
                    --query 'Instances[0].InstanceId' --output text
                    """
                    def instanceId = sh(script: launchCommand, returnStdout: true).trim()
                    echo "Launched EC2 Instance: ${instanceId}"
                }
            }
        }
    }
}


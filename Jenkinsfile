pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/jenkins.git'
            }
        }

        stage('Execute Script') {
            steps {
                sh 'chmod +x script.sh && ./script.sh'  // For shell scripts
                // sh 'python3 script.py'  // Uncomment to execute a Python script
            }
        }
    }
}

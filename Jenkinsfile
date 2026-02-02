pipeline {
    agent { label 'autoscale-agent' }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Balaji-official-006/jenkins-project.git'
            }
        }

        stage('Build') {
            steps {
                echo "Build step (static app)"
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['deploy-key']) {
                    sh """
                    ssh new.pem ec2-user@10.0.138.94 '
                      sudo rm -rf /usr/share/nginx/html/*
                      sudo cp -r * /usr/share/nginx/html/
                    '
                    """
                }
            }
        }
    }
}

pipeline {
    agent { label 'agent-1' }

    options {
        skipDefaultCheckout(true)
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/MUKESHMUU/AWS-Jenkins-Project.git'
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
                    sh '''
                    # Create temp directory on target
                    ssh -o StrictHostKeyChecking=no ubuntu@172.31.38.210 \
                    "mkdir -p /tmp/webapp"

                    # Copy project files
                    scp -o StrictHostKeyChecking=no -r ./* \
                    ubuntu@172.31.38.210:/tmp/webapp

                    # Deploy to Nginx web root
                    ssh -o StrictHostKeyChecking=no ubuntu@172.31.38.210 \
                    "sudo rm -rf /var/www/html/* && \
                     sudo cp -r /tmp/webapp/* /var/www/html/"
                    '''
                }
            }
        }
    }
}

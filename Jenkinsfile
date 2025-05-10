pipeline {
    agent any
    environment {
        SSH_KEY = credentials('ssh-production-key')
        USER = 'ec2-user'
    }
    stages {
        stage('Deploy to Testing') {
            steps {
                sh '''
                ssh -oStrictHostKeyChecking=no -i $SSH_KEY $USER@54.82.127.75 '
                    sudo dnf update -y &&
                    sudo dnf install git -y &&
                    sudo dnf install -y httpd &&
                    sudo systemctl start httpd &&
                    sudo git clone https://github.com/eduval/Kelownatrails /var/www/html
                '
                '''
            }
        }
        stage('Deploy to Staging') {
            steps {
                sh '''
                ssh -oStrictHostKeyChecking=no -i $SSH_KEY $USER@3.87.240.209 '
                    sudo dnf update -y &&
                    sudo dnf install git -y &&
                    sudo dnf install -y httpd &&
                    sudo systemctl start httpd &&
                    sudo git clone https://github.com/eduval/Kelownatrails /var/www/html
                '
                '''
            }
        }
        stage('Deploy to Production') {
            steps {
                sh '''
                ssh -oStrictHostKeyChecking=no -i $SSH_KEY $USER@54.211.159.130 '
                    sudo dnf update -y &&
                    sudo dnf install git -y &&
                    sudo dnf install -y httpd &&
                    sudo systemctl start httpd &&
                    sudo git clone https://github.com/eduval/Kelownatrails /var/www/html
                '
                '''
            }
        }
    }
}

pipeline {
    agent any

    stages {
        stage('Update System') {
            steps {
                echo 'Updating package lists...'
                sh 'sudo apt update'
            }
        }

        stage('Install Apache2') {
            steps {
                echo 'Installing Apache2...'
                sh '''
                    sudo apt install apache2 -y
                    sudo systemctl start apache2
                    sudo systemctl enable apache2
                '''
            }
        }

        
        stage('Check System Logs for 4xx/5xx Errors') {
            steps {
                echo 'Checking system logs via journalctl...'
                sh '''
                    sudo journalctl -xe | grep -E ' 4[0-9]{2} | 5[0-9]{2} ' || echo "No 4xx/5xx errors found in system logs."
                '''
            }
        }
    }
}

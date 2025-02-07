pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'git@github.com:Balaji-Jeyachandran/php.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'composer install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'php -l index.php'  // Simple syntax check for PHP files
            }
        }

        stage('Deploy to Local Apache') {
            steps {
                sh '''
                sudo systemctl stop apache2
                sudo rm -rf /var/www/html/Oxer
                sudo cp -r /mnt/a/github/php/ /var/www/html/Oxer
                sudo chown -R www-data:www-data /var/www/html/Oxer
                sudo chmod -R 755 /var/www/html/Oxer
                sudo systemctl start apache2
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'curl -s http://balaji.geocareindia.com | grep "Welcome to PHP App"'
            }
        }
    }
}

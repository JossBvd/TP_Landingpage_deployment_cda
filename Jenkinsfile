pipeline {
    agent any
    stages {
        stage('Continous Integration') {
            steps {
                git branch: 'main', url: 'https://github.com/JossBvd/TP_Landingpage_deployment_cda'
            }
        }
        stage('Sonarcube') {
            steps {
                sh """
                    sonar-scanner \
                    -Dsonar.projectKey=jocelyn-td-landing-page \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=https://669b-212-114-26-208.ngrok-free.app \
                    -Dsonar.token=${SONAR_TOKEN}
                """
            }
        }
        stage('Deploy via FTP') {
            steps {
                sh '''
                    lftp -d -u $jocelyn_ftp_nom,$jocelyn_ftp_mdp ftp-jocelyn1.alwaysdata.net -e "
                        mirror -R /home/jenkins/workspace/jocelyn-td-landing-page/ www/;
                        bye
                    "
                '''
            }
        }
    }
}

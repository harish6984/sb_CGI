pipeline {

    agent any

    stages{

        stage('Fetch Code') {
            steps {
                git branch: 'master', url: 'https://github.com/harish6984/sb_CGI.git'
            }
        }
        stage('BUILD'){
            steps {
                sh 'mvn install'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                    }
                }
        }

        stage('UNIT TEST'){
            steps {
                sh 'mvn test'
            }
        }

    }

}



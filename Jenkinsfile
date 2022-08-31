pipeline {

    agent any

    stages{

        stage('Fetch Code') {
            steps {
                git branch: 'paac', url: 'https://github.com/harish6984/sb_CGI.git'
            }
        }
        stage('BUILD'){
            steps {
                sh 'mvn install'
            }
        }

        stage('UNIT TEST'){
            steps {
                sh 'mvn test'
            }
        }

    }

}



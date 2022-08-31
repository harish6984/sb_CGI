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
                    archiveArtifacts artifacts: '**/target/*.jar'
                    }
                }
        }

        stage('UNIT TEST'){
            steps {
                sh 'mvn test'
            }
        }
		
		stage('Checkstyle Analysis'){
            steps {
                sh 'mvn checkstyle:checkstyle'

			}
		}
		stage('CODE ANALYSIS with SONARQUBE') {
             environment {
                scannerHome = tool 'sonar4.7'
             }
             steps {
                withSonarQubeEnv('SonarCloud') {
                    sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=harish6984_sb_CGI \
                    -Dsonar.projectName=sb_CGI \
                    -Dsonar.projectVersion=1.0 \
                    -Dsonar.sources=src/ \
                    -Dsonar.java.binaries=target/test-classes/com/example/helloworld/controller/ \
                    -Dsonar.junit.reportsPath=target/surefire-reports/ \
                    -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                    -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
                }


             }
        }

    }
}

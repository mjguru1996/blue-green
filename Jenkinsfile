pipeline{
    agent any
    environment{
        SCANNER_HOME = tool 'sonar-scanner'
    }
    stages{
        stage('SCM CHECKOUT'){
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/mjguru1996/blue-green.git'
            }
        }
        stage('SONARQUBE ANALYSIS'){
            steps{
                withSonarQubeEnv('sonar') {
                    sh "${SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=nodejsmysql -Dsonar.projectName=nodejsmysql"
                }
            }
        }
    }
}
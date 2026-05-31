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
        stage('Trivy FS Scan') {
            steps {
                sh "trivy fs --format table -o fs.html ."
            }
        }
        stage('Docker Build') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred') {
                        sh "docker build -t adijaiswal/app:blue ."}
                }
            }
        }
        stage('Trivy Image Scan') {
            steps {
                sh "trivy image --format table -o image.html adijaiswal/app:blue"
            }
        }

    }
}
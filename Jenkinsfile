pipeline{
    agent any
    stages{
        stage('SCM CHECKOUT'){
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/mjguru1996/blue-green.git'
            }
        }
    }
}
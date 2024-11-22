pipeline{
    agent any
    stages{
        stage('Checkout project'){
            steps{
                git branch: 'main', url:'https://github.com/JD-Lora1/saamfi2-h2.git'
            }
        }
        stage('Project Build'){
            steps{
                sh 'chmod +x mvnw'
                sh './mvnw clean package -DskipTests'
            }
        }
        stage('Deploy'){
            steps{
                sshagent(['dokku']){
                    sh 'git remote remove dokku || true'
                    sh 'git remote add dokku dokku@172.23.239.221:saamfi-h2 || true'
                    sh ' GIT_SSH_COMMAND="ssh -o StrictHostKeyChecking=no" git push dokku main -f'
                }
            }
        }
    }
}

pipeline {
    agent  { node { label 'Node02' } }
    stages {
        def mvnHome
        stage('Code Checkout'){
            steps {
                sh 'rm -rf /var/lib/jenkins/workspace/Adaptive_Pipeline/shopizer'
                sh 'git clone https://github.com/Rasmi20/shopizer.git'
                mvnHome = tool 'M3'
            }
        }
 
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}

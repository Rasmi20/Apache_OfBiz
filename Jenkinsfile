pipeline {
    agent  { node { label 'Node02' } }
    stages {
        stage('Build') {
            steps {
                source /etc/profile.d/maven.sh
                mvn clean install
                
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

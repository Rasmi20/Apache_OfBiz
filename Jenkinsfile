pipeline {
    agent any
    stages {
		def mvnHome 
        stage('Codecheckout') {
            steps {
                sh '''
                   sh 'rm -rf /var/lib/jenkins/workspace/Adaptive_Pipeline/shopizer'

					sh 'git clone https://github.com/Rasmi20/shopizer.git'
					mvnHome = tool 'M3' 
                '''
            }
        }
   
        stage('Build & Package') {
            steps {
                sh 'echo "Hello World"'
                sh '''
					source /etc/profile.d/maven.sh
                    cd /var/lib/jenkins/workspace/Adaptive_Pipeline/shopizer;

					mvn clean install
                '''
            }
        }
   
        stage('Build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }
    }
}

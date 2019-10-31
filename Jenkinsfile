pipeline {
    agent node02
    stages {
        stage ('Clone') {
            steps {
                git branch: '2.6.0', url: "https://github.com/Rasmi20/shopizer.git/"
            }
        }

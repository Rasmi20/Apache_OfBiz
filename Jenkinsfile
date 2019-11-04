node('Node02'){
    
    def mvnHome
    stage('Code Checkout'){
        checkout scm
        mvnHome = tool 'M3'     
    }
    
    
    stage('Build & Package') {
        sh ''' 
        source /etc/profile.d/maven.sh
        

        cd /var/lib/jenkins/workspace/mlpipeline_2.6.0;

        mvn clean install
      '''
   }
   
   stage('Static Code Analysis'){
       sh '''
       source /etc/profile.d/maven.sh
       cd /var/lib/jenkins/workspace/mlpipeline_2.6.0;
       mvn clean verify sonar:sonar
       '''
   }
   
    
    
  }

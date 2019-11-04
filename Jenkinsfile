node('Node02'){
    
    def mvnHome
    stage('Code Checkout'){
        checkout scm
        mvnHome = tool 'M3'     
    }
    
    stage('Build & Package') {
        sh ''' 
        cd shopizer
        mvn clean install
      '''
   }
   
   stage('Static Code Analysis'){
       sh '''
       source /etc/profile.d/maven.sh
       cd shopizer;
       mvn clean verify sonar:sonar
       '''
   }
   
    
    
  }

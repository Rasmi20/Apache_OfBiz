node('Node02'){
    
    def mvnHome
    stage('Code Checkout'){
       mvnHome = tool 'M3'     
    }
    
    stage('Build & Package') {
        sh ''' 
        source /etc/profile.d/maven.sh
        

        

        mvn clean install
      '''
   }
   
   stage('Static Code Analysis'){
       sh '''
       source /etc/profile.d/maven.sh
      
       mvn clean verify sonar:sonar
       '''
   }
}
   
    

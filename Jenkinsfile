node('Node02'){
    
    def mvnHome
    stage('Code Checkout'){
        sh 'rm -rf /var/lib/jenkins/workspace/Adaptive_Pipeline/shopizer'

        sh 'git clone https://github.com/Rasmi20/shopizer.git'
        mvnHome = tool 'M3'
        
    }
    
    stage('Build & Package') {
        sh ''' 
        source /etc/profile.d/maven.sh
        

        cd /var/lib/jenkins/workspace/Adaptive_Pipeline/shopizer;

        mvn clean install
      '''
   }
   
   stage('Static Code Analysis'){
       sh '''
       source /etc/profile.d/maven.sh
       cd /var/lib/jenkins/workspace/Adaptive_Pipeline/shopizer;
       mvn clean verify sonar:sonar
       '''
   }
   
    stage('Binary Store'){
       sh '''
       curl -u admin:admin -T /var/lib/jenkins/workspace/Adaptive_Pipeline/shopizer/sm-shop/target/ROOT.war "http://10.134.95.194:8081/artifactory/generic-local/var/lib/jenkins/workspace/java_app/sm-shop/target/ROOT.war"
   '''
   }
    stage('Containerize'){
       sh ''' cd /var/lib/jenkins/workspace/Adaptive_Pipeline/shopizer/sm-shop;
       docker build . -t rasmi20/assignment:demo1 '''
   }
   
        
        registry = "rasmi20/assignment"
          
          
        withDockerRegistry(credentialsId: 'da0b3ace-c316-42fa-aed3-9b5cbe6cc01e', url: 'https://index.docker.io/v1/') {
         sh 'docker push rasmi20/assignment:demo1'
    }
  
   stage('Test deploy'){
       sh '''
       ansible-playbook /var/lib/jenkins/pyflow/javatest.yml
       '''
   }
    stage('Model Integration'){
       sh '''
       python3 /var/lib/jenkins/testsuite/python/model/API-Final.py
       '''  
   }
   stage('Test'){
       sh '''
       python /var/lib/jenkins/testsuite/python/run_test.py
       '''
   }  
   stage('Prod deploy'){
        sh '''
       ansible-playbook /var/lib/jenkins/pyflow/javatest_prod.yml
       '''
   }
}

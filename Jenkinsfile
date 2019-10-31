pipeline {
agent {
node('Node02'){
    
    def mvnHome
    stage('Code Checkout'){
        sh 'rm -rf /var/lib/jenkins/workspace/Adaptive_Pipeline_TC_Prioritization/adaptive_pipeline'

        sh 'git clone http://10.134.95.191/bala/adaptive_pipeline.git'
        mvnHome = tool 'M3'
        
    }
    
    stage('Build & Package') {
        sh ''' 
        source /etc/profile.d/maven.sh
        

        cd /var/lib/jenkins/workspace/Adaptive_Pipeline_TC_Prioritization/adaptive_pipeline;

        mvn clean install
      '''
   }
   
   stage('Static Code Analysis'){
       sh '''
       source /etc/profile.d/maven.sh
       cd /var/lib/jenkins/workspace/Adaptive_Pipeline_TC_Prioritization/adaptive_pipeline;
       mvn clean verify sonar:sonar
       '''
   }
   
    stage('Binary Store'){
       sh '''
       curl -u admin:admin -T /var/lib/jenkins/workspace/Adaptive_Pipeline_TC_Prioritization/adaptive_pipeline/sm-shop/target/ROOT.war "http://10.134.95.194:8081/artifactory/generic-local/var/lib/jenkins/workspace/java_app/sm-shop/target/ROOT.war"
   '''
   }
    stage('Containerize'){
       sh ''' cd /var/lib/jenkins/workspace/Adaptive_Pipeline_TC_Prioritization/adaptive_pipeline/sm-shop;
       docker build . -t balabkool/bala_docker:demo2 '''
   }
   
        
        registry = "balabkool/bala_docker"
          
          
        withDockerRegistry(credentialsId: '6cdaac3b-b34c-43ba-9f95-76d5c46774ce', url: 'https://index.docker.io/v1/') {
         sh 'docker push balabkool/bala_docker:demo2'
    }
  
   stage('Test deploy'){
       sh '''
       ansible-playbook /var/lib/jenkins/pyflow/javatest.yml
       '''
          }
    stage('Model Integration'){
       
       sh '''
       python /var/lib/jenkins/testsuite/python/model/input.py
       ''' 
       sleep(100)
       
       sh '''
       python3 /var/lib/jenkins/testsuite/python/model/API-Final1.py
       ''' 
       sleep(100)
   }
   stage('Test'){
       sh '''
       python /var/lib/jenkins/testsuite/python/run_test.py
       '''
       sleep(100)
   }  
   stage('Prod deploy'){
        sh '''
       ansible-playbook /var/lib/jenkins/pyflow/javatest_prod.yml
       '''
   }
}
}
}

pipeline {
    agent any
	
    parameters {      
	choice(name: 'CHOICE', choices: ['Dev','Qa', 'Master'], description: 'Select branch')
       
    }
    stages {
       
        stage('Checkout') {
		
            steps {
                
             checkout([$class: 'GitSCM', branches: [[name:"${CHOICE}"  ]], 
             doGenerateSubmoduleConfigurations: false, 
             extensions: [], submoduleCfg: [], userRemoteConfigs:
             [[credentialsId: '5dc47f1f-542f-42d2-b5a6-1d2ec6cdcf5e', url: 'https://github.com/sohailshaikh001/Mavenwarproject.git']]])
    
            }
        }
        
        stage('build'){
		tools {
        	maven 'Maven_home' 
  			  }
        steps{
          
            bat "mvn clean install package"
           
           }
        }
	    
	    stage('sonarqube'){
		    steps{
		withSonarQubeEnv('MySonarQubeServer'){
			bat "mvn sonar:sonar"
					}
	    		}
	    }
        
        
    }
}

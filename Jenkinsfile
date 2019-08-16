pipeline {
    agent {
        node { 
  		label 'master'
  		customWorkspace 'D:/jenkins_ws/ws1' 
  	    } 

    }
    
    options{
  	buildDiscarder(logRotator(numToKeepStr:'5'))
  	timeout(time : 30, unit: 'MINUTES')
  }


    
    stages {
    
        stage('build') {
            steps {
                  deleteDir()
		          git(url: 'https://github.com/KritikaSri/Pet_clinic.git', branch: 'master')

            }
        }
        
        stage('Build') {
            steps {
               
                echo "maven clean build"
               
                	
   		            bat 'mvn clean compile package'   
                
            }
        }  
        /*
        stage('SCA_Sonar') {
            steps {
                    
   		            bat 'mvn sonar:sonar'   
                //}
            }
        }
        */
        stage('Test') {
            steps {
                
                    
                    bat 'mvn test'
               
	        }
        }
        
        stage('code_coverage') {
            steps {
                jacoco(deltaBranchCoverage: '10', deltaClassCoverage: '10', deltaComplexityCoverage: '10', deltaInstructionCoverage: '10', deltaLineCoverage: '10', deltaMethodCoverage: '20')
            }
        }
        
        
        
        stage('Tomcat Deploy') {
            steps {
               bat returnStatus: true, script: 'copy .\\target\\petclinic.war D:\\Prog_Files\\Tomcat\\apache-tomcat-8.5.34\\webapps\\'
            }
        }


    }
}

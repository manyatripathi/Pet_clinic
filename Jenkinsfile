def FAILED_STAGE
pipeline 
 {

	tools
	{
		maven 'MAVEN_HOME'
		jdk 'JAVA_HOME'
	}
	options
	{
		buildDiscarder(logRotator(numToKeepStr: '3', artifactNumToKeepStr: '3'))
		
	}
	agent 
	{
		node 
		{	
			label ''
		}
	}
	stages
	{
		
		stage('code checkout')
		{
			steps
			{
				script
				{
					FAILED_STAGE=env.STAGE_NAME
				}
				git 'https://github.com/manyatripathi/Pet_clinic'
				sh "mvn clean"
			}
	  
		}
		stage('compile')
		{
			
		  	steps
			{
				script
				{
					FAILED_STAGE=env.STAGE_NAME
				}
				sh "mvn compile"
			}
			
	  
		}
                /*stage('unit test')
		{
			steps
			{
				bat "mvn test "
				
				
			}
		}
                stage('code coverage')
		{
			steps
			{
				bat 'mvn package'
				
			}
		}
		stage('sonarqube analysis')
		{
			
			steps
			{
				script
				{
					FAILED_STAGE=env.STAGE_NAME
				}
				withSonarQubeEnv('Sonar')
				{
					bat 'mvn sonar:sonar -Dsonar.host.url=http://10.76.81.93:2500' 
				}	
				timeout(time: 10, unit: 'MINUTES') 
                               
				{
					waitForQualityGate abortPipeline: true
				} 
			}
		}
		*/	
		stage('performance and security')
		{
				steps
					{
						//bat "mvn findbugs:findbugs"
					
						sh "mvn verify"
					}
		}
		stage('war')
		{
			steps
			{
				script
				{
					FAILED_STAGE=env.STAGE_NAME
				}
				bat "mvn war:war "
			}
		}
                /*
		stage('deploy to artifactory')
		{
			steps
			{
				sh "mvn deploy"
			}
		}*/
		//stage('integration testing')
		//{
		//	steps
		//	{ 
		//		bat "mvn integration-test"
		//	}
		//}
		
	 }
	}
  

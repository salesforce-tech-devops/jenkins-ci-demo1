pipeline {
    agent any
	
    triggers {
         pollSCM('* * * * *')
     }

stages
	{
		stage ('Pck n deploy to salesforce stg')
		{

			 steps{
			 build job: 'sf_stg_depoy'
			 }
		}  

		stage ('deploy to prod')
		{
		  
			  steps
			  {
				timeout(time:7, unit:'DAYS'){
					input message:'Approve PROD DEPOYMENT';
					}
					build job: 'sf_prod_depoy'
			  }
			  
			  post 
			  {
					success {
						echo 'Code deployed successfully to production.'
					
					}
					failure {
					
						echo 'Deployment failed. Plz check the build logs'
					}
				  
			  }

		}

	}
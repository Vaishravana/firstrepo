pipeline{
    environment {
    async_test_number = 1
	}
	agent {
	label 'MAIN_FOUR_TARGETS'
	}  	
	stages{
		stage('async test 1'){
		    steps{
			    script{
				    catchError {
					    build job: 'dummy_repo2'		
				    }
	            }
		    }
		}
		stage('async test 2'){
		    steps{
				script{
					catchError {
					    build job: 'dummy_repo2'			
					}
			    }
		    }
		    post{
                success {
                    echo "Test pass"
                }
                failure {
                    script{
					    try{
						    build job: 'dummy_firmware_reload'		
					    }
					    catch(err){
					        mail bcc: '', body: 'Just  do it.', cc: '', from: '', replyTo: '', subject: 'Reset the board now!!', to: 'vaishravana.s@gmail.com'
                            error('Reset failed')
				       }
			        }
                }
			}
		}
		stage('async test 3'){
		    steps{
				script{
					catchError {
					    build job: 'dummy_repo2'			
					}
			    }
		    }
		    post{
                success {
                    echo "Test pass"
                }
                failure {
                    script{
					    try{
						    build job: 'dummy_firmware_reload'		
					    }
					    catch(err){
					        mail bcc: '', body: 'Just  do it.', cc: '', from: '', replyTo: '', subject: 'Reset the board now!!', to: 'vaishravana.s@gmail.com'
                            error('Reset failed')
				       }
			        }
                }
			}
		}
    }
}

void setBuildStatus(String message, String state) {
  step([
      $class: "GitHubCommitStatusSetter",
      reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/Vaishravana/firstrepo"],
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "context-name-1"],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}
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
		    setBuildStatus("Build pass", "SUCCESS");
                }
                failure {
                    script{
					    try{
						    build job: 'dummy_firmware_reload'		
					    }
					    catch(err){
                            error('Reset failed')
				       }
			        }
                }
			}
		}
		stage('async test 3'){
		    steps{
			    	sh '''cd test_dir
				python3 test2.py --sum 1 2 3'''
		    }
		    post{
                success {
                    echo "Test pass"
			
	            setBuildStatus("Build succeeded", "SUCCESS");
                }
                failure {
                    script{
					    try{
						    build job: 'dummy_firmware_reload'		
					    }
					    catch(err){
						setBuildStatus("Build failed", "FAILURE");

                            error('Reset failed')
				       }
			        }
                }
			}
		}
    }
}

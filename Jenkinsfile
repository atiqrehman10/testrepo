pipeline {
	agent any
	environment {
    SANITY = true
	}
	stages {
		stage('build') {
			steps {
				echo "I am building it"
			}
		}
		stage('test') {
			steps {
				echo "Testing now"
 				sh '''#!/bin/bash
                 			echo "hello world"
					./robot-runner.sh
         			    '''
			}
			post {
			     always {
						 when { environment name: 'SANITY', value: 'false' }
							 steps {
								 echo 'SANITY is false'
							 }
						when { environment name: 'SANITY', value: 'true' }
								 steps {
									 echo 'SANITY is true'
								 }

								 robot 'results'
			     }
			}
		}
	}
}

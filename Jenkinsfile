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
			when { environment name: 'SANITY', value: 'false' }
				steps {
					echo 'SANITY is false'
				}
		}
		 post {
			     always {
								 robot 'results'
			     }
		 }
	}
}

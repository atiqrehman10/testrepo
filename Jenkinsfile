pipeline {
	agent any
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
			     	     robot 'results'
			     } 
			}
		}
	}
}

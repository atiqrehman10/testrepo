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
 				bash '''#!/bin/bash
                 			echo "hello world" 
					./robot-runner.sh
         			    '''				
			}
		}
	}
}

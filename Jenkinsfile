pipeline {
	agent any
	environment {
    //  If the gerrit build has set tag "SANITY", then the variable "SANITIZE" is true.
    IS_GERRIT_BUILD = "${JOB_NAME == 'tools.pa.gerrit'}"
    GIT_TAG = sh(script: 'git tag -l', returnStdout: true).trim()
    IS_SANITY = "${GIT_TAG == 'SANITY' ? true: false}"
    SANITIZE = "${IS_GERRIT_BUILD == 'true' && IS_SANITY == 'true'}"
  }
	stages {
		stage('build') {
			steps {
				echo "I am building it!"
			}
		}
		stage('test') {
			steps {
        //Clean workspace before build starts.
        sh 'git clean -fxd .'
        sh '''#!/bin/bash -le
              echo "JOB NAME:  ${JOB_NAME}"
              echo "IS GERRIT: ${IS_GERRIT_BUILD}"
              echo "GIT TAG:   ${GIT_TAG}"
              echo "IS SANITY: ${IS_SANITY}"
              echo "SANITIZE:  ${SANITIZE}"

              git tag -l '''

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

pipeline {
	agent any
	environment {


    // If the gerrit build has set tag "SANITY", then the variable "SANITIZE" is true.
    IS_GERRIT_BUILD = "${currentBuild.projectName.contains('tools.pa.gerrit')}"
    GIT_TAG = sh(script: 'git tag -l', returnStdout: true).trim()
    IS_FULL = "${GIT_TAG == 'FULL' ? true: false}"
    SANITIZE = "${IS_GERRIT_BUILD == 'true' && IS_FULL == 'false'}"
  }
	stages {
		stage('build') {
			steps {
				echo "I am building it"
			}
		}
		stage('test') {
			steps {
        //Clean workspace before build starts.
        sh 'git clean -fxd .'
        sh '''#!/bin/bash -le
              echo "Project NAME:  ${currentBuild.projectName} "
              echo "IS GERRIT: ${IS_GERRIT_BUILD} "
              echo "GIT TAG:   ${GIT_TAG} "
              echo "IS FULL: ${IS_FULL} "
              echo "SANITIZE:  ${SANITIZE} "

              git tag -l '''

				echo "Testing now"
 				sh '''#!/bin/bash
                 			echo "hello world"
					./robot-runner.sh
			    '''
				script {
	        if (env.SANITIZE == 'false') {
						echo  'SANITIZE is false'
					}
					else {
						echo  'SANITIZE is true'
					}
					echo  "${currentBuild.projectName}"
				}
			}
		 post {
			     always {
						     sh 'git tag --delete $(git tag -l)'
								 robot 'results'
			     }
		 }
	 }
	}
}

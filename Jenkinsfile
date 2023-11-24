@Library('piper-lib-os') _
properties([pipelineTriggers([githubPush()])])
pipeline {
    agent none
    options { disableConcurrentBuilds() }
    stages {
        stage('prepare') {
		agent { label 'hana-jenkins-slave-prod' }
		steps {
			setupCommonPipelineEnvironment script:this
            }
        }
        stage('build') {
		agent { label 'hana-jenkins-slave-prod'}
		when {
               anyOf { branch 'develop';branch pattern: "release-.+", comparator: "REGEXP" ;branch 'hotfix' ;branch 'trsdeploy'}
            }
		steps {
			echo 'mtaBuild'
			mtaBuild script: this
		}
        }
	stage('xsDeploy') {
		agent { label 'hana-jenkins-slave-prod' }
		when {
                branch 'develop'
            }
		steps {	
			echo "Deployment on XS Advanced of space DEV"
			xsDeploy (
			    script: this,
			    apiUrl: 'https://api.dhlhvie0.eu.airbus.corp:36633',
			    deployOpts: '-f',
			    loginOpts: '--skip-ssl-validation',
                org: 'airbus',
                space: 'DEV'
                )
		}
	}
		stage('xsDeploytrs') {
		agent { label 'hana-jenkins-slave-prod' }
		when {
                branch 'trsdeploy'
            }
		steps {	
			echo "Deployment on XS Advanced of space TRS"
			xsDeploy (
			    script: this,
			    apiUrl: 'https://api.phlhdbe0.eu.airbus.corp:36033',
			    deployOpts: '-e trsextention.mtaext -f',
			    loginOpts: '--skip-ssl-validation',
                org: 'airbus',
                space: 'TRS'
                )
		}
	}
	stage('uploadToTransportRequest') {
		agent { label 'hana-jenkins-slave-prod'}
		when {
               anyOf { branch 'develop';branch pattern: "release-.+", comparator: "REGEXP" ;branch 'hotfix'}
            }
		steps {	
			echo 'transportRequestUploadFile'
        		transportRequestUploadFile script: this
        		
		}
    	}
    }
}

pipeline {
    agent none
    stages {
	stage("Commit") {
	    matrix {
		agent {
		    docker {
			image "cart.lge.com/swte/yocto:16.04"
		    }
		}
		axes {
		    axis {
			name "MACHINE"
                        values "qemuarm64", "qemuarm", "qemux86-64", "qemux86", "raspberrypi2"
		    }
		}
		stages {
		    stage("Test") {
			environment {
			    MACHINE = "${MACHINE}"
			}
			steps {
			    updateGitlabCommitStatus name: "jenkins", state: "running"
			    sh "git submodule update --init"
			    sh """
                            TEMPLATECONF=`pwd`/build-templates . poky/oe-init-build-env
                            bitbake-layers add-layer ../meta-sample-test/
                            bitbake core-image-minimal -c coverageall
                            """
			}
		    }
		}
	    }
	}
    }  // stages
    post {
    	success {
            updateGitlabCommitStatus name: "jenkins", state: "success"
        }
        failure {
            updateGitlabCommitStatus name: "jenkins", state: "failed"
        }
    }  // post
}  // pipeline

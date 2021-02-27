pipeline {
    agent {
	docker {
	    image "cart.lge.com/swte/yocto:16.04"
	}
    }
    stages {
	stage("Setup") {
	    steps {
		updateGitlabCommitStatus name: "jenkins", state: "running"
		sh "git clean -fdx"
		sh "git submodule update --init"
	    }
	}
	stage("Test") {
	    steps {
		sh """
                TEMPLATECONF=`pwd`/build-templates . poky/oe-init-build-env
                bitbake-layers add-layer ../meta-sample-test/
                bitbake core-image-minimal
                bitbake core-image-minimal -c coverageall
                """
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
	aborted {
	    updateGitlabCommitStatus name: "jenkins", state: "canceled"
	}
    }  // post
}  // pipeline

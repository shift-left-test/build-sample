pipeline {
    agent {
	docker {
	    image "cart.lge.com/swte/yocto:16.04"
	}
    }
    stages {
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
}  // pipeline

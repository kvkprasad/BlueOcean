node('master') {

//  def deploy = env.Environment
   stage('Code Checkout') { // for display purposes
      // Get some code from a GitHub repository
      git branch: 'blueocean', url: 'https://github.com/rsravanam/BlueOcean.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      // mvnHome = tool 'M3'
   }
   
   stage('Build') {
	    parallel (
	        "Clean": {
	        	dir('maven-hello-world-master-release') {
	        	    // Run the maven build
	        		if (isUnix()) {
	        		sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean"
	        		} else {
	        		// bat(/"D:\Maven_339\apache-maven-3.3.9\bin\mvn" -Dmaven.test.failure.ignore clean/)
	        		echo "check out done"
	        		}
	        	}	
	        },
	    	
	    	"Install": {
	        	dir('maven-hello-world-master-release') {
	        	    // Run the maven build
	        		if (isUnix()) {
	        		sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore install"
	        		} else {
	        		// bat(/"D:\Maven_339\apache-maven-3.3.9\bin\mvn" -Dmaven.test.failure.ignore install/)
	        		echo "check out done"
	        		}
	        	}	
	        },
        
	    	"Compile": {
	        	dir('maven-hello-world-master-release') {
	        	    // Run the maven build
	        		if (isUnix()) {
	        		sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore compile"
	        		} else {
	        		// bat(/"D:\Maven_339\apache-maven-3.3.9\bin\mvn" -Dmaven.test.failure.ignore compile/)
	        		echo "check out done"
	        		}
	        	}	
	        },	
	    )
   }
   
   stage('Test') {
   
		dir('maven-hello-world-master-release') {
		    // Run the maven build
			if (isUnix()) {
				sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore test"
			} else {
				bat(/"D:\Maven_339\apache-maven-3.3.9\bin\mvn" -Dmaven.test.failure.ignore test/)
			}
		}
   } 
   
   stage('Test Results') {
   
		dir('maven-hello-world-master-release') {		    
			junit '**/target/surefire-reports/TEST-*.xml'
			archive 'target/*.jar'
		}
	}
	
    stage('Prepare Artifacts') {
   
		dir('maven-hello-world-master-release') {
		    // Run the maven build
			if (isUnix()) {
				sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
			} else {
				bat(/"D:\Maven_339\apache-maven-3.3.9\bin\mvn" -Dmaven.test.failure.ignore package/)
			}
		}
   }     
}
node {
//  def deploy = env.Environment
   stage('Code Checkout') { // for display purposes
      // Get some code from a GitHub repository
      git branch: 'demo', url: 'git@github.com:rsravanam/jenkinsipeline.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      // mvnHome = tool 'M3'
   }
   stage('Build') {
   
		dir('maven-hello-world-master-snapshot') {
		    // Run the maven build
			if (isUnix()) {
			sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean install compile"
			} else {
			// bat(/"D:\Maven_339\apache-maven-3.3.9\bin\mvn" -Dmaven.test.failure.ignore clean install compile/)
			echo "check out done"
			}
		}
   }
   stage('Test') {
   
		dir('maven-hello-world-master-snapshot') {
		    // Run the maven build
			if (isUnix()) {
				sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore compile test"
			} else {
				bat(/"D:\Maven_339\apache-maven-3.3.9\bin\mvn" -Dmaven.test.failure.ignore compile test/)
			}
		}
   }  
   stage('Results') {
   
		dir('maven-hello-world-master-snapshot') {		    
			junit '**/target/surefire-reports/TEST-*.xml'
			archive 'target/*.jar'
		}
	}
    stage('Artifacts') {
   
		dir('maven-hello-world-master-snapshot') {
		    // Run the maven build
			if (isUnix()) {
				sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
			} else {
				bat(/"D:\Maven_339\apache-maven-3.3.9\bin\mvn" -Dmaven.test.failure.ignore package/)
			}
		}
   }     
}
node ("master") {    
   
env.BN = VersionNumber([
        versionNumberString : '${BUILD_MONTH}.${BUILDS_TODAY}.${BUILD_NUMBER}', 
        projectStartDate : '2017-02-09', 
        versionPrefix : 'v1.'
    ])

	stage('Provision'){		
		echo 'Pipeline Started'
		
		echo 'Checkout dev branch'
		git branch: 'developer', credentialsId: 'JenkinsGit', url: 'git@github.com:ionitadaniel19/SpringMVCDemo.git'
		
		echo 'Change the project version ...'
        def W_M2_HOME = tool 'MVN3.3.9'
        bat "${W_M2_HOME}/bin/mvn versions:set -DnewVersion=$BN -DgenerateBackupPoms=false" 
		
		echo "Create a new branch with name release_${BN} ..."
        def W_GIT_HOME = tool 'Git'
        bat "${W_GIT_HOME} checkout -b release_${BN}"
		
		echo 'Stash the project source code ...'
        stash includes: '**', excludes: '**/TestPlan.jmx', name: 'SOURCE_CODE'
		
  }
}

node ("TestMachine") {
        env.M2_HOME = '/usr/share/maven'
        env.JAVA_HOME = '/usr'	 
        
        stage('Run-ut') {   
                echo 'Unstash the project source code ...'
                unstash 'SOURCE_CODE'	                                                       
                                
                echo 'Run the unit tests (and Jacoco) ...'
                sh "'${M2_HOME}/bin/mvn' clean test"   
		}
}





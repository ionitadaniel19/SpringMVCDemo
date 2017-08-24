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
        sh "${W_M2_HOME}/bin/mvn versions:set -DnewVersion=$BN -DgenerateBackupPoms=false" 
		
		echo "Create a new branch with name release_${BN} ..."
        def W_GIT_HOME = tool 'Git'
        sh "${W_GIT_HOME} checkout -b release_${BN}"
		
		echo 'Stash the project source code ...'
        stash includes: '**', excludes: '**/TestPlan.jmx', name: 'SOURCE_CODE'
		
  }
}


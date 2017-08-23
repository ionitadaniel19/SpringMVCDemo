node ("master") {    
   
env.BN = VersionNumber([
        versionNumberString : '${BUILD_MONTH}.${BUILDS_TODAY}.${BUILD_NUMBER}', 
        projectStartDate : '2017-02-09', 
        versionPrefix : 'v1.'
    ])

	stage('Provision'){		
		echo 'Pipeline Started'
		
		echo 'Checkout dev branch'
		git branch: 'developer', credentialsId: 'github', url: 'git@github.com:ionitadaniel19/SpringMVCDemo.git'
		
		echo 'Change the project version ...'
        def W_M2_HOME = tool 'Maven3.3.9'
        bat "${W_M2_HOME}\\bin\\mvn versions:set -DnewVersion=$BN -DgenerateBackupPoms=false" 
  }
}


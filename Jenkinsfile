pipeline{

agent any
stages {
    stage('Jenkins Pipeline Jenkins file'){
	    steps {
	    	echo 'Iniatilization'
	    //	git branch: 'main', credentialsId: 'a1b19d49-e9d9-480d-b182-081c80f53fd8', url: 'https://github.com/chetandg123/API_Pipeline' 
	    }
    }
    stage('Test'){
    	steps{
    		dir('/var/lib/jenkins/workspace/Pipe_JenkinsFile'){
		sh 'docker run -t --rm -v "$(pwd)":/tmp/project katalonstudio/katalon katalonc.sh -projectPath=/tmp/project -retry=0 -testSuitePath="Test Suites/SmokeTest" -browserType="Web Service" -executionProfile="default" -apiKey="fb7016b2-47ee-4d22-9e60-85b5b47f7d6b" --config -proxy.auth.option=NO_PROXY -proxy.system.option=NO_PROXY -proxy.system.applyToDesiredCapabilities=true -webui.autoUpdateDrivers=false'	
    		}
    	}
    }
}
post {

  always{
  	archiveArtifacts artifacts: 'Reports/**/*.*',fingerprint: true
  	junit 'Reports/*/SmokeTest/*/*.xml'
  }
}
}

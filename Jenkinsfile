pipeline {
    agent any
    stages {
        stage('Load Jenkinsfile from git repo') {
            steps {
                echo 'Loaded Jenkinsfile pipeline script to Jenkins'
            }
        }
        stage('Test') {
            steps {
                dir('/var/lib/jenkins/workspace/Pipe_JenkinsFile') {
                    // Run first test suite
                    sh 'docker run -t --rm -v "$(pwd)":/tmp/project katalonstudio/katalon katalonc.sh -projectPath=/tmp/project -retry=0 -testSuitePath="Test Suites/SmokeTest" -browserType="Web Service" -executionProfile="default" -apiKey="fb7016b2-47ee-4d22-9e60-85b5b47f7d6b" --config -proxy.auth.option=NO_PROXY -proxy.system.option=NO_PROXY -proxy.system.applyToDesiredCapabilities=true -webui.autoUpdateDrivers=false'

                    // Run second test suite
                    sh 'docker run -t --rm -v "$(pwd)":/tmp/project katalonstudio/katalon katalonc.sh -projectPath=/tmp/project -retry=0 -testSuitePath="Test Suites/SecondTestSuite" -browserType="Web Service" -executionProfile="default" -apiKey="fb7016b2-47ee-4d22-9e60-85b5b47f7d6b" --config -proxy.auth.option=NO_PROXY -proxy.system.option=NO_PROXY -proxy.system.applyToDesiredCapabilities=true -webui.autoUpdateDrivers=false'
                }
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'Reports/**/*.*', fingerprint: true
            junit 'Reports/*/SmokeTest/*/*.xml'
        }
    }
}


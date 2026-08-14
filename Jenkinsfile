pipeline {
    agent any
    stages {
        stage('Publishing Static Analysis Results') {
            steps {
                recordIssues (
                    tools: [
                        parasoftFindings (
                            pattern: 'reports/MISRA.xml',
                            localSettingsPath: 'settings.properties'
                        )
                    ]
                )
            }
        }

	stage('Publishing Test Execution Results') {
            steps {
                xunit (
                    tools: [[$class: 'ParasoftType', pattern: 'reports/report.xml']]   
                )
            }
        }

	stage('Attaching HTML Report') {
			steps {
				publishHTML (target : [allowMissing: false,
 				alwaysLinkToLastBuild: true,
 				keepAll: true,
 				reportDir: 'reports',
 				reportFiles: 'report5932398513366191311.html',
 				reportName: 'Parsoft Coverage Report HTML',
 				reportTitles: 'Parasoft Coverage Report'])
			}
	}

        stage('Publishing Code Coverage Results') {
            steps {
                recordParasoftCoverage (
                    pattern: 'reports/cvg_08-14-26_09-38-47',
                    referenceJob: 'CT',
                    sourceCodeEncoding: 'UTF-8',
                    coverageQualityGates: [
                        [
                            criticality: 'NOTE',
                            threshold: 60.0,
                            type: 'PROJECT'
                        ]
                    ]
                )
            }
        }
    }
}

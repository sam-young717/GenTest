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
                    tools: [[$class: 'ParasoftType', pattern: '\reports\report.xml']]   
                )
            }
        }

        stage('Publishing Code Coverage Results') {
            steps {
                recordParasoftCoverage (
                    pattern: '/reports/report.xml',
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

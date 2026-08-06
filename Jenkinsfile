pipeline {
    agent any
    stages {
        stage('Publishing Static Analysis Results') {
            steps {
                recordIssues (
                    tools: [
                        parasoftFindings (
                            pattern: 'reports/report.xml',
                            localSettingsPath: 'settings.properties'
                        )
                    ]
                )
            }
        }

	stage('Publishing Test Execution Results') {
            steps {
                xunit (
                    tools: [[$class: 'ParasoftType', pattern: '**/report.xml']]   
                )
            }
        }

        stage('Publishing Code Coverage Results') {
            steps {
                recordParasoftCoverage (
                    pattern: 'reports/coverage.xml',
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
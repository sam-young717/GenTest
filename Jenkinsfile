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
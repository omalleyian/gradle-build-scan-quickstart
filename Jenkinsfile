pipeline {
    agent { label 'gradle-latest' }

    stages {
        stage('Gradle Check') {
            steps {
                sh('gradle --version')
            }
        }

        stage('Dependency Check') {
            steps {
                sh('gradle useLatestVersions && gradle useLatestVersionsCheck')
            }
        }
    }
}

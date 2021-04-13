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
                sh('gradle dependencyUpdates')
                script {
                    def dependencyReport = readJSON(file: 'build/dependencyUpdates/report.json')
                    def updateCount = dependencyReport.outdated.count
                    if (updateCount != 0) {
                        String updateOutput = sh(script: 'gradle useLatestVersions && gradle useLatestVersionsCheck', returnStdout: true)

                        String branchUUID = UUID.randomUUID().toString()
                        println branchUUID
                        String branchName = 'update_dependencies'
                        sh("git branch -b $branchName && \
                            git add build.gradle && \
                            git commit -m 'Update $updateCount Dependencies' -m '$updateOutput' && \
                            git push -f")
                    }
                }
            }
        }
    }
}

pipeline {
  agent any
  
  stages {
    stage("Gradle Check") {
      steps {
        script {
          println "test"
        }
        sh("gradle --version")
      }
    }
  }
}

pipeline {

  agent any

  stages {
    stage('Local unit test') {
      steps {
        // sh 'docker build -t androidsdk -f cicd/androidsdk/Dockerfile cicd/androidsdk'
        // sh 'docker inspect -f . androidsdk'
        sh './gradlew test'
      }
    }
    stage('Build') {
      steps {
        // sh 'docker build -t androidsdk -f cicd/androidsdk/Dockerfile cicd/androidsdk'
        // sh 'docker inspect -f . androidsdk'
        sh './gradlew assembleDebug'
        sh 'ls -R app/build/outputs/apk'
        stash name: "apk", includes: 'app/build/outputs/apk/debug/*.apk', allowEmpty: true
        archiveArtifacts artifacts: 'app/build/outputs/apk/debug/*.apk', fingerprint: true
      }
    }
  }
}

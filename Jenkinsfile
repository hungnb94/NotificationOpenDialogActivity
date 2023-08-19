pipeline {

  agent any

  stages {
    stage('Local unit test') {
      agent {
        dockerfile {
          dir 'cicd/androidsdk'
          args '--network bridge'
          reuseNode true
        }
      }
      steps {
          sh './gradlew test'
      }
    }
    stage('Build') {
      agent {
        dockerfile {
          dir 'cicd/androidsdk'
          args '--network bridge'
          reuseNode true
        }
      }
      steps {
          sh './gradlew assembleDebug'
          sh 'ls -R app/build/outputs/apk'
          stash name: "apk", includes: 'app/build/outputs/apk/debug/*.apk', allowEmpty: true
          archiveArtifacts artifacts: 'app/build/outputs/apk/debug/*.apk', fingerprint: true
      }
    }
  }
}

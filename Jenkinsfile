pipeline {
  agent any
  stages {
    stage('MobSF-Scan') {
      steps {
        sh 'NO_COLOR=1 mobsfscan MASTG-Hacking-Playground/iOS/MSTG-JWT/'
      }
    }
  }
}

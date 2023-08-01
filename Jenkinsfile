pipeline {
  agent any
  options {
        ansiColor('xterm')
  }
  stages {
    stage('MobSF-Scan') {
      steps {
        sh 'mobsfscan MASTG-Hacking-Playground/iOS/MSTG-JWT/'
      }
    }
  }
}

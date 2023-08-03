pipeline {
  agent any
  options {
        ansiColor('xterm')
  }
  stages {
    stage('MobSF-Scan') {
      steps {
        sh 'mobsfscan iOS/MSTG-JWT/ --json -o mobscan.json'
      }
    }
  }
}

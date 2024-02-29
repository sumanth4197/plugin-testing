pipeline {
  agent {label 'worker1'}
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  stages {
    stage('Lint') {
      steps {
        sh 'python3 -m flake8 --format=pylint --statistics --show-source --count data_ingest_core --config .flake8 2>&1 | tee pylint.log'
      }
    }
  }
  post {
    always {
        recordIssues tools: [flake8(pattern: "**/pylint.log", reportEncoding:"UTF-8", skipSymbolicLinks:"true")]
    }
  }
}

//node('jenkins-slave-CI') {
node {
  stage('Checkout') {
    checkout scm
  }

  stage('Build') {
    echo 'building app, not really.'
  }

  stage('Integration test' {
    try {
      sh 'docker-compose up -d'
      sleep 10
      //mail subject: 'all well', to: 'me@example.com', body: 'All well.'
    } catch (e) {
      def w = new StringWriter()
      e.printStackTrace(new PrintWriter(w))
      //mail subject: "failed with ${e.message}", to: 'me@example.com', body: "Failed: ${w}"
      throw e
      } finally {
      sh 'docker-compose stop'
      sh 'docker-compose rm -f'
    }
  }

  stage('Upload to repository') {
    echo 'upload done'
  }
}

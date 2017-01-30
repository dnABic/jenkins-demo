//node('jenkins-slave-CI') {
//
//
node {
  stage('Checkout') {
    //properties([pipelineTriggers([[$class: 'GitHubPushTrigger']])]) 
    properties([pipelineTriggers([[$class: 'GitHubPushTrigger'], pollSCM('H/15 * * * *')])])
    checkout scm
  }

  stage('Build and Test image test-app:test') {
    //docker.withRegistry('https://141047255820.dkr.ecr.us-east-1.amazonaws.com:443') {
      def newImg = docker.build ("test-app:test",".")
      docker.image("test-app:test").inside('-u 0:0') {
        //sh 'ls -la /opt/; ps auxw; ls -la /ebs/; ls -la /ebs/data/'
        //sh '. /opt/venv/bin/activate && cd /opt/app/ && pylint -f parseable -d I0011,R0801 modules | tee pylint.out'
        //sh '. /opt/venv/bin/activate && cd /opt/app/ && nosetests -vi test_app.py'
        //sh '. /opt/venv/bin/activate && cd /opt/app/ && nosetests --with-xunit --traverse-namespace --with-coverage --cover-package=modules --cover-inclusive tests/'
        //sh '. /opt/venv/bin/activate && cd /opt/app/ && python -m coverage xml --include=modules*'
        //sh 'cd /opt/app/ && cp coverage.xml /ebs/jenkins/workspace/event-log/'
        sh 'ls -la'
        sh 'ps -a'
      }
    //}
    //step([$class: 'JUnitResultArchiver', allowEmptyResults: false, testResults: '**/coverage.xml'])
  }

  stage('Integration test') {
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
    echo 'Image pushed to repo'
    //newImg.push 'production1'
  }
}

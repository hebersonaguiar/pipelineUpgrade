node('slave') {
    stage('Container Runing') {
        checkout scm
        sh "docker-compose -f /srv/compose/docker-compose-jboss.yml ps > /tmp/ContainersRun"
        sh "cat /tmp/ContainersRun" 
        sh "rm -rf /tmp/ContainersRun"
    }
}

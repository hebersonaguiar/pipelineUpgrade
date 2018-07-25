node('slave') {
    stage('Container Runing') {
        checkout scm
        sh "docker-compose -f /srv/compose/docker-compose-jboss.yml ps > /tmp/ContainersRun"
        sh "cat /tmp/ContainersRun" 
        sh "rm -rf /tmp/ContainersRun"
    }
}

node('slave') {
    stage('Container Runing') {
        sh "git clone https://github.com/hebersonaguiar/composes.git /srv/composesGit"
        sh "cat /srv/composesGit/docker-compose-jboss.yml"
        sh "rm -rf /srv/composesGit" 
    }
}

node('slave') {
    stage('Container Runing') {
        checkout scm
        sh "docker-compose -f /srv/compose/docker-compose-jboss.yml ps > /tmp/ContainersRun"
        sh "cat /tmp/ContainersRun" 
        sh "rm -rf /tmp/ContainersRun"
    }
}

node('slave') {
    stage('Editing Compose Jboss') {
        sh "rm -rf /tmp/tagJboss"
        sh "rm -rf /srv/composesGit"
        sh "git clone https://github.com/hebersonaguiar/composes.git /srv/composesGit"
        sh "cat /srv/composesGit/docker-compose-jboss.yml | grep image | awk -F: '{print \$3}' > /tmp/tagJboss"
        sh "sed -e 's/`cat /tmp/tagJboss`/8.2.3.Final/g' /srv/composesGit/docker-compose-jboss.yml" 
        sh "cat /srv/composesGit/docker-compose-jboss.yml"
        sh "rm -rf /tmp/tagJboss"
        sh "rm -rf /srv/composesGit"
    }
}

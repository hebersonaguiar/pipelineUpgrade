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
        sh "sed -i 's/'\$(cat /tmp/tagJboss)'/${params.Tag}/g' /srv/composesGit/docker-compose-jboss.yml" 
        sh "cat /srv/composesGit/docker-compose-jboss.yml"
    }
}

node('slave') {
    stage('Update Container') {
        input 'Deseja continuar com a ação?'

        sh "docker-compose -f /srv/composesGit/docker-compose-jboss.yml up --build --no-deps -d Jboss > /tmp/logUpdate"
        sh "cat /tmp/logUpdate"
        sh "rm -rf /tmp/tagJboss"
        sh "rm -rf /tmp/logUpdate"
        sh "rm -rf /srv/composesGit" 
    }
}

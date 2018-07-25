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
        sh "cp -R /srv/compose/ /srv/composeBKP"
        sh "cat /srv/compose/docker-compose-jboss.yml | grep image | awk -F: '{print \$3}' > /tmp/tagJboss"
        sh "sed -i 's/'\$(cat /tmp/tagJboss)'/${params.Tag}/g' /srv/compose/docker-compose-jboss.yml" 
        sh "cat /srv/compose/docker-compose-jboss.yml"
        sh "rm -rf /srv/composeBKP"
    }
}

node('slave') {
    stage('Update Container') {
        input 'Deseja continuar com a ação?'

        sh "docker-compose -f /srv/compose/docker-compose-jboss.yml up --build --no-deps -d Jboss"
        sh "rm -rf /tmp/tagJboss"
    }
}

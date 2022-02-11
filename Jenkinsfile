node{
    stage('Deploiement') {
        checkout scm
    }
      stage('Injection SSH') {
        sh 'echo "127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4" > /etc/hosts'
        sh 'echo "::1         localhost localhost.localdomain localhost6 localhost6.localdomain6" >> /etc/hosts'
        sh 'echo "172.16.171.132 app-salaire.adrien.form" >> /etc/hosts'
        sh 'apk add sshpass'
        sh 'rm -fr /root/.ssh/*'
        sh 'ssh-keygen -q -t rsa -N \'\' -f "/root/.ssh/id_rsa"'
        sh 'sshpass -p \'Poseidon\' ssh-copy-id  -o stricthostkeychecking=no "root@app-salaire.adrien.form"'
    }
    stage('Ansible') {
      ansiblePlaybook (
          colorized: true,          
          playbook: 'playbook.yml',
          inventory: 'hosts.yml'
      )
    }
}

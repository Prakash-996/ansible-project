pipeline {
    agent any

    environment {
        INVENTORY = 'inventory'
        PLAYBOOK = 'Projectnginx.yaml'
        PEM_FILE = "${WORKSPACE}/devops.pem"
        USER = 'ec2-user'
    }

    stages {
        stage('Setup SSH Known Hosts') {
            steps {
                sh '''
                    mkdir -p ~/.ssh
                    chmod 700 ~/.ssh
                    grep -v '^#' ${INVENTORY} | grep -E '^[0-9]' | awk '{print $1}' | while read ip; do
                        ssh-keyscan -H $ip >> ~/.ssh/known_hosts
                    done
                    chmod 644 ~/.ssh/known_hosts
                '''
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh """
                    ansible-playbook ${PLAYBOOK} -i ${INVENTORY} \
                    --private-key ${PEM_FILE} -u ${USER}
                """
            }
        }
    }
}

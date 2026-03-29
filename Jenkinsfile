pipeline {
    agent any

    environment {
        ANSIBLE_USER = "ec2-user"
    }

    stages {

        stage('Setup SSH') {
            steps {
                sshagent(['ec2-key']) {  // uses the credential
                    sh """
                        mkdir -p ~/.ssh
                        chmod 700 ~/.ssh
                        for ip in \$(grep -E '^[0-9]' inventory | awk '{print \$1}'); do
                            ssh-keyscan -H \$ip >> ~/.ssh/known_hosts
                        done
                        chmod 644 ~/.ssh/known_hosts
                    """
                }
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sshagent(['ec2-key']) {
                    sh "ansible-playbook Projectnginx.yaml -i inventory -u \$ANSIBLE_USER"
                }
            }
        }
    }

    post {
        success { echo "✅ Pipeline completed successfully!" }
        failure { echo "❌ Pipeline failed. Check the errors above." }
    }
}

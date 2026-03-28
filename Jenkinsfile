pipeline {
    agent any

    environment {
        ANSIBLE_PRIVATE_KEY = "${WORKSPACE}/devops.pem"
    }

    stages {

        stage('Setup SSH Known Hosts') {
            steps {
                // Create .ssh directory in Jenkins workspace
                sh """
                    mkdir -p ~/.ssh
                    chmod 700 ~/.ssh
                    # Add all IPs from inventory to known_hosts
                    for ip in \$(grep -E '^[0-9]' inventory); do
                        ssh-keyscan -H \$ip >> ~/.ssh/known_hosts
                    done
                    chmod 644 ~/.ssh/known_hosts
                """
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh """
                    # Make sure PEM file has correct permissions
                    chmod 400 ${ANSIBLE_PRIVATE_KEY}
                    # Run your Ansible playbook
                    ansible-playbook Projectnginx.yaml -i inventory \
                        --private-key ${ANSIBLE_PRIVATE_KEY} -u ec2-user
                """
            }
        }
    }

    post {
        success {
            echo "🎉 Ansible playbook executed successfully!"
        }
        failure {
            echo "❌ Pipeline failed. Check the errors above."
        }
    }
}

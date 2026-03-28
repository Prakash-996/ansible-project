pipeline{
    agent any

        stages{
            stage("run the ansible"){
                steps {
                sh 'ansible-playbook Projectnginx.yaml -i inventory'
            }
            }
        }
    }

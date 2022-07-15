pipeline {
    agent any

    stages {
        stage('Check Configuration') {
            steps {
                ansiblePlaybook credentialsId: 'vagrant-ssh-key',
                        inventory: 'inventory',
                        playbook: 'check-nginx-configuration.yml',
                        vaultCredentialsId: 'vault-password-file'
            }
        }
    }
}

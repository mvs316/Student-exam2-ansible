node("my_agent") {
    stage('Clone repository') {
        checkout scm
    }

    stage('Execute ansible playbook for deployment') {
        ansiblePlaybook credentialsId: 'private-key-ansible', installation: 'ansible', inventory: 'myhosts.ini', playbook: 'start_roles.yml', vaultCredentialsId: 'vault-password'
    }

    
    stage('Testing') {
        def response = httpRequest "http://192.168.56.106"
        println('Status: '+response.status)
        println('Response: '+response.content)
    }
}


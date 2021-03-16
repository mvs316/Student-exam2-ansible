node("my_agent") {
    stage('Clone repository') {
        checkout scm
    }

    stage('Execute ansible playbook for deployment') {
        ansiblePlaybook credentialsId: becomeUser: 'exam', 'private-key-ansible', installation: 'ansible', inventory: 'myhosts.ini', playbook: 'start_roles.yml', vaultCredentialsId: 'vault-password'
    }
    
    stage('Testing') {
        def response = httpRequest "http://localhost:5000" , validResponseCodes: '200'
        println('Status: '+response.status)
        println('Response: '+response.content)
    }
}


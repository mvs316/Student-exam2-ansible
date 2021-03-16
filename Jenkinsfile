node("my_agent") {
    stage('Clone repository') {
        checkout scm
    }

    stage('Execute ansible playbook for deployment') {
        ansiblePlaybook credentialsId: 'private-key-ansible', installation: 'ansible', inventory: 'myhosts.ini', playbook: 'start_roles.yml', vaultCredentialsId: 'ansible-vault'
    }
    
    stage('Testing') {
        def response = httpRequest "http://localhost:5000" , validResponseCodes: '200'
        println('Status: '+response.status)
        println('Response: '+response.content)
    }
}


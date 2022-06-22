pipeline {

        stages {
        stage('Scanning Image') {
            steps {
                // This will always be executed in the JNLP container
                sh "echo grocamador/web-dvwa:latest > sysdig_secure_images"
                sysdig engineCredentialsId: 'sysdig-secure-api-credentials', name: 'sysdig_secure_images', inlineScanning: true
            }
        }
     }
}

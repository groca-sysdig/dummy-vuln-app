pipeline {
 
    parameters { 
        string(name: 'DOCKER_REPOSITORY', defaultValue: 'grocamador/dummy-demo', description: 'Name of the image to be built (e.g.: sysdiglabs/dummy-vuln-app)') 
    }
    
    environment {
        DOCKER = credentials('docker-repository-credentials')
    }
    
    stages {
        stage('Checkout') {
            steps {
                container("dind") {
                    checkout scm
                }
            }
        }
        stage('Build Image') {
            when {
                branch 'master'
            }
            steps {
                container("dind") {
                    sh "docker build -f Dockerfile -t ${params.DOCKER_REPOSITORY} ."
                    sh "echo ${params.DOCKER_REPOSITORY} > sysdig_secure_images"
                }
            }
        }
        stage('Scanning Image') {
            steps {
                // This will always be executed in the JNLP container
                sysdig engineCredentialsId: 'sysdig-secure-api-credentials', name: 'sysdig_secure_images', inlineScanning: true
            }
        }
   }
}

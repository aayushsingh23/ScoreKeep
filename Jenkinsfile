pipeline {
    agent any
    
    environment {
        NODEJS_HOME = tool name: 'Node.js', type: 'hudson.plugins.nodejs.tools.NodeJSInstallation'
    }
    
    stages {
        stage('Install Node.js') {
            steps {
                script {
                    // Set PATH to include Node.js binaries
                    env.PATH = "${env.NODEJS_HOME}/bin:${env.PATH}"
                }
            }
        }
        
        stage('Build') {
            steps {
             echo "build hora"
            }
        }
        
        // Add more stages as needed
    }
}

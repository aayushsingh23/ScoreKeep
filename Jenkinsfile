//FOR WINDOWS IMAGE
pipeline {
    agent any
    
    tools {
        // Specify the correct Node.js installation name
        nodejs 'NodeJS-22.2.0'
    }

    triggers {
        cron('H * * * *') // Runs the pipeline every minute
    }
    
    stages {
        // stage('Install Node.js') {
        //     steps {
        //         script {
        //             // Define the Node.js version to install
        //             def nodejsVersion = '22.2.0'
                    
        //             // Check if Node.js is already installed
        //             def nodeHome = tool name: "NodeJS-${nodejsVersion}", type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
                    
        //             // If Node.js is not installed, install it
        //             if (nodeHome == null) {
        //                 // Install Node.js using the 'NodeJS' tool name
        //                 nodeHome = tool 'NodeJS'
        //             }
                    
        //             // Set the environment variable for NODE_HOME
        //             env.NODE_HOME = nodeHome

        //             bat 'node --version'
        //             bat 'npm --version'
        //         }
        //     }
        // }
        
        // stage('Create package.json') {
        //     steps {
        //         // Create package.json using npm init with default options
        //         bat 'npm init -y'
        //         // Verify package.json creation
        //         bat 'type package.json'
        //     }
        // }
        
        // stage('Add Dependencies') {
        //     steps {
        //         // Install express as a dependency
        //         bat 'npm install express'
        //         // Verify the dependencies
        //         bat 'type package.json'
        //     }
        // }
        
        // stage('Kill Server') {
        //     steps {
        //         script {
        //             // Define the port to check
        //             def port = 3000
        
        //             // Find the PID of the process listening on the specified port
        //             def netstatResult = bat(script: "netstat -ano | findstr :${port}", returnStdout: true).trim()
                    
        //             if (netstatResult) {
        //                 // Extract PID from netstat result
        //                 def pid = netstatResult.split()[-1]
                        
        //                 // Kill the process using the extracted PID
        //                 bat "taskkill /PID ${pid} /F"
        //                 echo "Server process running on port ${port} with PID ${pid} has been killed."
        //             } else {
        //                 echo "No server process is listening on port ${port}."
        //             }
        //         }
        //     }
        // }
        stage('Kill Server') {
            when {
                expression {
                    // Check if a process is listening on port 3000
                    def netstatResult = bat(script: "netstat -ano | findstr :3000", returnStdout: true).trim()
                    return netstatResult ? true : false
                }
            }
            steps {
                script {
                    // If the condition is met, kill the process
                    def port = 3000
                    def netstatResult = bat(script: "netstat -ano | findstr :${port}", returnStdout: true).trim()
                    
                    if (netstatResult) {
                        def pid = netstatResult.split()[-1]
                        bat "taskkill /PID ${pid} /F"
                        echo "Server process running on port ${port} with PID ${pid} has been killed."
                    }
                }
            }
        }
        
        stage('Start Server') {
            steps {
                bat 'npm install express'
                bat 'node server.js'
            }
        }
        
        stage('Build') {
            steps {
                bat '${NODE_HOME}\\bin\\node --version'
                bat '${NODE_HOME}\\bin\\npm --version'
                // Add more build steps as needed
            }
        }
    }
}


//FOR LINUX BASED IMAGE
// pipeline {
//     agent any
    

//     // triggers{
//     //     cron('H * * * *')
//     // }
//     // triggers {
//     //     cron('H * * * *') // Runs the pipeline every minute
//     // }

//     tools {
//         // Specify the correct Node.js installation name
//         nodejs 'NodeJS-22.2.0'
//     }
    
//     stages {
//         stage('Install Node.js') {
//             steps {
//                 script {
//                     // Define the Node.js version to install
//                     def nodejsVersion = '22.2.0'
                    
//                     // Check if Node.js is already installed
//                     def nodeHome = tool name: "NodeJS-${nodejsVersion}", type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
                    
//                     // If Node.js is not installed, install it
//                     if (nodeHome == null) {
//                         // Install Node.js using the 'NodeJS' tool name
//                         nodeHome = tool 'NodeJS'
//                     }
                    
//                     // Set the environment variable for NODE_HOME
//                     env.NODE_HOME = nodeHome

//                     sh 'node --version'
//                     sh 'npm --version'
//                 }
//             }
//         }
//        stage('Create package.json') {
//             steps {
//                 // Create package.json using npm init with default options
//                 sh 'npm init -y'
//                 // Verify package.json creation
//                 sh 'cat package.json'
//             }
//         }
//         stage('Add Dependencies') {
//             steps {
//                 // Install express as a dependency
//                 sh 'npm install express'
//                 // Verify the dependencies
//                 sh 'cat package.json'
//             }
//         }
        
//         stage('Install lsof') {
//             steps {
//                 script {
//                     // Install lsof tool on Jenkins
//                     tool name: 'lsof', type: 'hudson.plugins.toolenv.ToolEnvBuildWrapper'
//                 }
//             }
//         }
        
//         stage('Kill Server') {
//             steps {
//                 script {
//                     // Find the process ID (PID) using ss
//                     def port = 3000 // Example port number
//                     def pid = sh(script: "ss -ltn | grep ':${port}' | awk '{print \$6}' | cut -d'=' -f2", returnStdout: true).trim()
                    
//                     if (pid) {
//                         // Kill the process
//                         sh "kill ${pid}"
//                         echo "Server process running on port ${port} has been killed."
//                     } else {
//                         echo "No server process is listening on port ${port}."
//                     }
//                 }
//             }
//         }
// stage('Start Server') {
//     steps {
//         // sh 'npm install express'
//         sh 'node server.js'
//     }
// }



//         stage('Build') {
//             steps {
//                  sh '${NODE_HOME}/bin/node --version'
//                 sh '${NODE_HOME}/bin/npm --version'
//                 // Add more build steps as needed
//             }
//         }
//     }
// }

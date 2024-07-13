// CreatedBy     : Harish Raj
// CreatedTime   : 15 Feb 2023
// ModifiedBy    : Harish Raj
// ModifiedTime  : 15 Feb 2023
// Description   : This file contains all the instruction for jenkins pipeline
 

pipeline {
    agent { label "dev" }
    stages {
        //        stage('CLONE CONFIG REPOSITORY') {
        //     steps {
        //         script{
        //             catchError {
        //                 sh "git clone --recurse-submodules ${CONFIG_REPO_URL} -b ${CONFIG_REPO_BRANCH}"
        //             }
        //         }
        //     }
        // }

        // stage('SETTING UP ALL THE CONFIGURATIONS') {
        //     steps {
        //         script {
        //                 def sourcePath = sh(script: 'pwd', returnStdout: true).trim()
        //                 def targetPath = sh(script: 'pwd', returnStdout: true).trim()
        //                 sh "rm -rf ${sourcePath}/package-lock.json"
        //                 sh "cp -r ${sourcePath}/${CONFIG_REPO_NAME}/${CONFIG_REPO_FOLDER}/package.json ${targetPath}"
        //                 sh "cp -r ${sourcePath}/${CONFIG_REPO_NAME}/${CONFIG_REPO_FOLDER}/post.deployment.email.sh ${targetPath}"
        //                 sh "cp -r ${sourcePath}/${CONFIG_REPO_NAME}/${CONFIG_REPO_FOLDER}/pre.deployment.email.sh ${targetPath}"
        //                 sh "cp -r ${sourcePath}/${CONFIG_REPO_NAME}/${CONFIG_REPO_FOLDER}/test.report.email.sh ${targetPath}"
        //                 sh "cp -r ${sourcePath}/${CONFIG_REPO_NAME}/${CONFIG_REPO_FOLDER}/Dockerfile ${targetPath}"
        //                 sh "cp -r ${sourcePath}/${CONFIG_REPO_NAME}/${CONFIG_REPO_FOLDER}/config.js ${targetPath}"
        //                 sh "rm -rf ${sourcePath}/${CONFIG_REPO_NAME}"
        //         }
        //     }
        // }

        //  stage('PRE-DEPLOYMENT EMAIL') {
        //     steps {
        //         script {
        //             sh 'chmod +x pre.deployment.email.sh'
        //              sh './pre.deployment.email.sh'
        //         }
        //     }
        // }

        stage('STOPPING THE CURRENTLY RUNNING CONTAINER') {
            steps {
                script{
                    catchError {
                        sh 'echo admin | sudo -S docker stop auth-container || true'
                    }
                }
            }
        }
        stage('DELETING THE STOPPED CONTAINER') {
            steps{
                script{
                    catchError {
                        sh 'echo admin | sudo -S docker rm auth-container || true'
                    }
                }
            }
        }
        stage('DELETING THE IMAGE OF THE CONTAINER') {
            steps{
                script{
                    catchError {
                        sh 'echo admin | sudo -S docker rm auth-image || true '
                    }
                }
            }
        }
       stage('BUILDING A NEW IMAGE FROM SOURCE CODE') {
            steps{
                script{
                    catchError{
                        sh 'echo admin | sudo -S docker build -t auth-image .' 
                    }
                 }
            }
            }
        stage('RUNNING A NEW CONATINER FROM NEW IMAGE') {
            steps{
                script{
                    catchError{
                        sh 'echo admin | sudo -S docker run -d -p 7001:7001 --name auth-container auth-image'
                    }
                }
            }
        }
        // stage('POST-DEPLOYMENT EMAIL') {
        //     steps{
        //         script{
        //            sh 'chmod +x post.deployment.email.sh'
        //              sh './post.deployment.email.sh'
        //         }
        //     }
        // }
    }
}

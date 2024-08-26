#!groovy
library "knime-pipeline@main"

properties([
    buildDiscarder(logRotator(numToKeepStr: '5')),
    disableConcurrentBuilds(),
])


try {
    node ('partner-agent'){
        stage('Checkout Sources') {
            checkout scm
        }
        stage('build python extension'){
            sh '''
                micromamba activate knime-ext-bundling
                micromamba list                
                build_python_extension.py --knime-version 5.3 pst updatesite
            '''
        }
    }
} catch (ex) {
    currentBuild.result = 'FAILURE'
    throw ex
}
/* vim: set shiftwidth=4 expandtab smarttab: */

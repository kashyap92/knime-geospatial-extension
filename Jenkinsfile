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
            // build_python_extension path\to\directoryof\myextension\ path\to\directoryof\output  
            knimetools.buildPythonExtension(updateSiteProject = '', knimeVersion = '5.3', ExtensionPath = 'knime_extension', OutputPath = 'updatesite')
        }
    }
} catch (ex) {
    currentBuild.result = 'FAILURE'
    throw ex
}
/* vim: set shiftwidth=4 expandtab smarttab: */

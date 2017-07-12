@Library('deployment') _

node('cmake') {
    stage('checkout') {
        step([$class: 'WsCleanup'])
        checkout scm
    }
    
    stage('prepare') {
        sh 'mkdir build'
    }
    
    stage('build') {
        sh 'cd build; cmake ..; make'
    }
    
    stage('install') {
        var shell = SecureShell(steps)
        //shell.scp('build/osm2pgsql', 'osm2pgsql')
        //shell.ssh([
         //   'sudo cp osm2pgsql /usr/local/bin'
        //]);
    }
    
    stage('clean-up') {
        step([$class: 'WsCleanup'])
    }
}
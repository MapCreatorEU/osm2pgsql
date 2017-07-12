@Library('deployment') _
import org.mapcreator.SecureShell

node('cmake') {
    stage('checkout') {
        step([$class: 'WsCleanup'])
        checkout scm
    }
    
    stage('prepare') {
        shell = new SecureShell(steps)
        shell.init('f206c873-8c0b-481e-9c72-1ecb97a5213a', '10.58.32.45', 'deploy', false)
        
        String basedir = "/home/deploy/osm2pgsql_${BUILD_NUMBER}/"
        shell.ssh([
            "mkdir ${basedir}"
        ])
        
        shell.scp('./', basedir)
                shell.ssh([
            "cd ${basedir}",
            "mkdir build",
            "cd build",
            "cmake ..",
            "make -j\$(nproc)",
            "sudo make install"
        ])
    }
    
    stage('clean-up') {
        step([$class: 'WsCleanup'])
    }
}

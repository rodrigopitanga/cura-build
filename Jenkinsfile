node ('linux && cura') {
    stage('Prepare') {
        step([$class: 'WsCleanup'])

        checkout scm
    }

    stage('Build') {
        sh 'cmake . -DCMAKE_PREFIX_PATH=/opt/ultimaker/cura-build-environment -DCMAKE_BUILD_TYPE=Release -DSIGN_PACKAGE=OFF -DBUILD_TESTING=ON'
        sh 'make'
    }

    stage('Package') {
        sh 'make package'
    }

    stage('Run Integration Tests') {
        sh 'make test'
    }

    stage('Archive') {
        archiveArtifacts '*.AppImage'
    }
}
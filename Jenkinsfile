pipeline {
    agent any

    options {
        timeout(time: 60, unit: 'MINUTES')
    }

    environment {
        TUANJIE = '/Applications/Tuanjie/Hub/Editor/2022.3.62t10/Tuanjie.app/Contents/MacOS/Tuanjie'
        BUILD_OUTPUT = 'Builds/Android/jenkinsTest.apk'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Android') {
            steps {
                sh '''
                    set -e
                    mkdir -p Builds/Android
                    "$TUANJIE" \
                        -batchmode \
                        -quit \
                        -projectPath "$WORKSPACE" \
                        -executeMethod BuildScript.BuildAndroid \
                        -buildOutput "$BUILD_OUTPUT" \
                        -logFile "$WORKSPACE/Builds/Android/tuanjie-build.log"
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'Builds/Android/**/*', allowEmptyArchive: true
        }
    }
}

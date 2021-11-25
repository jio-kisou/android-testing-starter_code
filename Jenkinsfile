pipeline {
    agent any

    stages {
        stage('tests') {
            steps {
                // sh 'git clone https://github.com/jio-kisou/android-testing-starter_code.git'
                // dir('android-testing-starter_code'){
                    sh '.\gradlew testDebugUnitTest'
                    sh '.\gradlew jacocoTestReport'
                // }
                // git branch: 'main', url: 'https://github.com/jio-kisou/android-testing-starter_code'
                // gradlew 'testDebugUnitTest'
            }
        }
    }

    post {
        always {
            junit allowEmptyResults: true, testResults:'build/test-results/**/*.xml'
            publishCoverage adapters: [jacocoAdapter('build/reports/jacoco/jacocotestReport/jacocotestReport.xml')]
            deleteDir()
        }
        success { // 成功した場合
            postBuildSlackSend("good", "SUCCESS")
        }
        failure { // 失敗した場合(どこかのステップでエラーを吐いた場合)
            postBuildSlackSend("danger", "FAILURE")
        }
        aborted { // 中断した場合
            postBuildSlackSend("warning", "ABORTED")
        }
    }
}

node {
    stage('Build') {
        docker.image('python:2-alpine').inside {
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }
    } // menggunakan docker image python:2-alpine2 untuk menjalankan python -m py py_compile

    stage('Test') {
        docker.image('qnib/pytest').inside {
            try {
                sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            } finally {
                junit 'test-reports/results.xml'
            }
        }
    } // menggunakan docker image qnib/pyest untuk pengujian py.test dan file hasil pengujian ditaruh di reports/results.xml

    /* stage('Deliver') {
        docker.image('cdrx/pyinstaller-linux:python2').inside {
            sh 'pyinstaller --onefile sources/add2vals.py'
        }
        archiveArtifacts 'dist/add2vals'
    } */
}

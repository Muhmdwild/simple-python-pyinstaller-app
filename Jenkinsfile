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

    stage('Manual Approval') {
        input message: 'Apakah Anda ingin melanjutkan ke tahap Deploy?', ok: 'Lanjutkan'
        echo 'Tahap Deploy dilanjutkan setelah persetujuan manual.'
    }

    stage('Deploy') {
    docker.image('python:2-alpine').inside {
        sh 'python sources/add2vals.py 5 10' // Contoh menjalankan dengan argumen 5 dan 10
        echo 'Aplikasi berjalan selama 1 menit...'
        sh 'sleep 60' // Menjeda eksekusi selama 1 menit
        echo 'Waktu habis, eksekusi pipeline selesai.'
        }
    }
}

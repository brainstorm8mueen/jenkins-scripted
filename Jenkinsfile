node {
    try {
        stage('checkout') {
            echo 'Checking out the code...'
            checkout scm
        }
        stage('show files') {
        echo 'Displaying the files...'

        if (isUnix()) {
            sh 'ls -l'
        } else {
            bat 'dir'
        }
    }
    stage('Install Dependencies') {
        echo 'Installing dependencies...'
        if (isUnix()) {
            sh 'python3 -m pip install -r requirements.txt'
        } else {
            bat 'python3 -m pip install -r requirements.txt'
        }
    }
    stage('Run Application') {
        echo 'Running the python application...'
        if (isUnix()) {
            sh 'python3 app.py'
            } else {
            bat 'python3 app.py'
        }
    }
    stage('Run Test') {
        echo 'Running the Automated Test...'
        if (isUnix()) {
            sh 'python3 -m pytest'
            } else {
            bat 'python3 -m pytest -v'
        }
    }

    stage('Build Result') {
        echo "Application build and testing completed successfully."
    }
}
catch (Exception e) {
    echo "An error occurred: ${e.getMessage()}"
    currentBuild.result = 'FAILURE'
}
finally {
    echo "Cleaning up workspace..."
    deleteDir()
}
}

pipeline {
    agent {
        dockerfile true
        // label 'proxmox'
        // docker { 
        //     image 'python' 
        //     label 'proxmox'
        // }
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/tymofiismyrnov/jenkins_test'
            }
        }
        stage('Installing dependencies') {
            steps {
                sh 'pip --version'
                sh 'pip install -r ./requirements.txt'
            }
        }
        stage('Execute'){
            steps {
                withCredentials([file(credentialsId: 'test-job-secret-file', variable: 'SECRET')]) {
                    sh 'ls -la'
                    sh "cat $SECRET"
                    sh 'ln -s -f $SECRET ./settings.py'
                    sh 'cat settings.py'
                    sh 'python main.py'
                }
            }
        }
    }
}

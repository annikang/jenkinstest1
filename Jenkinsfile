pipeline {
    agent {
        label "!master"
    }
    //options {
        //ansiColor('xterm')
    //}
    //从git获取代码
    stages {
        stage('Get source code'){
            steps{
                checkout scm
                sh 'git submodule init && git submodule update'
            }
        }
    //初始化环境，这里主要只是newman镜像
        stage('Init Environment'){
            steps{
                sh 'docker pull postman/newman:4.5-alpine'
            }
        }
    //运行接口测试了，即用docker来运行newman
        stage('build') {
            steps {
                sh 'docker run --rm -v \$(pwd):/etc/newman -t postman/newman:4.5-alpine run weather.json --insecure'
            }
        }
    }
}


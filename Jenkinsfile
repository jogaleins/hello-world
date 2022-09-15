pipeline {
  options {
    ansiColor('xterm')
  }
  agent any
  tools {
    maven "maven-3.8.6"
    jdk "openjdk-11"
  }
  stages{
    stage('Checkout SCM'){
        steps {
            git branch: 'master', url: 'https://github.com/jogaleins/hello-world.git'
        }
    }
    stage('Initialize'){
        steps {
            echo "PATH = ${M2_HOME}/bin:$PATH"
            echo "M2_HOME = ${M2_HOME}"
        }
    }
    stage('Build'){
        steps{
            sh 'mvn clean install'
        }
    }
    stage('Deploy'){
        steps{
                sshagent(credentials: ['jenkins-centos-sshkey']) {

                sh 'pwd'
                sh 'hostname'
                sh 'ssh centos@192.168.2.142 date'
                 
                }
        }
    }

    }
  }

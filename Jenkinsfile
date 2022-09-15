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
    stage('Publish and Deploy'){
        steps{
                sshagent(credentials: ['jenkins-centos-sshkey']) {

                sh 'pwd;hostname;whoami'
                sh 'ssh -o StrictHostKeyChecking=no -l centos 192.168.2.142 date'
                sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/RegappCICD/webapp/target/webapp.war centos@192.168.2.142:/opt/docker/'
                sh 'ssh -o StrictHostKeyChecking=no -l centos 192.168.2.142 ansible-playbook -i /opt/docker/ansible/inventory.ini /opt/docker/ansible/main.yaml'

                }
        }
    }

    }
  }

pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    doGenerateSubmoduleConfigurations: false, 
                    extensions: [[$class: 'CleanCheckout']], 
                    submoduleCfg: [], 
                    userRemoteConfigs: [[credentialsId: 'github-pass', url: 'https://github.com/domingo-ultratendency/zookeeper-cluster-ansible.git']]
                ])
            }
        }
        stage('Download Zookeeper source code') {
            steps {
                sh "wget https://dlcdn.apache.org/zookeeper/zookeeper-3.7.0/apache-zookeeper-3.7.0-bin.tar.gz"
            }
        }
        stage('Cluster Setup') {
            steps {
                sh "ansible-playbook -i inventory/development/cluster.ini clusterSetup.yml"
            }
        }
    }
}
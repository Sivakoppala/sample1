pipeline {
    agent {
        label 'Ansible-Master'
    }
    stages {
        stage('Checkout Dev branch') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'origin/dev']], userRemoteConfigs: [[url: 'https://github.com/Knowledgesprint-Technologies/FN-Dev.git']]])
            }
        }
        stage('Execute Dev Playbook') {
            when {
                changeset "documents/*.docx"
            }
            steps {
                sh 'echo A new file has been added........Running Dev Playbook'
            }
        }
        stage('Checkout QA branch') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'origin/qa']], userRemoteConfigs: [[url: 'https://github.com/Knowledgesprint-Technologies/FN-Dev.git']]])
            }
        }
        stage('Execute QA Playbook') {
            when {
                changeset "documents/*.docx"
            }
            steps {
                sh 'echo A new file has been added........Running QA Playbook'
                dir('/home/ansibleadm/FN-Dev/env-configs/qa/playbooks') {
                    sh 'ansible-playbook ansible-qa-deploy.yml'
                }
            }
        }
    }
}

//Getting maven goals as a input from user
pipeline {
    agent  {
        label 'jenkins'
    } 
    
    tools {
        maven 'Maven'
    }
    parameters {
        string(name: 'MAVEN_GOAL', defaultValue: 'clean install', description: 'Enter maven goal choice')
        string(name: 'MAVEN_DEPLOY_GOAL', defaultValue: 'clean deploy', description: 'Enter maven deploy goal choice')
    }
    stages {
        stage ('Checkout source') {
            steps {
               checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Hari-Ramesh/java-maven-war-appH.git']]) 
            }
        }
        // stage ('Get Maven Goal') {
        //     steps {
        //         script {
        //             env.MAVEN_GOAL = input(id: 'mavenGoal', message: 'Enter the Maven goal to execute:', parameters: [[$class: 'ChoiceParameterDefinition', choices: ['clean', 'install'], name: 'MAVEN_GOAL']])
        //         }
        //     }
        // }
        stage('Run Maven Build') {
            steps {
                    sh "mvn ${MAVEN_GOAL}"
                }
        }
        // stage ('Build') {
        //     steps {
        //        sh 'mvn clean install'
        //     }
        // }
        // stage ('sonar scanning') {
        //     steps {
        //        withSonarQubeEnv("Sonar") {
        //         sh "${tool("Sonar")}/bin/sonar-scanner \
        //         -Dsonar.host.url=http://ec2-18-141-24-107.ap-southeast-1.compute.amazonaws.com:9000/ \
        //         -Dsonar.login=sqp_047f03ee8671e99ebdac9e49e7cf1f74a6230ebe \
        //         -Dsonar.projectKey=java-maven-war-appH \
        //         -Dsonar.java.binaries=target "
        //         }
        //     }
        // }
        // stage ('upload into nexus') {
        //     steps {
        //        sh 'mvn -s settings.xml clean deploy'
        //     }
        // }
        // stage ('Enter Maven Goal') {
        //     steps {
        //         // sh 'mvn -s settings.xml' 
        //         script {
        //             sh 'mvn -s settings.xml'
        //             env.MAVEN_DEPLOY_GOAL = input(id: 'mavenDeployGoal', message: 'Enter the Maven goal to execute:', parameters: [[$class: 'ChoiceParameterDefinition', choices: ['clean', 'deploy'], name: 'MAVEN_GOAL']])
        //         }
        //     }
        // }
        stage('Run Maven to upload into nexus') {
            steps {           
                // sh 'mvn -s settings.xml'
                sh "mvn -s settings.xml ${MAVEN_DEPLOY_GOAL}"
                }
        }
        // stage ('Deployment') {
        //     agent {
        //         label 'Atti'
        //     }
        // steps {
        //        checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Hari-Ramesh/java-maven-war-appH.git']]) 
        //     }
        // steps {
        //        sh 'ansible-playbook -i inventory.yml deployment_playbook.yml -e "build_number=${BUILD_NUMBER}"'
        //     }
        // }    
        // stage ('ansible dep'){
        //     steps {
        //        sh 'ansible-playbook -i inventory.yml deployment_playbook.yml -e "build_number=${BUILD_NUMBER}"'
        //     }
        // }        
    }
}

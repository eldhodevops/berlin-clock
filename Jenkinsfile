pipeline {
    agent any

    tools {
        jdk 'jdk8'
        maven 'maven3'
    }

    stages {
        stage('install and sonar parallel') {
            steps {
                parallel(install: {
                    sh "mvn -U clean test cobertura:cobertura -Dcobertura.report.format=xml"
                }, sonar: {
                    sh "mvn sonar:sonar -Dsonar.host.url=http://172.17.0.3:9000"
                 
                    
                })
            }
            post {
                always {
                    junit '**/target/*-reports/TEST-*.xml'
                    step([$class: 'CoberturaPublisher', coberturaReportFile: 'target/site/cobertura/coverage.xml'])
                }
            }
        }
    }
}


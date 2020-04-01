pipeline{
    tools{
        maven 'my_maven'
        jdk 'my_java'
    }
    agent {label 'aws_centos_node'}
    stages{
        stage('Compile'){
            steps{
                sh 'mvn compile'
            }
        }
        stage('Code_Review'){
            steps{
                sh 'mvn pmd:pmd'
            }
            post{
                always{
                    pmd pattern: 'target/pmd.xml'
                }
            }
        }
        stage('Unit_Test'){
            steps{
                sh 'mvn test'
            }
            post{
                always{
                    junit 'target/surefire-reports/*.xml'

                }
            }
        }
        stage('Metric_Check'){
            steps{
                sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
            }
            post{
                always{
                    cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
                }
            }
        }
        stage('Package'){
            steps{ 
                sh 'mvn package'
            }
        }  
    }
}

pipeline {
    agent any

    stages {
        stage('repo') {
            steps {
                echo '******************'
                // Get some code from a GitHub repository
                git branch: 'main', credentialsId: 'github-nn', url: 'https://github.com/nitishnambiar/jgsu-spring-petclinic.git'
                echo '******************'
                // Run Maven on a Unix agent.
                //sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('Build') {
            steps {
                echo '******************'
                // Run Maven on a Unix agent.
                sh " ./mvnw spring-javaformat:apply"
                sh " ./mvnw compile"
                echo '******************'
                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('test') {
            steps {
                echo '******************'
                // Run Maven on a Unix agent.
                sh " ./mvnw test"
                echo '******************'
                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('package') {
            steps {
                echo '******************'
                // Run Maven on a Unix agent.
                sh " ./mvnw package"
                echo '******************'
                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        
           post {
               // If Maven was able to run the tests, even if some of the test
               // failed, record the test results and archive the jar file.
               always {
                   //junit '**/target/surefire-reports/TEST-*.xml'
                   archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
               }
           }
        }
    }
}

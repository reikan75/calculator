pipeline{
    agent any
    stages{
        stage("Checkout"){
            steps{
                git branch: 'main', credentialsId: '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', url: 'https://github.com/reikan75/calculator.git'
            }
        }
        
        stage("Compile"){
            steps{
               sh "./gradlew clean" 
               sh "./gradlew compileJava" 
            }
        }
        
        stage("Unit Test") {
          steps {
              echo 'For now i replace the unit tests'
          }  
        }
        
        stage("Code coverage"){
        	steps{
        		sh "./gradlew test jacocoTestReport"
        		publishHTML (target: [
        			reportDir: 'build/reports/jacoco/test/html',
        			reportFiles: 'index.html',
        			reportName: 'JaCoCo Report'
        		])
        		sh "./gradlew jacocoTestCoverageVerification"
        	}
        }

        stage("Checkstyle"){
        	steps{
        		sh "./gradlew checkstyleMain"
        		publishHTML (target: [
        			reportDir: 'build/reports/checkstyle/',
        			reportFiles: 'main.html',
        			reportName: 'Checkstyle Report'
        		])
        		sh "./gradlew jacocoTestCoverageVerification"
        	}
        }
        stage("Package"){
            steps{
                sh "./gradlew build"
            }
        }
        stage("Docker build"){
            steps{
                sh "docker build -t reikan/calculator ."
            }
        }
        stage("Docker push"){
            steps{
                sh "docker push reikan/calculator"
            }
        }
        stage("Deploy to staging"){
            steps{
                sh "docker run -d --rm -p 8765:8080 --name calculator reikan/calculator"
            }
        }
        stage("Acceptance test"){
            steps{
                sleep 60
                sh "chmod +x acceptance_test.sh && ./acceptance_test.sh"
            }
        }
    }
    post{
        always{
            sh "docker stop calculator"
        }
    }
}

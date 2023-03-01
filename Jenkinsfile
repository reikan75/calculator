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
    }
}
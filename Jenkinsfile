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
        		sh "./gradlew jacocoTestReport"
        		publishHTML(target:[
        			reportDir: 'build/reports/jacoco/test/html',
        			reportFiles: 'index.html',
        			reportName: 'Jacoco Report'
        		])
        		sh "./gradlew jacocoTestCoverageVerification"
        	}
        }
    }
}
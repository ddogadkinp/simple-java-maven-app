pipeline { 
    
    agent { 
        docker { 
            image 'maven:3.8.4-ibmjava-alpine' 
            args '-v /Users/denisdogadkin/.m2:/root/.m2'  
        } 
    } 
  
    options { 
        skipStagesAfterUnstable() 
    } 

    stages { 
      
        stage('Build') { 
            steps { 
                echo "Build"
                sh 'mvn -B -DskipTests clean package' 
            } 
        } 

        stage('Test') { 
            steps {
                echo "Test"
                //sh 'mvn test' 
            } 
          
            post { 
                always { 
                    junit 'target/surefire-reports/*.xml' 
                } 
            } 
        } 

        stage('Deliver') {  
            steps { 
                echo "Deliver"
                //sh './jenkins/scripts/deliver.sh'  
            } 
        } 
    } 
} 

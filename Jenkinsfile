pipeline { 
    
    agent { 
        docker { 
            image 'maven:3-alpine'  
        } 
    } 
  
    options { 
        skipStagesAfterUnstable() 
    } 

    stages { 
      
        stage('Build') { 
            steps { 
                echo "Build"
                script {
                    System.setProperty("org.jenkinsci.plugins.durabletask.BourneShellScript.LAUNCH_DIAGNOSTICS", "true");
                }
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

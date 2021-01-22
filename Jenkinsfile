pipeline {
     agent any
	 tools {
        maven 'maven3.6' 
	jdk 'jdk1.8'
	allure 'allure2'
    }
	 environment {
        containerName = "shraddhal/seleniumtest2"
        container_version = "1.0.0.${BUILD_ID}"
        dockerTag = "${containerName}:${container_version}"
		     
    }
    stages { 	
	    stage('Clone repository') {
			   steps {	       
				 git 'https://github.com/shraddhaL/selenium_repo2.git' }
        
			   }
	    
	   stage('Build Jar') {
	    
		steps {////
		   	//sh'docker stop $(docker ps -q) || docker rm $(docker ps -a -q) || docker rmi $(docker images -q -f dangling=true)'
        		bat 'docker system prune --all --volumes --force'
		       bat 'mvn clean package -DskipTests'
        }
        }
	   
	    
	  /*   stage('Build Image') {
            steps {
                script {
                	app = docker.build("shraddhal/seleniumtest2")
                }
            }
        }
	    
	    
       stage('Push Image') {
            steps {
                script {// aws:76599700-71c5-4af4-b805-1bcd97a088e4
			     withCredentials([usernamePassword( credentialsId: 'aecd95e5-cb44-4e0e-93e9-52385789176c', usernameVariable: 'shraddhal', passwordVariable: 'dockerhub1234')]) {
					
			docker.withRegistry('https://registry.hub.docker.com', 'aecd95e5-cb44-4e0e-93e9-52385789176c') {
					bat "docker login -u shraddhal -p dockerhub1234"
					app.push("${BUILD_NUMBER}")
					app.push("latest")
				}
			
             		   }
         	   }
	      }        
   	 }
	    */
	    
	    stage('compose') {
            steps {
                script {
			//sh 'docker run -d -p 4444:4444 --memory="1.5g" --memory-swap="2g" -v /dev/shm:/dev/shm selenium/standalone-chrome'
			bat 'docker-compose up -d --scale chrome=3'
			
                }
	    }
        }
	   
	 stage('test') {
            steps {
                script {
			bat 'mvn -Dtest="SearchTest.java,SearchTest2.java" test'
			/*bat 'allure generate target/allure-results --clean'
			bat 'allure open target/allure-report/'
			bat 'allure serve C:/Users/Dilip/.jenkins/workspace/seleniumAssi3-local-allure/target/surefire-reports/'
			 bat 'mvn allure:serve'
		  	 bat 'mvn allure:report'*/
                }
	    }
        }    
	    
	  /*   stage('Create Report') {
		    steps {
                script {
        // Generate Allure Report
			
        allure includeProperties: false, jdk: '', results: [[path: 'allure-results']]
		}}}
	   */ 
	 /*   stage('Execute') {
		 steps {
                script {
		// Execute the pytest script. On faliure proceed to next step
        catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
     // bat 'mvn test'
            //  bat 'docker run --network="host" --rm -v C:\Windows\System32\config\systemprofile\AppData\Local\Jenkins\.jenkins\workspace\seleniumAssi3\target\allure-results:\AllureReports shraddhal/seleniumtest  --browser "chrome" .'
       bat 'docker run --network="host" --rm -v C:\\Windows\\System32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\seleniumAssi3\\target\\allure-results:\\AllureReports shraddhal/seleniumtest2  -v /dev/shm:/dev/shm --suitename "testng.xml" --executor "remote" --browser "chrome" .'
	}}}
  	 }
	    
	     */
}  /*
post {
          always {
            script {
		    
		  
              allure([
                includeProperties: false,
                jdk: '',
		      properties: [[key: 'allure.results.directory', value: '**/target/allure-results']],
                reportBuildPolicy: 'ALWAYS',
                results: [[path: 'target/allure-results']]
              ])
            }
          }
        }
		*/	
}

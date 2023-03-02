node {
    stage ("Checkout DataService"){
        git branch: 'main', url: 'https://github.com/bgoggins/Team4ProjectData.git'
    }
    
    stage ("Gradle Build - DataService") {
	
        sh 'gradle clean build'

    }
    
    stage ("Gradle Bootjar-Package - DataService") {
        sh 'gradle bootjar'
    }
	
	stage ("Containerize the app-docker build - DataApi") {
        sh 'docker build --rm -t team4-data:v1.1 .'
    }
    
    stage ("Inspect the docker image - DataApi"){
        sh "docker images team4-data:v1.1"
        sh "docker inspect team4-data:v1.1"
    }
    
    stage ("Run Docker container instance - DataApi"){
        sh "docker run -d --rm --name team4-data -p 8080:8080 team4-data:v1.1"
     }
    
    stage('User Acceptance Test - DataService') {
	
	  def response= input message: 'Is this build good to go?',
	   parameters: [choice(choices: 'Yes\nNo', 
	   description: '', name: 'Pass')]
	
	  if(response=="Yes") {

	    stage('Release- DataService') {
		 sh "docker stop team4-data"
	     sh 'echo MCC DataService is ready to release!'

	    }
	  }
    }
}

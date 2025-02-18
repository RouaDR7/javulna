pipeline { // Defines a pipeline
  agent any // Specifies that the pipeline can be run on any available agent

  tools { // Configures the tools used in the pipeline
    maven 'maven' // Specifies the Maven tool that should be used in the pipeline
  }

  stages { // Defines the different stages of the pipeline
    stage('Checkout Source') { // Defines the 'Checkout Source' stage
      steps { // Specifies the steps to be executed within this stage
        git 'https://github.com/MarwenSoula/javulna.git' // Retrieves the source code from the specified GitHub repository
      }
    }

    stage ('Secret scanner') { 
      steps { 
        sh 'gitleaks detect --source  . -f json --report-path gitleaks.json || true'  
      }   
    }
stage('SonarQube Analysis') {
      steps {
        sh "mvn clean verify sonar:sonar \
            -Dsonar.projectKey=MyProject \
            -Dsonar.host.url=http://localhost:9010 \
            -Dsonar.login=sqp_6bb33359ef73d245121b0718747b78155015b0a9"
      }
    }

    
   stage ('Unit Test') { // Defines the 'Unit Test' stage
      steps { // Specifies the steps to be executed within this stage
        sh 'mvn test' // Runs the Maven command to execute the unit tests
      }   
    }
 stage ('Build') { // Defines the 'Build' stage
      steps { // Specifies the steps to be executed within this stage
        sh 'mvn clean install' // Runs the Maven command to clean and build the project
      }   
    }
    stage ('docker build') { // Defines the 'docker build' stage
      steps { // Specifies the steps to be executed within this stage
        sh 'docker build -t javulna-0.1 .' // Builds a Docker image with the specified tag
      }   
    }

 stage ('docker scann') { // Defines the 'docker build' stage
      steps { 
        sh ' trivy image --format json -o docker-report.json javulna-0.1 ' // Builds a Docker image with the specified tag
      }   
 }
     stage ('docker run container') { // Defines the 'docker run container' stage
      steps { // Specifies the steps to be executed within this stage
        sh 'docker stop app || true' // Stops any running container with the name 'app'
        sh 'docker rm app || true' // Removes the container with the name 'app' if it exists
        sh 'docker run --name app -it -d -p 9001:8080 javulna-0.1' // Runs a new Docker container named 'app' based on the 'javulna-0.1' image, with port mapping from 8080 to 9000, in detached mode (-d), and allocates a pseudo-TTY (-it)
     }
   }
 }
}
 

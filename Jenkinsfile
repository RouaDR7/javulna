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


 }
}
 

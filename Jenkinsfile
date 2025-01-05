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

    stage('SonarQube Analysis') {
      steps {
        sh "mvn  verify sonar:sonar \
             -Dsonar.projectKey=TEST1 \
             -Dsonar.host.url=http://192.168.27.128:9002 \
             -Dsonar.login=sqp_24c9c23056ca58b9baf086f13aa08e6a32981f53"
      }
    }

 }
}
 

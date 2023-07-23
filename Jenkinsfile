def registry = 'https://lanka.jfrog.io'
def imageName = 'lanka.jfrog.io/image-docker/image'
   def version   = '2.1.2'
pipeline{
    agent { label 'slave-server' }
    environment{
        PATH = "/opt/apache-maven-3.9.3/bin:$PATH"
    }
    stages {
stage("build"){
          steps{
                sh 'mvn clean deploy'
            }
        }
        // 
             
           
    stage(" Docker Build ") {
      steps {
        script {
           echo '<--------------- Docker Build Started --------------->'
           app = docker.build(imageName+":"+version)
           echo '<--------------- Docker Build Ends --------------->'
        }
      }
    }

            stage (" Docker Publish "){
        steps {
            script {
               echo '<--------------- Docker Publish Started --------------->'  
                docker.withRegistry(registry, 'jfrog-cred'){
                    app.push()
                }    
               echo '<--------------- Docker Publish Ended --------------->'  
            }
        }
    }
        //
    }
    }


def echoBanner(def ... msgs) {
   echo createBanner(msgs)
}

def errorBanner(def ... msgs) {
   error(createBanner(msgs))
}

def createBanner(def ... msgs) {
   return """
       ===========================================

       ${msgFlatten(null, msgs).join("\n        ")}

       ===========================================
   """
}

pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echoBanner("build", ["mvn install"])
                sh 'mvn install'
                    }
                }
        stage('check'){
            steps{
                
               echoBanner("check", ["checking diskspace", "saying hi"])
               step([$class: 'HelloWorldBuilder', name:'Liberis'])
               } 
            }
        }
    }

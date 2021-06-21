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

// flatten function hack included in case Jenkins security
// is set to preclude calling Groovy flatten() static method
// NOTE: works well on all nested collections except a Map
def msgFlatten(def list, def msgs) {
   list = list ?: []
   if (!(msgs instanceof String) && !(msgs instanceof GString)) {
       msgs.each { msg ->
           list = msgFlatten(list, msg)
       }
   }
   else {
       list += msgs
   }

   return  list
}
environments = 'lab\nstage\npro'
def props = readProperties  file: 'demo.environment'
properties([
    parameters([
        [$class: 'CascadeChoiceParameter', 
            choiceType: 'PT_CHECKBOX1',
            description: 'Select a choice',
            filterLength: 1,
            filterable: true,
            name: 'choice1',
            referencedParameters: 'ENVIRONMENT',
            script: [$class: 'GroovyScript',
                fallbackScript: [
                    classpath: [], 
                    sandbox: true, 
                    script: 'return ["ERROR"]'
                ],
                script: [
                    classpath: [], 
                    sandbox: true, 
                    script: """
                        if (ENVIRONMENT == 'lab') { 
                            return[props]
                        }
                        else {
                            return[props]
                        }
                    """.stripIndent()
                ]
            ]
        ]
    ])
])

pipeline {
    agent any

    parameters {
        choice(name: 'ENVIRONMENT', choices: "${environments}")
    }

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

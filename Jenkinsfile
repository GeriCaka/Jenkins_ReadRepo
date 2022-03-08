pipeline {
    agent any
    parameters {
        activeChoiceParam('Service') {
            description('Select service you wan to deploy')
            choiceType('SINGLE_SELECT')
            groovyScript {
                script("return ['web-service', 'proxy-service', 'backend-service']")
                fallbackScript('"fallback choice"')
            }
        }
        activeChoiceReactiveParam('Tag') {
            description('Select tag from dockerhub')
            choiceType('SINGLE_SELECT')
            groovyScript {
                script('''
                    import groovy.json.JsonSlurperClassic
                    import jenkins.model.Jenkins

                    image = imageName(Service)
                    token = getAuthTokenDockerHub()
                    tags = getTagFromDockerHub(image, token)
                    return tags

                    def getTagFromDockerHub(imgName, authToken) {
                        def url = new URL("https://hub.docker.com/v2/repositories/${imgName}/tags?page=1&page_size=50")
                        def parsedJSON = parseJSON(url.getText(requestProperties:["Authorization":"JWT ${authToken}"]))
                        def regexp = "^\\d{1,2}.\\d{1,2}\$"
                        parsedJSON.results.findResults { 
                        it.name =~ /$regexp/ ? "${it.name}".toString() : null
                        }
                    }

                    def getAuthTokenDockerHub() {
                        def creds = com.cloudbees.plugins.credentials.CredentialsProvider.lookupCredentials(
                        com.cloudbees.plugins.credentials.common.StandardUsernameCredentials.class,
                        Jenkins.instance,
                        null,
                        null)
                        for (c in creds) {
                        if (c.id == "dockerhub_credentials") {
                            user = c.username
                            pass = c.password
                        }
                        }
                        def url = new URL("https://hub.docker.com/v2/users/login/")
                        def conn = url.openConnection()
                        conn.setRequestMethod("POST")
                        conn.setRequestProperty("Content-Type", "application/json")
                        conn.doOutput = true

                        def authString = "{\"username\": \"${user}\", \"password\": \"${pass}\"}"
                        def writer = new OutputStreamWriter(conn.outputStream)
                        writer.write(authString)
                        writer.flush()
                        writer.close()
                        conn.connect()

                        def result = parseJSON(conn.content.text)
                        return result.token
                    }
                    def parseJSON(json) {
                        return new groovy.json.JsonSlurperClassic().parseText(json)
                    }
                    def imageName(name){
                    return "bartekj/${name}".toString()
                    }               
                ''')
                fallbackScript('"fallback choice"')
            }
            referencedParameter('Service')
        }
        choiceParam('Environment', ['test', 'stage', 'prod'], 'Select environment')
    }  
        
}

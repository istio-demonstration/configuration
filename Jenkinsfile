pipeline {
   agent any

   environment {
    
     // YOUR_DOCKERHUB_USERNAME (it doesn't matter if you don't have one)
     // get curretn commit sha, command 'git rev-parse HEAD' return full sha
     // if you wanna push image to dockerhub, image name must be unique
     GITCOMMITSHA = sh(returnStdout: true, script: "git log -n 1 --pretty=format:'%h'").trim()
     SERVICE_NAME = "configuration"
     // ORGANIZATION_NAME = 'ERP-CI-CD-Organization'
   
   }

   stages {
      stage('Preparation') {
         steps {
            cleanWs()
            git credentialsId: 'GitHub', url: "https://github.com/${ORGANIZATION_NAME}/${SERVICE_NAME}"
         }
      }

      stage('apply configuration') {
          steps {
                 // sh 'kubectl apply -f addons'
                 // sh 'kubectl apply -f chat-api-env-configMap.yaml'
                  sh 'kubectl apply -f circuit-breaking'
                  sh 'kubectl delete -f default-ingress-gateway-config.yaml'
                  sh 'kubectl apply -f istio-system-ingress-gateway-config.yaml'
                }
      }
   }
}
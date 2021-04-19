// Uses Declarative syntax to run commands inside a container.
pipeline {
    agent {
        kubernetes {
            // Rather than inline YAML, in a multibranch Pipeline you could use: yamlFile 'jenkins-pod.yaml'
            // Or, to avoid YAML:
            // containerTemplate {
            //     name 'shell'
            //     image 'ubuntu'
            //     command 'sleep'
            //     args 'infinity'
            // }
            yaml '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: shell
    image: ubuntu
    resources:
      limits:
        cpu: "50m"
        memory: "50Mi"
      requests:
        cpu: "50m"
        memory: "50Mi"
    command:
    - sleep
    args:
    - infinity
  - name: jnlp
    resources:
      limits:
        cpu: "200m"
        memory: "150Mi"
      requests:
        cpu: "200m"
        memory: "150Mi"
'''
            // Can also wrap individual steps:
            // container('shell') {
            //     sh 'hostname'
            // }
            defaultContainer 'shell'
        }
    }
    stages {
        stage('Main') {
            steps {
		echo "Printing contents of testfile.txt"
                container('shell') {
		    sh 'cat testfile.txt'
		    sh 'sleep 60'
		}
            }
        }
    }
}


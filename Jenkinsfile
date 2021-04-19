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
    resourceLimitCpu: "50m"
    resourceLimitMemory: "150Mi"
    resourceRequestCpu: "50m"
    resourceRequestMemory: "150Mi"
    command:
    - sleep
    args:
    - infinity
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


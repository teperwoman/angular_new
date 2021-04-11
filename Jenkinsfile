pipeline {
  agent {
    kubernetes {
      label "jenkins-slave-test-${env.BUILD_NUMBER}"
      defaultContainer 'docker'
      yaml """
metadata:
  labels:
    some-label: some-label-value
spec:
  containers:
    - name: docker
      image: docker:18.09.9
      command:
        - cat
      tty: true
      volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /etc/docker/daemon.json
          name: docker-daemon-json
  volumes:
    - name: docker-sock
      hostPath:
        path: /var/run/docker.sock
    - name: docker-daemon-json
      hostPath:
        path: /etc/docker/daemon.json
"""
    }
  }
  stages
  {
    stage('build')
    {
      steps
      {
          sh "docker build -t tftest/angular:${env.BUILD_NUMBER} ."
      }
    }
    stage('merde')
    {
      steps
      {
          sh "echo bravo"
      }
    }
  }
}
node {
    stage('Checkout git repo') {
      sh(script: "cd /opt/AspNetCore-Sample, returnStdout: true)
      sh(script: "sudo git stash, returnStdout: true)
      sh(script: "sudo git pull, returnStdout: true)
    }
    stage('Build and push Docker image') {
      sh(script: "sudo docker build -t 9011603079/testing-repo:customerapi -f src/CustomersAPI/Dockerfile .", returnStdout: true)
      sh(script: "sudo docker push 9011603079/testing-repo:customerapi", returnStdout: true)
      sh(script: "sudo docker build -t 9011603079/testing-repo:customermvc -f src/CustomersMVC/Dockerfile .", returnStdout: true)
      sh(script: "sudo docker push 9011603079/testing-repo:customermvc", returnStdout: true)
    }
    stage('Unit Tests') {
      sh 'echo test'
    }
    stage('Browser Tests'){
        parallel(
            "Edge":{sh 'echo test'},
            "Firefox":{sh 'echo test'},
            "Chrome":{sh 'echo test'}
            )
    }
    stage('Deploy into k8s') {
      sh(script: "sudo kubectl apply -f /opt/AspNetCore-Sample/dotnet.yaml", returnStdout: true)
    }
}

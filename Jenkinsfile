abcs = ['curl -s -o /dev/null -w "%{http_code}" http://admin01:7001/console', 'curl -s -o /dev/null -w "%{http_code}" http://admin01:7001/console', 'curl -s -o /dev/null -w "%{http_code}" http://admin01:7001/console']

pipeline{
    agent { label 'linuxagent' }
            stages{
                    stage('Stop'){
                        steps{
                            echo "${Clust_Name}"
                            echo "Stopping Managed Server"
                            sh 'ssh admin01@127.0.0.1 df -h'
                        }
                                 
                    }
                    stage('Start'){
                        steps{
                            echo "Starting Managed Server"
                            sh 'ssh admin01@127.0.0.1 du -sh'
                            
                        }
                                 
                    }
                    stage('Test'){
                        when {
                            expression {"${HealthCheck}" == 'true'}
                        }
                        steps{
                            loop_of_sh(abcs)
                        }
                                 
                    }
                    
           }

}

def loop_of_sh(list) {
    list.each { item ->
        echo "${item}"
        sh "${item}"
    }
}

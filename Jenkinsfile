node {
   stage ('Checkout'){
        checkout scm
   }

   stage('Build') {
      bat "mvn clean package"
      dir('target\\classes'){
        stash name: "tmi_perf_test.yml", includes: "*"
      }
   }
   stage('Performance Tests') {
        BlazeMeterTest: {
            dir ('target\\classes') {
                bat 'bzt tmi_perf_test.yml -report'
            }
            perfReport '**/target/classes/*.csv'
        }
   }
   stage('Deploy') {
     dir('target\\classes'){
           unstash "tmi_perf_test.yml"
     }
   }
}

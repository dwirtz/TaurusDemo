node {
   stage ('Checkout'){
        checkout scm
   }

   stage('Build') {
      bat "mvn clean package"
      dir('target\\classes'){
        stash name: "perf_test.yml", includes: "*"
      }
   }
   stage('Performance Tests') {
        BlazeMeterTest: {
            dir ('target\\classes') {
                bat 'bzt perf_test.yml -report'
            }
            perfReport '**/target/classes/*.csv'
        }
   }
   stage('Deploy') {
     dir('target\\classes'){
           unstash "perf_test.yml"
     }
   }
}

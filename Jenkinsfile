node {
   stage('Build') {
      // Run the Taurus build
   }
   stage('Performance Tests') {
        BlazeMeterTest: {
            dir ('src\\main\\resources') {
                bat 'bzt tmi_perf_test.yml -report'
            }
        }
   }
   stage('Deploy') {
   }
}

node {
   stage('Build') {
      // Run the Taurus build
   }
   stage('Performance Tests') {
    parallel(
        BlazeMeterTest: {
            dir ('src/main/resources') {
                sh 'bzt tmi_perf_test.yml -report'
            }
        },
   }
   stage(‘Deploy’) {
   }
}

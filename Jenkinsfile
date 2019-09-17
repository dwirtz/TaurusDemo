node {
   stage('Build') {
      configFileProvider([configFile(fileId: 'org.jenkinsci.plugins.configfiles.maven.GlobalMavenSettingsConfig1407837213087', variable: 'MAVEN_SETTINGS_XML')]) {
        // Run the maven build
        bat "./mvnw -s $MAVEN_SETTINGS_XML clean package"
      }
      dir('target\\classes'){
        stash name: "tmi_perf_test.yml", includes: "*"
      }
   }
   stage('Performance Tests') {
        BlazeMeterTest: {
            dir ('target\\classes') {
                bat 'bzt tmi_perf_test.yml -report'
            }
        }
   }
   stage('Deploy') {
     dir('target\\classes'){
           unstash "tmi_perf_test.yml"
     }
   }
}

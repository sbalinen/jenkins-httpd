node {
stage 'CI'
    git branch: 'dev', 
        url: 'https://github.com/sbalinen/httpd'        
stage 'Deploy'
    input 'Deploy application?'
    sshPublisher(publishers: [sshPublisherDesc(configName: 'jenkinsdeploy_test', transfers: [sshTransfer(excludes: '', execCommand: '/home/sbalinen/jenkins-httpd/usr/sbin/httpd -f /home/sbalinen/jenkins-httpd/etc/httpd/conf/httpd.conf -p /home/sbalinen/jenkins-httpd/run/httpd/httpd.pid -k restart', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: 'jenkins-httpd/var/', remoteDirectorySDF: false, removePrefix: 'var', sourceFiles: 'var/*')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])   
	notify('Web server started')
}
def notify(status){
    emailext (
      to: "sbalinen@ftdi.com",
      subject: "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
    )
}

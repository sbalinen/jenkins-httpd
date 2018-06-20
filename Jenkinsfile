node {
stage 'CI'
	checkout scm
    //git branch: 'dev', 
        //url: 'https://github.com/sbalinen/httpd'        
stage 'Deploy'
    input 'Deploy application?'
    sshPublisher(publishers: [sshPublisherDesc(configName: 'jenkinsdeploy_test', transfers: [sshTransfer(excludes: '', execCommand: '/home/sbalinen/jenkins-httpd-bak/usr/sbin/httpd -f /home/sbalinen/jenkins-httpd-bak/etc/httpd/conf/httpd.conf -k restart', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: 'jenkins-httpd-bak/var/www/html/', remoteDirectorySDF: false, removePrefix: 'var/www/html', sourceFiles: 'var/www/html/*.html')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])

    //sshPublisher(publishers: [sshPublisherDesc(configName: 'jenkinsdeploy_test', transfers: [sshTransfer(excludes: '', execCommand: '/home/sbalinen/jenkins-httpd-bak/usr/sbin/httpd -f /home/sbalinen/jenkins-httpd-bak/etc/httpd/conf/httpd.conf -k restart', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/home/sbalinen/jenkins-httpd-bak/var/www/html/', remoteDirectorySDF: false, removePrefix: 'var/www/html', sourceFiles: 'var/www/html/*.html')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])

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

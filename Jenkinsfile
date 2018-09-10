node {
    def mvnHome = tool 'maven3'
    
    // Mark the code checkout 'stage'....
    stage 'Checkout'
    // Get some code from a GitHub repository
    git url: 'https://github.com/jijeesh/Java-Junit-Selenium.git'
    stage 'Compile'
    sh "${mvnHome}/bin/mvn compile"
    stage 'Test'
    sauce('saucelabs') {
        sauceconnect(useGeneratedTunnelIdentifier: true, verboseLogging: true) {
            sh "${mvnHome}/bin/mvn test"
        }
    }
    stage 'Collect Results'
    step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
    step([$class: 'SauceOnDemandTestPublisher'])
}

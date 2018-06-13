node (label: 'Node1') {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

     stage ('Install Maven') {
           sh 'mvn install'
     }
	 
    stage ('Compile Stage') {
          sh 'mvn clean package test'
    }
    
    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("myawsecr")
    }

        stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
            docker.withRegistry('https://694839757085.dkr.ecr.ap-south-1.amazonaws.com', 'ecr:ap-south-1:demo-ecr-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}

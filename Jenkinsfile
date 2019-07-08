node {
    stage('specifying git url')
    git url: 'https://github.com/Reshma-rechu/Git_repo.git'

    // Get Artifactory server instance, defined in the Artifactory Plugin administration page.
    stage('upload and download')
    def server = Artifactory.server "Artifactory-1"

    // Read the upload spec and upload files to Artifactory.
    def downloadSpec =
            '''{
            "files": [
                {
                    "pattern": "Reshma_Repo/*.txt",
                    "target": "dependencies/",
                    "props": "p1=v1;p2=v2"
                }
            ]
        }'''

    def buildInfo1 = server.download spec: downloadSpec

    // Read the upload spec which was downloaded from github.
    def uploadSpec =
            '''{
            "files": [
                {
                    "pattern": "*.txt",
                    "target": "Reshma_Repo",
                    "props": "p1=v1;p2=v2"
                }
            ]
        }'''

    // Upload to Artifactory.
    def buildInfo2 = server.upload spec: uploadSpec

    // Merge the upload and download build-info objects.
    buildInfo1.append buildInfo2

    // Publish the build to Artifactory
    server.publishBuildInfo buildInfo1
}

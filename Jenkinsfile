node {
  library('vapps')
  stage 'Init'
  checkout scm
  
  dotnet=dotnetFactory(tool('MSBuild15'), "packages\\xunit.runner.console.2.2.0\\tools\\xunit.console.exe")
	build=buildFactory()
  
  // build pipeline
  build.pipeline {
	build.
		 stage('Build') {
			dotnet.msbuild('ManagedWinapi.sln',"Release", "\"/p:OutDir=${outputdir}\"")
		}
  }

  // artifacts
  archiveArtifacts 'build/**'
}
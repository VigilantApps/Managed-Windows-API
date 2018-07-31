node {
  library('vapps')
  stage 'Init'
  checkout scm
  
  dotnet=dotnetFactory(tool('MSBuild15'), "packages\\xunit.runner.console.2.2.0\\tools\\xunit.console.exe")
  
  // build pipeline
  build.pipeline {
	build.
		prereqs(dotnetcore: false, dotnetframework: true).
		codeAnalysis(project: 'alpha-vapps-cb9', ignoreQualityGate: true/*TODO: remove this eventually*/) {
			dotnet.msbuild('ManagedWinapi.sln',"Release", "\"/p:OutDir=${outputdir}\"")
		}
  }

  // artifacts
  archiveArtifacts 'build/**'
}
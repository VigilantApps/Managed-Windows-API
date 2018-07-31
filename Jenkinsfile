node {
  library('vapps')
  stage 'Init'
  checkout scm
	
  String[] dotnetFrameworkProjects = [
		// desktop agent
		"ViProDesktopAgent",
  ]

  build=higherOrderBuildFactory(
			'9.0', 
			/packages\xunit.runner.console.2.3.1\tools\net452\xunit.console.exe/,
			tool('MSBuild15'),
			dotnetCoreProjects,
			dotnetFrameworkProjects)
  
  // build pipeline
  build.pipeline {
	build.
		prereqs(dotnetcore: false, dotnetframework: true).
		codeAnalysis(project: 'alpha-vapps-cb9', ignoreQualityGate: true/*TODO: remove this eventually*/) {
			build.
				dotnet_build_solution(solution: 'ManagedWinapi.sln')
		}
  }

  // artifacts
  archiveArtifacts 'build/**'
}
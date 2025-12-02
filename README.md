# DevhubWorkshop
Here is a list of all actions in github: 
https://github.com/marketplace?type=actions

To get started:

Fork this project.

Create an action with the yml file at .github/workflows/ci-pipeline.yml.
This file already has the basic steps (install .net, package restore ect)

In the application, .net 9 was used, so keep that in mind for the pipeline tasks.

# Code setup
1. Implement git version

GitVersion automatically generates consistent semantic version numbers from your Git history, removing manual versioning and ensuring every build and artifact is uniquely and predictably versioned.

 
There is 2 steps <br><br>
First you need to set it up: <br><br>
[https://gitversion.net/docs/](https://github.com/GitTools/actions/blob/main/docs/examples/github/gitversion/setup.md).

Then you need to execute: <br><br>
https://github.com/GitTools/actions/blob/main/docs/examples/github/gitversion/execute.md   
   
 
# Code quality and testing
1. Run the tests
   You can find documentation about how to test here: https://docs.github.com/en/actions/tutorials/build-and-test-code/net

2. Implement linting

   You can use JetBrains.ReSharper.GlobalTools if you run script in your pipeline. <br><br>

   This can be done with this action: https://github.com/actions/github-script
   
   Output the insepction to a jsonfile. <br><br>
   
   In a seperate step, use the analyzation script found under .github/scripts to analyze the findings from the inspection

   If you want a simpler approach, there is a specific github action for this: https://github.com/marketplace/actions/jetbrains-resharper-inspect-code

4. Static code analysis

   Log into 1password. Find the SonarQube item. Click on website url and login with the 1password credentials.
   Create a new project.

   Name it something like: ```<your-initials>-shoppingCart``` <br><br>
   Follow the guide provided in SonarQube.
   Hint: Sonar token can be created here: ```User > My Account > Security```

# Dependencies
1. Create an sbom file

   Create the sbomfile:
   https://github.com/CycloneDX/gh-dotnet-generate-sbom
   
   We need a server to push our sbom file to. <br><br>
   Download the latest docker-compose file for the server:
   
   ```curl -LO https://dependencytrack.org/docker-compose.yml```

   Once you have spun up this server locally, push your sbom file to your server in your pipeline: <br><br>
   https://github.com/DependencyTrack/gh-upload-sbom 


2. Implement Dependabot

   Create a seperate yaml-file for another pipeline action. This is where you will implement dependabot. <br><br>
   You can set to run once every morning, night or on every pull request made on the Shoppingcart repo. <br><br>
   This is to ensure your dependecies is up to date.

   Documentation: https://docs.github.com/en/code-security/dependabot/working-with-dependabot/automating-dependabot-with-github-actions
   
   
# Security scanning 
1. Implement Git leaks

   You can use github's own action for this: https://github.com/marketplace/actions/gitleaks. <br><br>
   If you find any vulnerabilties in the ShoppingCart application - fix them!
   
2. Implement Zap Scan

   Congratulations. You made it to the final boss!

   Here is how to implement the zap scanner:

   https://github.com/zaproxy/action-full-scan

   

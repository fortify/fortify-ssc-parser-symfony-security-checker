<x-tag-head>
<x-tag-meta http-equiv="X-UA-Compatible" content="IE=edge"/>

<x-tag-script language="JavaScript"><!--
<X-INCLUDE url="https://cdn.jsdelivr.net/gh/highlightjs/cdn-release@10.0.0/build/highlight.min.js"/>
--></x-tag-script>

<x-tag-script language="JavaScript"><!--
<X-INCLUDE url="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js" />
--></x-tag-script>

<x-tag-script language="JavaScript"><!--
<X-INCLUDE url="${gradleHelpersLocation}/spa_readme.js" />
--></x-tag-script>

<x-tag-style><!--
<X-INCLUDE url="https://cdn.jsdelivr.net/gh/highlightjs/cdn-release@10.0.0/build/styles/github.min.css" />
--></x-tag-style>

<x-tag-style><!--
<X-INCLUDE url="${gradleHelpersLocation}/spa_readme.css" />
--></x-tag-style>
</x-tag-head>

# Fortify SSC Parser Plugin for Symfony Security Checker

## Introduction

This Fortify SSC parser plugin allows for importing scan results from Symfony Security Checker.

### Deprecation notice

The Symfony/SensioLabs PHP Security Checker is no longer functional as stated at https://github.com/sensiolabs/security-checker#readme, and as such this parser plugin has been deprecated. 

At the time of writing the JSON output of the alternative [Local PHP Security Checker](https://github.com/fabpot/local-php-security-checker) is compatible with the Symfony Security Checker parser plugin, so existing users may consider sticking with this parser plugin to avoid having to re-audit their existing results. It is however strongly recommended to migrate to the new [Local PHP Security Checker parser plugin](https://github.com/fortify-ps/fortify-ssc-parser-php-security-checker).

Use the following steps to migrate from this parser plugin to the Local PHP Security Checker parser plugin:

1. Install and enable the Local PHP Security Checker parser plugin
2. Make sure your application version has no pending audit information
3. Download the application file for your application version
4. Make the following changes to the application file you just downloaded, using your favorite zip tool (the FPR file is just a zip file) and editor:
    * Inside the application file, rename `SYMFONY_SECCHECK.zip` to `PHP_SECCHECK.zip`
    * Inside `PHP_SECCHECK.zip`, update `scan.info` to show `engineType=PHP_SECCHECK` (instead of `engineType=SYMFONY_SECCHECK`)
    * Edit `audit.xml`, pre-pending a 'P' to all issue instance id's. For example, search for `instanceId="` and replace with `instanceId="P`
5. Upload the modified application file to SSC
6. Delete all previously uploaded SYMFONY_SECCHECK artifacts after verifying that the audit information has been successfully applied to the PHP_SECCHECK issues



### Related Links

* **Downloads**: https://github.com/fortify-ps/fortify-ssc-parser-symfony-security-checker/releases
    * _Development releases may be unstable or non-functional. The `*-thirdparty.zip` file is for informational purposes only and does not need to be downloaded._
* **Sample input files**: [sampleData](sampleData)
* **GitHub**: https://github.com/fortify-ps/fortify-ssc-parser-symfony-security-checker
* **Automated builds**: https://github.com/fortify-ps/fortify-ssc-parser-symfony-security-checker/actions
* **Symfony Security Checker resources**:
	* Web interface: https://security.symfony.com/
	* CLI interface: https://github.com/sensiolabs/security-checker


## Plugin Installation

These sections describe how to install, upgrade and uninstall the plugin.

### Install & Upgrade

* Obtain the plugin binary jar file
	* Either download from Bintray (see [Related Links](#related-links)) 
	* Or by building yourself (see [Developers](#developers))
* If you already have another version of the plugin installed, first uninstall the previously 
 installed version of the plugin by following the steps under [Uninstall](#uninstall) below
* In Fortify Software Security Center:
	* Navigate to Administration->Plugins->Parsers
	* Click the `NEW` button
	* Accept the warning
	* Upload the plugin jar file
	* Enable the plugin by clicking the `ENABLE` button
  
### Uninstall

* In Fortify Software Security Center:
	* Navigate to Administration->Plugins->Parsers
	* Select the parser plugin that you want to uninstall
	* Click the `DISABLE` button
	* Click the `REMOVE` button 


## Obtain results

Please see the Symfony Security Checker documentation for details on checking applications and 
generating reports. Note that the SSC parser plugin requires the uploaded reports to be in JSON
format.

## Upload results

As a 3<sup>rd</sup>-party results zip bundle:

* Generate a scan.info file containing a single line as follows:  
`engineType=SYMFONY_SECCHECK`
* Generate a zip file containing the following:
	* The scan.info file generated in the previous step
	* The JSON file containing scan results
* Upload the zip file generated in the previous step to SSC
	* Using any SSC client, for example FortifyClient or Maven plugin
	* Or using the SSC web interface
	* Similar to how you would upload an FPR file

As raw scan results:  

* Navigate to the Artifacts tab of your application version
* Click the `UPLOAD` button
* Click the `ADD FILES` button, and select the JSON file to upload
* Enable the `3rd party results` check box
* Select the `SYMFONY_SECCHECK` type

*Note that uploading raw scan results is only supported for manual uploads through the SSC web interface, and this functionality was removed in SSC 20.2 so no longer available in recent SSC versions. Please submit a feature request if you'd like to see this easier process for ad-hoc uploading of 3<sup>rd</sup>-party results restored, referencing Octane id #448174.*


## Developers

The following sections provide information that may be useful for developers of this utility.

### IDE's

This project uses Lombok. In order to have your IDE compile this project without errors, 
you may need to add Lombok support to your IDE. Please see https://projectlombok.org/setup/overview 
for more information.

### Gradle Wrapper

It is strongly recommended to build this project using the included Gradle Wrapper
scripts; using other Gradle versions may result in build errors and other issues.

The Gradle build uses various helper scripts from https://github.com/fortify-ps/gradle-helpers;
please refer to the documentation and comments in included scripts for more information. 

### Common Commands

All commands listed below use Linux/bash notation; adjust accordingly if you
are running on a different platform. All commands are to be executed from
the main project directory.

* `./gradlew tasks --all`: List all available tasks
* Build: (plugin binary will be stored in `build/libs`)
	* `./gradlew clean build`: Clean and build the project
	* `./gradlew build`: Build the project without cleaning
	* `./gradlew dist distThirdParty`: Build distribution zip and third-party information bundle
* `./fortify-scan.sh`: Run a Fortify scan; requires Fortify SCA to be installed

### Automated Builds

This project uses GitHub Actions workflows to perform automated builds for both development and production releases. All pushes to the main branch qualify for building a production release. Commits on the main branch should use [Conventional Commit Messages](https://www.conventionalcommits.org/en/v1.0.0/); it is recommended to also use conventional commit messages on any other branches.

User-facing commits (features or fixes) on the main branch will trigger the [release-please-action](https://github.com/google-github-actions/release-please-action) to automatically create a pull request for publishing a release version. This pull request contains an automatically generated CHANGELOG.md together with a version.txt based on the conventional commit messages on the main branch. Merging such a pull request will automatically publish the production binaries and Docker images to the locations described in the [Related Links](#related-links) section.

Every push to a branch in the GitHub repository will also automatically trigger a development release to be built. By default, development releases are only published as build job artifacts. However, if a tag named `dev_<branch-name>` exists, then development releases are also published to the locations described in the [Related Links](#related-links) section. The `dev_<branch-name>` tag will be automatically updated to the commit that triggered the build.


## License
<x-insert text="<!--"/>

See [LICENSE.TXT](LICENSE.TXT)

<x-insert text="-->"/>

<x-include url="file:LICENSE.TXT"/>


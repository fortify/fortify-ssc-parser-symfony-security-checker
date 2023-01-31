# Fortify SSC Parser Plugin for Symfony Security Checker 


<!-- START-INCLUDE:p.marketing-intro.md -->

Build secure software fast with [Fortify](https://www.microfocus.com/en-us/solutions/application-security). Fortify offers end-to-end application security solutions with the flexibility of testing on-premises and on-demand to scale and cover the entire software development lifecycle.  With Fortify, find security issues early and fix at the speed of DevOps. 

<!-- END-INCLUDE:p.marketing-intro.md -->



<!-- START-INCLUDE:repo-intro.md -->

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

<!-- END-INCLUDE:repo-intro.md -->


## Resources


<!-- START-INCLUDE:repo-resources.md -->

* **Releases**: https://github.com/fortify/fortify-ssc-parser-symfony-security-checker/releases
    * _Development releases may be unstable or non-functional. The `*-thirdparty.zip` file is for informational purposes only and does not need to be downloaded._
* **Sample input files**: [sampleData](sampleData)
* **Source code**: https://github.com/fortify/fortify-ssc-parser-symfony-security-checker
* **Automated builds**: https://github.com/fortify/fortify-ssc-parser-symfony-security-checker/actions
* **Contributing Guidelines**: [CONTRIBUTING.md](CONTRIBUTING.md)
* **Code of Conduct**: [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)
* **License**: [LICENSE.txt](LICENSE.txt)
* **Symfony Security Checker resources**:
	* Web interface: https://security.symfony.com/
	* CLI interface: https://github.com/sensiolabs/security-checker

<!-- END-INCLUDE:repo-resources.md -->


## Support

The software is provided "as is", without warranty of any kind, and is not supported through the regular Micro Focus Support channels. Support requests may be submitted through the [GitHub Issues](https://github.com/fortify/fortify-ssc-parser-symfony-security-checker/issues) page for this repository. A (free) GitHub account is required to submit new issues or to comment on existing issues. 

Support requests created through the GitHub Issues page may include bug reports, enhancement requests and general usage questions. Please avoid creating duplicate issues by checking whether there is any existing issue, either open or closed, that already addresses your question, bug or enhancement request. If an issue already exists, please add a comment to provide additional details if applicable.

Support requests on the GitHub Issues page are handled on a best-effort basis; there is no guaranteed response time, no guarantee that reported bugs will be fixed, and no guarantee that enhancement requests will be implemented. If you require dedicated support for this and other Fortify software, please consider purchasing Micro Focus Fortify Professional Services. Micro Focus Fortify Professional Services can assist with general usage questions, integration of the software into your processes, and implementing customizations, bug fixes, and feature requests (subject to feasibility analysis). Please contact your Micro Focus Sales representative or fill in the [Professional Services Contact Form](https://www.microfocus.com/en-us/cyberres/contact/professional-services) to obtain more information on pricing and the services that Micro Focus Fortify Professional Services can provide.

---

*This document was auto-generated from README.template.md; do not edit by hand*

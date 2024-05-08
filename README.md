# Fortify SSC Parser Plugin for Symfony Security Checker 


<!-- START-INCLUDE:p.marketing-intro.md -->

[Fortify Application Security](https://www.microfocus.com/en-us/solutions/application-security) provides your team with solutions to empower [DevSecOps](https://www.microfocus.com/en-us/cyberres/use-cases/devsecops) practices, enable [cloud transformation](https://www.microfocus.com/en-us/cyberres/use-cases/cloud-transformation), and secure your [software supply chain](https://www.microfocus.com/en-us/cyberres/use-cases/securing-the-software-supply-chain). As the sole Code Security solution with over two decades of expertise and acknowledged as a market leader by all major analysts, Fortify delivers the most adaptable, precise, and scalable AppSec platform available, supporting the breadth of tech you use and integrated into your preferred toolchain. We firmly believe that your great code [demands great security](https://www.microfocus.com/cyberres/application-security/developer-security), and with Fortify, go beyond 'check the box' security to achieve that.

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

* **Usage**: [USAGE.md](USAGE.md)
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



<!-- START-INCLUDE:h2.support.md -->

## Support

The only warranties for products and services of Open Text and its affiliates and licensors (“Open Text”) are as may be set forth in the express warranty statements accompanying such products and services. Nothing herein should be construed as constituting an additional warranty. Open Text shall not be liable for technical or editorial errors or omissions contained herein. The information contained herein is subject to change without notice.

The software is provided "as is" and is not supported through the regular OpenText Support channels. Support requests may be submitted through the [GitHub Issues](https://github.com/fortify/fortify-ssc-parser-symfony-security-checker/issues) page for this repository. A (free) GitHub account is required to submit new issues or to comment on existing issues. 

Support requests created through the GitHub Issues page may include bug reports, enhancement requests and general usage questions. Please avoid creating duplicate issues by checking whether there is any existing issue, either open or closed, that already addresses your question, bug or enhancement request. If an issue already exists, please add a comment to provide additional details if applicable.

Support requests on the GitHub Issues page are handled on a best-effort basis; there is no guaranteed response time, no guarantee that reported bugs will be fixed, and no guarantee that enhancement requests will be implemented. If you require dedicated support for this and other Fortify software, please consider purchasing OpenText Fortify Professional Services. OpenText Fortify Professional Services can assist with general usage questions, integration of the software into your processes, and implementing customizations, bug fixes, and feature requests (subject to feasibility analysis). Please contact your OpenText Sales representative or fill in the [Professional Services Contact Form](https://www.microfocus.com/en-us/cyberres/contact/professional-services) to obtain more information on pricing and the services that OpenText Fortify Professional Services can provide.

<!-- END-INCLUDE:h2.support.md -->


---

*[This document was auto-generated from README.template.md; do not edit by hand](https://github.com/fortify/shared-doc-resources/blob/main/USAGE.md)*

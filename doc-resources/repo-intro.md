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
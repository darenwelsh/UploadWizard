# UploadWizard
Enterprise fork of WMF UploadWizard


# LocalSettings.php mods
``` php
require_once $egExtensionLoader->registerLegacyExtension(
        'UploadWizard',
        'https://gerrit.wikimedia.org/r/mediawiki/extensions/UploadWizard',
        'REL1_25'
);

// Needed to make UploadWizard work in IE, see bug 39877
// See also: https://www.mediawiki.org/wiki/Manual:$wgApiFrameOptions
$wgApiFrameOptions = 'SAMEORIGIN';

// Use UploadWizard by default in navigation bar
$wgUploadNavigationUrl = "$wgScriptPath/index.php/Special:UploadWizard"; //Update with #156
$wgUploadWizardConfig = array(
        'debug' => false,
        'autoCategory' => 'Uploaded with UploadWizard',
        'feedbackPage' => 'FeedbackTest2',
        'altUploadForm' => 'Special:Upload',
        'fallbackToAltUploadForm' => false,
        'enableFormData' => true,  # Should FileAPI uploads be used on supported browsers?
        'enableMultipleFiles' => true,
        'enableMultiFileSelect' => true,
        'tutorial' => array('skip' => true),
        'fileExtensions' => $wgFileExtensions, //omitting this can cause errors
        'licensing' => array(
        //      'defaultType' => 'thirdparty',
                'ownWorkDefault' => 'own',
                //'ownWorkDefault' => 'notown',
                'ownWork' => array(
                    'type' => 'or',
                    'template' => 'self', // maybe this can be modified???
                    'licenses' => array(
                         'enterprise',
                    )
                ),
                'thirdParty' => array(
                        'type' => 'or',
                        'defaultLicense' => 'enterprise',
                        'licenseGroups' => array(
                                array(
                                        'head' => 'mwe-upwiz-license-enterprise-head',
                                        'licenses' => array(
                                                'enterprise',
                                        )
                                ),
                        ),
                ),
        ),

//      'minAuthorLength' => 0,
//      'minSourceLength' => 0,

);
```

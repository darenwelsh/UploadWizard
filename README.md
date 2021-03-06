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
                'ownWorkDefault' => 'own', //'notown',
                'ownWork' => array(
                    'type' => 'or',
                    'template' => 'licensing', // this adds a link to Template:Licensing to the file info page
                    'licenses' => array(
                         'generic',
                    )
                ),
                'thirdParty' => array(
                        'type' => 'or',
                        'defaultLicense' => 'generic',
                        'licenseGroups' => array(
                                array(
                                        'head' => 'mwe-upwiz-license-generic-head',
                                        'licenses' => array(
                                                'generic',
                                        )
                                ),
                        ),
                ),
        ),

);
```

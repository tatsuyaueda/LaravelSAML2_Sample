# Laravel SAML2 認証サンプル

1. git clone https://github.com/tatsuyaueda/LaravelSAML2_Sample.git
1. cd LaravelSAML2_Sample
1. cp .env.example .env
1. .env にデータベースの設定をする
1. php artisan key:generate
1. php artisan migrate
1. app/config/saml2_settings.php を作成
1. Laravelのユーザを登録
1. ブラウザで /saml2/login にアクセスすると、SAMLで認証が走ります。

## saml2_settings.php のサンプル
```
<?php

return $settings = array( 'useRoutes' => true,
    'routesPrefix' => '/saml2',
    'routesMiddleware' => ['saml'],
    'retrieveParametersFromServer' => false,
    'logoutRoute' => '/logout',
    'loginRoute' => '/home',
    'errorRoute' => '/error',
    'strict' => true, //@todo: make this depend on laravel config
    'debug' => true, //@todo: make this depend on laravel config
    'sp' => array(
        'NameIDFormat' => 'urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress',
        'x509cert' => 'foobar',
        'privateKey' => 'foobar',
    ),
    'idp' => array(
        'entityId' => 'https://openam.example.com/OpenAM',
        'singleSignOnService' => array(
            'url' => 'https://openam.example.com/OpenAM/SSORedirect/metaAlias/idp',
        ),
        'singleLogoutService' => array(
            'url' => 'https://openam.example.com/OpenAM/IDPSloRedirect/metaAlias/idp',
        ),
        'certFingerprint' => 'foobar',
    ),
    'security' => array(
        'nameIdEncrypted' => false,
        'authnRequestsSigned' => true,
        'logoutRequestSigned' => false,
        'logoutResponseSigned' => false,
        'signMetadata' => false,
        'wantMessagesSigned' => false,
        'wantAssertionsSigned' => false,
        'wantNameIdEncrypted' => false,
        'requestedAuthnContext' => true,
    ),
);
```

## License

The Laravel framework is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT).

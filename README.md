# Laravel Facebook Ads Mahen

> [Stable 1.0](https://github.com/edbizarro/laravel-facebook-ads/tree/1.0) version in progress

Get ads infos (campaigns, clicks, insights, cost , etc...) from Facebook ads API

 - Supported Facebook API version: 2.7

Support for version 2.8 will be avaliable with version 1.0

---
<p align="center">

![logo](laravel-facebook-ads.png)
</p>

<p align="center">

[![Build Status](https://semaphoreci.com/api/v1/edbizarro/laravel-facebook-ads/branches/master/badge.svg)](https://semaphoreci.com/edbizarro/laravel-facebook-ads)
[![Packagist](https://img.shields.io/packagist/v/edbizarro/laravel-facebook-ads.svg)](https://packagist.org/packages/edbizarro/laravel-facebook-ads) [![Code Climate](https://codeclimate.com/github/edbizarro/laravel-facebook-ads/badges/gpa.svg)](https://codeclimate.com/github/edbizarro/laravel-facebook-ads) [![Codacy Badge](https://api.codacy.com/project/badge/grade/d6deeeac233847dba57afb5c07ccad4b)](https://www.codacy.com/app/edbizarro/laravel-facebook-ads) [![StyleCI](https://styleci.io/repos/55666212/shield)](https://styleci.io/repos/55666212) [![SensioLabsInsight](https://insight.sensiolabs.com/projects/f5001994-d22b-45a1-aa50-d4ac356cd42f/mini.png)](https://insight.sensiolabs.com/projects/f5001994-d22b-45a1-aa50-d4ac356cd42f) [![Total Downloads](http://img.shields.io/packagist/dm/edbizarro/laravel-facebook-ads.svg)](https://packagist.org/packages/edbizarro/laravel-facebook-ads)

</p>

---

## Installation

Follow this steps to use this package on your Laravel installation

### 1. Require it on composer

```bash
composer require edbizarro/laravel-facebook-ads
```

### 2. Load service provider

You need to update your `config/app.php` configuration file to register our service provider, adding this line on `providers` array:

```php
Edbizarro\LaravelFacebookAds\Providers\LaravelFacebookServiceProvider::class
```

### 3. Enable the facade (optional)

This package comes with an facade to make the usage easier. To enable it, add this line at `config/app.php` on `alias` array:

```php
'FacebookAds' => Edbizarro\LaravelFacebookAds\Facades\FacebookAds::class
```

## Configuration

If you want to change any configurations, you need to publish the package configuration file. To do this, run `php artisan vendor:publish` on terminal.
This will publish a `facebook-ads.php` file on your configuration folder like this:

```php
<?php
return [
    'app_id' => env('FB_ADS_APP_ID'),
    'app_secret' => env('FB_ADS_APP_SECRET'),
];
```

Note that this file uses environment variables, it's a good practice put your secret keys on your `.env` file adding this lines on it:


```
FB_ADS_APP_ID="YOUR_APP_ID"
FB_ADS_APP_SECRET="YOUR_APP_SECRET_KEY"
```

## First steps

Before using it, it's necessary to initialize the library with an valid [access token](https://developers.facebook.com/docs/facebook-login/access-tokens#usertokens), [php example](https://github.com/facebook/facebook-php-sdk-v4#usage).

#### Example getting all ads

```php
<?php
/** Your controller */
namespace App\Http\Controllers;

use Edbizarro\LaravelFacebookAds\FacebookAds;

class ExampleController extends Controller
{
    public function __construct(FacebookAds $ads)
    {
      $adAccounts = $ads->adAccounts();

      $ads = $adAccounts->all(['name', 'id'])->map(function ($adAccount) {
          return $adAccount->ads(
              [
                  'name',
                  'account_id',
                  'account_status',
                  'balance',
                  'campaign',
                  'campaign_id',
                  'status'
              ]
          );
      });

      dd($ads);
    }
}
```

## Usage

To obtain a list of all available fields, look at [this](https://github.com/facebook/facebook-php-ads-sdk/blob/master/src/FacebookAds/Object/Fields/AdAccountFields.php).

To obtain a list of all available fields, look at [this](https://github.com/facebook/facebook-php-ads-sdk/blob/master/src/FacebookAds/Object/Fields/AdFields.php).


To obtain a list of all available fields, look at [this](https://github.com/facebook/facebook-php-ads-sdk/blob/master/src/FacebookAds/Object/Fields/CampaignFields.php).


To obtain a list of all available fields, look at [this](https://github.com/facebook/facebook-php-ads-sdk/blob/master/src/FacebookAds/Object/Fields/AdsInsightsFields.php).

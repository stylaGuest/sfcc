# Styla Salesforce Commerce Cloud Cartridge

This cartridge connects your Salesforce with [Styla](http://www.styla.com/) by embedding Styla content on a specific path. [This documentation page](https://docs.styla.com/) should provide you an overview of how Styla works in general. 

## Installation and Configuration

Please consult the [documentation](https://github.com/styladev/demandware/tree/master/documentation) folder for information on how to install and configure the cartridge. 

Please note that OCAPI needs to be configured for Styla to source product data and display products in your Content Hub(s) and enable adding them to your cart. This is also described in the documentation.


## SEO Content from Styla's SEO API

The cartridge uses data from Styla's SEO API to:
* generate tags like: meta tags including `<title>`, canonical link, og:tags, static content inserted into <body>, `robots` instructions
* insert these tags accordingly into HTML of the template the page with Styla content uses
  
This is done to provide search engine bots with data to crawl and index all Styal URLs, which are in fact a Single-Page-Application.

Once you install and configure the module, please open source of the page on which your Styla content is embedded and check if none of the tags mentioned below are duplicated. In case `robots`or `link rel="canonical"` or any other are in the HTML twice, make sure to remove the original ones coming from your default template. Otherwise search engine bots might not be able to crawl all the Styla content or crawl it incorrectly. 

You can find more information on the SEO API on [this page](https://docs.styla.com/seo-integration)

## Setup Process

The process of setting up your Content Hub(s) usually goes as follows:

1. Install and configure the cartridge on your stage using Content Hub IDs shared by Styla
2. Configure OCAPI on your stage
3. Share the stage URL, credentials and OCAPI endpoints with Styla, including URL parameters for different locales and currencies (if used by you)
4. Styla integrates product data from stage OCAPI, test your stage Content Hub and asks additional questions, if needed
5. Configure the cartridge and OCAPI on production, without linking to the Content Hub(s) there and, again, share the URL and OCAPI endpoints with Styla
6. Make sure your content is ready to go live
7. Styla conducts final User Acceptance Tests before the go live
8. Go live (you link to the Content Hub embedded on your production)

**Important: When updating from any previous version to 18.0.0 or higher, please let Styla know beforehand. Your settings need to be updated so that everything works fine.**

## Salesforce-certified and available on Marketplace

The latest version of this cartridge has been certified by Salesforce and can also be downloaded from its marketplace: https://xchange.demandware.com/docs/DOC-34370


## Solution in SFCC for linking to one page on multiple SFCC locales from Styla account embedded there

The below solution helps you if you use one Styla account on multiple locales, for instance:
yourname-en on yourdomain/gb/en/styla/ and yourdomain/de/en/styla/
Using this solution, you can use just one link on a given Styla page in both accounts and they will be routed by SFCC correctly. 

The solution below is provided by courtesy of NorthSails https://webstore.northsails.com 

The following DemandWare pipelines are being used to create the internal URL:
 - Page-Show (content pages / assets)
 - Search-Show (category pages / storefront)
In the DemandWare Business Manager, the content manager has to make the following changes:

1. Visit the path "Merchant Tools > SEO > URL Rules > Pipeline URLs"
2. Create an "alias" for the above pipeline URLs (could be already existing)
3. In our case:
 - "search" resolves To "Page-Show"
 - "page" resolves To "Search-Show"

After this has been set up, content or category pages can be accessed using:
 - Content page: `https://webstore.northsails.com/it/it/show/?cid=about` in which "about" can be replaced with the ID of the content asset ID.
 - Category page: `https://webstore.northsails.com/it/it/search/?cgid=featured-new-men` in which "featured-new-men" can be replaced with the ID of the catalog storefront category.

In our case we can use Styla's relative URL option to support our locales, using:
 - `../show/?cid=about`
 - `../search/?cgid=featured-new-men`



# Fooman EssentialCatalog 
## Extension for Magento 2.3+
The motivation behind this extension is the latest update to online trading regulations in New Zealand in response to the COVID-19 pandemic. As per the [government website](https://www.mbie.govt.nz/about/open-government-and-official-information/coronavirus-covid-19/essential-services/) as of 2020-04-03:

>1. Orders must be taken online or by phone only. Storefronts must not be open and the public should not be able to visit stores to select or collect goods.
>2. Orders must be for only essential non-food consumer products.
 In fulfilling orders, businesses must take all appropriate public health measures (e.g. physical distancing, hygiene basics, appropriate personal protective equipment for staff).
>3. Orders must be home delivered in a contactless way (i.e. there is no physical interaction between the deliverer and customer).
>4. The business must inform MBIE of its intention to offer essential non-food products for sale, and provide a list of the products they intend to offer. 

This extension adds the ability to classify a product as an Essential Product. And once enabled all simple, configurable or bundle products that aren't set as essential products would be out of stock products.

## Installation Instructions
### Easy option using the ExtDN Installer
Copy and paste the below command into the command line in your Magento root folder. The installation will proceed automatically from there:

```
sh -ic "$(curl -sS https://raw.githubusercontent.com/extdn/installer-m2/master/bin/oneliner.sh)" -- install fooman/essentialcatalog-m2:^1.0
```
### You install extensions all the time
This package is available via packagist.org. Please use Composer to install the extension

```
bin/magento deploy:mode:set developer (if you are in production mode)
composer require fooman/essentialcatalog-m2:^1.0
bin/magento module:enable --clear-static-content Fooman_EmailAttachments
bin/magento setup:upgrade

your usual sequence of commands to enable production mode, for example
bin/magento deploy:mode:set production
```

## How to use
Enable the setting "Restrict Catalog to Essential Products" under Stores > Configuration
![Stores > Configuration](docs/stores-configuration.png?raw=true")

Catalog > Inventory > Product Stock Options
![Restrict Catalog to Essential Products](docs/enable-restricted-catalog.png?raw=true")
The Magento Cache would need to get refreshed after making a change.

Then set the product as essential or not. The value "Use Config" would indicate no decision yet applied and the product would not change it's stock status. Details on what is deemed essential or not (for New Zealand) can also be found on this [page](https://www.mbie.govt.nz/about/open-government-and-official-information/coronavirus-covid-19/essential-services/).
![Essential Products](docs/essential-product.png?raw=true")

Alternatively you may wish to export and then re-import your complete catalog to a csv file and set the attribute `fooman_is_product_essential` to
* 0 for not essential
* 1 for essential

## Developer Note - Depending on EssentialCatalog
If you are using EssentialCatalog to build functionality on top of please require the implementation package
`composer require essentialcatalog-implementation-m2` instead as only that package will be semantically versioned.
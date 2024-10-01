# Theme Installation

Before applying our theme package, we strongly recommend implementing it on a development server. Please ensure you back up your Magento files and database. We cannot be held responsible for any data loss.


#### Install the theme package using the composer command given below:

### M2.4.6
```bash
  composer require viraxpress/frontend=1.0.5
```
### M2.4.7
```bash
  composer require viraxpress/frontend=2.0.1
```
### Composer Update
```bash
  composer require viraxpress/frontend=x.x.x -W
```

Manually edit the composer.json file in the Magento root directory and include the entries under the psr-4 section, as shown in the example below.
<p><img src="https://demo.viraxpress.com/vx/ViraXpress/frontend/web/wysiwyg/VX-psr-4.png"></p>

```bash
"ViraXpress\\Catalog\\": "vendor/viraxpress/catalog/",
"ViraXpress\\Cms\\": "vendor/viraxpress/cms/",
"ViraXpress\\Checkout\\": "vendor/viraxpress/checkout/",
"ViraXpress\\ConfigurableProduct\\": "vendor/viraxpress/configurable-product/",
"ViraXpress\\Configuration\\": "vendor/viraxpress/configuration/",
"ViraXpress\\Customer\\": "vendor/viraxpress/customer/",
"ViraXpress\\Framework\\": "vendor/viraxpress/framework/",
"ViraXpress\\Newsletter\\": "vendor/viraxpress/newsletter/",
"ViraXpress\\Sales\\": "vendor/viraxpress/sales/",
"ViraXpress\\Store\\": "vendor/viraxpress/store/",
"ViraXpress\\Swatches\\": "vendor/viraxpress/swatches/",
"ViraXpress\\Theme\\": "vendor/viraxpress/theme/",
"ViraXpress\\Widget\\": "vendor/viraxpress/widget/",
"ViraXpress\\Wishlist\\": "vendor/viraxpress/wishlist/"
```


Run the below magento commands

```bash
  composer clearcache
  composer dumpautoload
  php bin/magento setup:upgrade
  php bin/magento setup:di:compile
  php bin/magento setup:static-content:deploy -f
  php bin/magento c:c
  php bin/magento c:f
```

- Assign ViraXpress as your frontend theme for your website or store from the admin panel.

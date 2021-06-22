# Vue Storefront AEM Integration Examples

This repository demonstrates how to use the Vue Storefront AEM integration with these examples:

* Render a [Hero](https://docs.storefrontui.io/?path=/docs/components-organisms-hero--common) with Content Fragment data coming from AEM.
* Render a [Carousel](https://docs.storefrontui.io/?path=/docs/components-organisms-carousel--common) with a list of Magento products defined in a Content Fragment (via CIF).

We're using Magento in this example but the AEM integration works independently from whatever commerce engine you're using.
Just note that filtering by SKU might be different for other integrations (see `productCarouselSearchMagento` in `Home.vue`).

## Setup

### Prerequisites

* Java 11+
* Maven
* A running Magento 2.4.2 instance

### AEM

1. Start an Author and Publish instance using the AEMaaCS SDK.
    * The Author is only required if you want to change any of the CFM data or models.
    * You'll also need the "AEM CIF Add-On" installed in Author if you want to change the CFM data for the product carousel.
      See [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/storefront/developing/develop.html) for more information.

2. Download the "GraphQL Endpoint Content Package" package from the Software Distribution portal and install it on both instances.
    * You may also want to download the "GraphiQL Content Package" and install it on Author so that you can test GraphQL queries.

3. In `aem/config/src/main/content/jcr_root/apps/vsf-aem-demo/config/com.adobe.cq.cif.proxy.GraphQLProxyServlet.cfg.json` update the `graphQLOriginUrl` to point to your Magento instance.

4. In `aem/content/src/main/content/jcr_root/content/dam/vsf-aem-demo/homepage-product-carousel/.content.xml` update the SKUs in the `products="[...]` property to match your Magento catalog. (You can also do this via your Author instance after the initial build.)

5. Build the packages in `aem` using `mvn clean install -PautoInstallPackage` (for Author) and `mvn clean install -PautoInstallPackagePublish` (for Publish).


### Vue Storefront

1. Follow the VSF installation instructions [here](https://docs.vuestorefront.io/v2/general/installation.html#prerequisites) and select "Magento 2" as the commerce integration.

2. Follow the instructions in the VSF README.md to connect VSF to your Magento instance. Confirm that your localhost loads fine.
   See [here](https://docs.vuestorefront.io/v1/guide/installation/magento.html) for more information.

3. Follow the setup instructions in the `@bounteous/vue-storefront-aem` README to install the VSF AEM integration.

4. Replace the file `pages/Home.vue` in the VSF codebase with the `vsf/Home.vue` file provided in this repository. It contains the two examples mentioned above.

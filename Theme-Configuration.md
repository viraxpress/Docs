### Theme Configuration

- Go to Admin > Stores > Configuration  > ViraXpress > ViraXpress Configuration.

## General tab:
<p><img src="https://demo.viraxpress.com/vx/ViraXpress/frontend/web/wysiwyg/VX-st1.png"></p>

- **Enable ViraXpress:** Set “Yes” to use ViraXpress.
- **Server npm node path:** In the terminal command line, go to the magento root path and enter "which npm", to update the server npm node path. Which is used to update the tailwind css for cms page and block. Kindly refer the screenshot for your reference.

## Checkout Theme Switcher:
<p><img src="https://demo.viraxpress.com/vx/ViraXpress/frontend/web/wysiwyg/VX-st2.png"></p>

- **Checkout Controllers:** Pre-filled value for the controllers and that can load based on the below chosen theme.
- **Theme:** Select the theme that you want to apply for the above checkout controller’s.

## Catalog Product Image Resize:
<p><img src="https://demo.viraxpress.com/vx/ViraXpress/frontend/web/wysiwyg/VX-st3.png"></p>
<p><img src="https://demo.viraxpress.com/vx/ViraXpress/frontend/web/wysiwyg/VX-st4.png"></p>

- **Product List View:** Enter the value of the image width and height as px for PLP.
- **Product Grid View:** Enter the value of the image width and height as px for PLP.
- **Product Detail Page:** Enter the value of the image width and height as px for PDP.
- **Product Widget Carousel/Grid:** Enter the value of the image width and height as px for the widget.
- **Related Products, Up-Sells and Cross-Sells:** Enter the value of the image width and height as px.

## Colors:
<p><img src="https://demo.viraxpress.com/vx/ViraXpress/frontend/web/wysiwyg/VX-st5.png"></p>

- **Primary Color:** Enter the value that you want to apply the color for the overall website.
- If you are facing any nodejs issue while saving the configuration. kindly refer the below link (https://github.com/viraxpress/Documentation/blob/main/Theme-configuration.md#resolving-configuration-save-conflicts-for-tailwind)

## Header:
<p><img src="https://demo.viraxpress.com/vx/ViraXpress/frontend/web/wysiwyg/VX-st6.png"></p>

- **Enable Sticky Header:** Enable or disable sticky header at frontend.
- **Top Static Block ID:** Enter the Block Id to display the announcement content at the top of header.

## Footer:
<p><img src="https://demo.viraxpress.com/vx/ViraXpress/frontend/web/wysiwyg/VX-st7.png"></p>

- **Footer Description Text:** Enter the content that you want to display in the footer.
- **Footer Static Links Block ID:** Enter the block ID for the footer static links.
- **Footer Extra Info Block ID:** Enter the block ID to display the extra info or app logo in the footer.
- **Enable Footer Social Links:** set “yes” to display the social links in the footer.
- **Footer Social Links:** click add button to choose the social media and enter the url for it.


## Resolving Configuration Save Conflicts For Tailwind:

If you encounter conflicts while saving configurations or CMS pages and blocks, follow these steps to troubleshoot the issue:

- **Check Node.js Version:** Open your terminal and check your current Node.js version.
- **Use a PHP Script for Verification:** Create a simple PHP script to check the Node.js version. This script can execute a command in the terminal and display the current version.
- **Compare Versions:** Ensure that the Node.js version matches the required version for your application. If there is a discrepancy, proceed to uninstall Node.js completely from your system.
- **Uninstall Node.js:** Use the appropriate method for your operating system to remove Node.js entirely.
- **Reinstall Node.js:** Download the correct version of Node.js from the official website or use a package manager to install the appropriate version for your system. kindly use Option 2 from the below link
    - https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04#option-2-installing-node-js-with-apt-using-a-nodesource-ppa
- **Verify the Installation:** After reinstalling, confirm the installation by checking the Node.js version again.
- **Retry Saving Configurations:** Restart your application and attempt to save your configurations, CMS pages, or blocks again.

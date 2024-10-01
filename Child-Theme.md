
# Steps to Create ViraXpress Child Theme:

Creating a child theme allows you to extend and customize a parent theme without altering its core files, ensuring your modifications remain intact during theme updates. Follow these steps to set up a child theme:


## Step 1: Create Theme Directory

- Navigate to app/design/frontend/ and create a directory for your child theme: app/design/frontend/VendorName/ChildTheme.

## Step 2: Create the theme.xml File

- Create the file theme.xml to define the parent theme and theme information.
- Note: if you are importing a preview image create the media folder and import preview image.

```bash
<theme xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Config/etc/theme.xsd">
    <title>Child Theme</title> <!-- Child Theme Name -->
    <parent>ParentThemeVendor/ParentTheme</parent> <!-- Parent Theme -->
    <media>
        <preview_image>media/preview.jpg</preview_image> <!-- Preview Image (optional) -->
    </media>
</theme>
```

## Step 3: Create the registration.php File

- The registration.php file is essential for registering the theme within Magento.
- Include the following PHP code to register the theme using the standard approach:

```bash
<?php
\Magento\Framework\Component\ComponentRegistrar::register(
    \Magento\Framework\Component\ComponentRegistrar::THEME,
    'frontend/VendorName/ChildTheme',
    __DIR__
);
```

## Step 4: Override or Extend Files

- Now you can begin overriding or extending files in your child theme:
  - Templates: Place them in ChildTheme/Magento_Theme/templates/.
  - Layouts: Override layout files in ChildTheme/Magento_Theme/layout/.

## Step 5: Activate the Child Theme

- After creating the child theme files, activate the theme through the Magento Admin panel.
- Navigate to Admin Panel → Content → Design → Configuration, then set the Child Theme as the active theme for your store view.


## Step 6: Upgrade and Deploy Static Content

- To fully activate your child theme, you need to deploy the static content, which generates the necessary CSS, JavaScript, and image files for the theme.
- It's recommended to back up the pub/static folder to avoid losing any custom static files (optional but suggested).
- Once the theme is configured, run the following commands:

    ```bash
    bin/magento setup:upgrade
    bin/magento setup:static-content:deploy
    ```

## Step 7: Tailwind Configuration

- To apply style changes to your child theme, navigate to the pub/vx/VendorName/ChildTheme/web/tailwind/ directory and add your custom styles to the tailwind.css file and run the necessary command to compile your Tailwind utility classes into standard CSS.
- If you prefer to create a separate file for a component or block, place your .css file in the pub/vx/ViraXpress/frontend/web/tailwind/vx-components folder and import it at the top of the tailwind.css file like this:

    ```bash
    @import "vx-components/your-style.css";
    ```


Note: For compiling the Tailwind CSS: you need to run the tailwind command(npm run dev/prod) under the following directory pub/vx/VendorName/ChildTheme/web/tailwind/.

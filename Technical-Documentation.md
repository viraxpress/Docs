### Technical Documentation

# Magento_Directory:

##### File Path:

- Magento_Directory/templates/currency.phtml

##### Overview:

- This customization modifies the default Magento 2 currency switcher, enhancing it with Alpine.js for better interaction and responsiveness. It replaces Magento's default dropdown behavior with a more modern, interactive UI.

##### Changes Summary:

- The default Magento template uses jQuery (data-mage-init) to handle dropdown and currency selection functionality.
- The customized template replaces this with Alpine.js (x-data, x-show, @click, etc.), allowing a more interactive experience and eliminating the dependency on Magento's jQuery-based dropdown system.
- The custom code introduces Tailwind CSS for styling and ensures the switcher is mobile-responsive by using dynamic classes like min-h-[28px] and w-full.
- Kindly refer the below screenshot for the difference between vendor currency template file and customized template file

##### Vendor Core Template:
<p><img src="https://demo.viraxpress.com/vx/ViraXpress/frontend/web/wysiwyg/VX-cd.png"></p>

```bash
<?php if ($block->getCurrencyCount() > 1) : ?>
  <?php $currencies = $block->getCurrencies(); ?>
  <?php $currentCurrencyCode = $block->getCurrentCurrencyCode(); ?>
  <?php $id = $block->getIdModifier() ? '-' . $block->getIdModifier() : '' ?>
  <div class="switcher currency switcher-currency" id="switcher-currency<?= $block->escapeHtmlAttr($id) ?>">
      <strong class="label switcher-label"><span><?= $block->escapeHtml(__('Currency')) ?></span></strong>
      <div class="actions dropdown options switcher-options">
          <div class="action toggle switcher-trigger"
               id="switcher-currency-trigger<?= $block->escapeHtmlAttr($id) ?>"
               data-mage-init='{"dropdown":{}}'
               data-toggle="dropdown"
               data-trigger-keypress-button="true">
              <strong class="language-<?= $block->escapeHtml($block->getCurrentCurrencyCode()) ?>">
                  <span><?= $block->escapeHtml($currentCurrencyCode) ?> - <?= $currencies[$currentCurrencyCode] ? $block->escapeHtml($currencies[$currentCurrencyCode]) : '' ?></span>
              </strong>
          </div>
          <ul class="dropdown switcher-dropdown" data-target="dropdown">
              <?php foreach ($currencies as $_code => $_name) : ?>
                  <?php if ($_code != $currentCurrencyCode) : ?>
                      <li class="currency-<?= $block->escapeHtmlAttr($_code) ?> switcher-option">
                          <a href="#" data-post='<?= /* @noEscape */ $block->getSwitchCurrencyPostData($_code) ?>'><?= $block->escapeHtml($_code) ?> - <?= $block->escapeHtml($_name) ?></a>
                      </li>
                  <?php endif; ?>
              <?php endforeach; ?>
          </ul>
      </div>
  </div>
<?php endif; ?>
```

##### Customized VX Template:
<p><img src="https://demo.viraxpress.com/vx/ViraXpress/frontend/web/wysiwyg/VX-cust.png"></p>

```bash
<?php if ($block->getCurrencyCount() > 1): ?>
<div class="relative w-full lg:w-max min-h-[28px]" x-data="currencySwitcher('<?= $escaper->escapeHtml($currentCurrencyCode) ?> - <?= $currencies[$currentCurrencyCode] ? $escaper->escapeHtml($currencies[$currentCurrencyCode]) : '' ?>')">
    <button type="button" @click="isCurrencySwitcher = !isCurrencySwitcher" class="w-full relative cursor-pointer font-medium rounded pl-5 py-3 lg:text-sm lg:py-0 lg:pl-3 pr-10 text-left text-gray-900 lg:text-white sm:leading-6" :aria-haspopup="isCurrencySwitcher" :aria-expanded="isCurrencySwitcher" aria-labelledby="listbox-label">
        <span class="min-h-[20px] inline-block" x-text="selectedCurrency"></span>
        <?php if (!empty($currencies)) { ?>
            <span class="pointer-events-none absolute z-10 inset-y-0 right-0 ml-3 flex items-center pr-2">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="h-4 w-4 text-gray-900 lg:text-white">
                    <path stroke-linecap="round" stroke-linejoin="round" d="m19.5 8.25-7.5 7.5-7.5-7.5" />
                </svg>
            </span>
        <?php } ?>
    </button>
    <?php if (!empty($currencies)) { ?>
        <ul x-cloak x-show="isCurrencySwitcher" x-transition:leave="transition ease-in duration-100" x-transition:leave-start="opacity-100" x-transition:leave-end="opacity-0" @click.away="isCurrencySwitcher = false" class="absolute z-[500] right-0 top-full w-full lg:w-max rounded p-2 bg-white origin-top-right rounded-md bg-white shadow-lg focus:outline-none ring-1 ring-black ring-opacity-5 focus:outline-none" tabindex="-1" role="listbox" aria-labelledby="listbox-label" aria-activedescendant="listbox-option-3">
            <?php foreach ($currencies as $_code => $_name): ?>
                <?php if ($_code != $currentCurrencyCode): ?>
                    <?php $selectedCurrency = $_code; ?>
                    <li class="currency-<?= $escaper->escapeHtmlAttr($_code) ?> switcher-option">
                        <a href="javascript:void(0)" @click="changeCurrency('<?= $escaper->escapeUrl($block->getUrl('directory/currency/switch', ['currency' => $escaper->escapeJs($selectedCurrency)])) ?>')" id="currency" name="currency" class="text-gray-700 font-medium block p-2 rounded text-sm capitalize hover:bg-gray-100 focus:bg-primary focus:text-white"><?= $escaper->escapeHtml($_code) ?> - <?= $escaper->escapeHtml($_name) ?></a>
                    </li>
                <?php endif; ?>
            <?php endforeach; ?>
        </ul>
    <?php } ?>
</div>
<?php endif; ?>
```


# Magento_Customer:

##### File Path:

- Magento_Customer/templates/address/edit.phtml

##### Overview:

- This customization enhances the Magento 2 default country and region form fields by incorporating Alpine.js to dynamically manage the state/province field based on the selected country. It replaces the default Magento HTML select functionality with a more interactive and responsive design.

##### Vendor Core Template:

- The vendor code uses Magento’s built-in block method $block->getCountryHtmlSelect() to generate the country select element.
- It does not dynamically fetch regions based on country selection, and all logic is handled server-side.

##### Customized VX Template:
- Alpine.js Integration:
    - Alpine.js is used to handle country selection and dynamically load the regions based on the selected country.
    - The custom addressEditCountryRegion function manages the state by fetching available regions via AJAX using the onCountryChange() method.

- Dynamic Country & Region Selection:
    - Country Field:
      - Displays a dropdown for selecting the country.
      - An event listener (@change="onCountryChange") is attached to handle country changes and trigger the fetching of regions.

    - Region Field:
      - If regions are available for the selected country, a dropdown list is displayed.
      - If no regions are available, a text input field is shown instead.

- Styling with Tailwind CSS:
    - Tailwind CSS is used for styling, providing responsive and modern UI elements, such as rounded borders (rounded-md), focus effects (focus:ring-primary), and input styling (text-gray-900).

- AJAX Request:
    - The template makes an AJAX request to the server (/viraxpresscustomer/address/state) to fetch available regions when the country is changed.
    - If regions exist, they are populated into the dropdown. If not, a text input field is shown for manual entry.

Kindly refer the below screenshot for the difference between vendor currency template file and customized template file


##### Vendor Core Template:
<p><img src="https://demo.viraxpress.com/vx/ViraXpress/frontend/web/wysiwyg/VX-ven.png"></p>

```bash
<div class="field country required">
    <label class="label" for="country">
        <span><?= /* @noEscape */ $block->getAttributeData()->getFrontendLabel('country_id') ?></span>
    </label>
    <div class="control">
        <?= $block->getCountryHtmlSelect() ?>
    </div>
</div>
```

##### Customized VX Template:
<p><img src="https://demo.viraxpress.com/vx/ViraXpress/frontend/web/wysiwyg/VX-custo.png"></p>

```bash
<div x-data="addressEditCountryRegion" class="space-y-5">
    <div class="col-span-2 sm:col-span-1">
        <?php $countries = $block->getCountryCollection()->setForegroundCountries($directoryViewModel->getTopCountryCodes())->toOptionArray(); ?>
        <div class="field">
            <label for="country" class="block text-sm leading-6 text-gray-900">
                <?= $escaper->escapeHtml(__('Country  ')) ?><span class="text-required ml-1">*</span>
            </label>
            <div class="mt-1 control">
                <select id="country" @change="onCountryChange" x-on:input.debounce="onChange" required
                name="country_id" title="Country"
                class="block w-full rounded-md border-0 py-2.5 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-primary sm:text-sm sm:leading-6">
                    <?php foreach ($countries as $country): ?>
                        <option name="<?=/** @noEscape */ $country['label'] ?>"
                        value="<?= /** @noEscape */ $country['value'] ?>" <?= ($block->getCountryId() ===  $country['value']) ? 'selected="selected"' : '' ?>>
                            <?= /** @noEscape */ $country['label'] ?>
                        </option>
                    <?php endforeach; ?>
                </select>
            </div>
        </div>
    </div>
    <div class="col-span-2 sm:col-span-1">
        <div class="field">
            <label for="region_id" class="block text-sm leading-6 text-gray-900">
                <?= $escaper->escapeHtml(__('State/Province ')) ?>
                <span class="text-required ml-1">*</span>
            </label>
            <div class="mt-1 control" id="field_region_id">
                <template x-if="isRegionAvailable">
                    <select id="region_id" title="State/Province" name="region_id" required=""
                    x-on:input.debounce="onChange"
                    class="block w-full rounded-md border-0 py-2.5 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-primary sm:text-sm sm:leading-6 region_id validate-select">
                        <option value="">Please select a region, state or province.</option>
                        <template x-for="(region, key) in regionArray" :key="key">
                            <option :value="key" x-text="region"
                            :selected="region === '<?= $escaper->escapeHtmlAttr($block->getRegion()) ?>'"></option>
                        </template>
                    </select>
                </template>
                <template x-if="!isRegionAvailable">
                    <input id="region" required="" name="region" x-on:input.debounce="onChange"
                    value="<?= $escaper->escapeHtmlAttr($block->getRegion()) ?>"
                    class="form-input validate-not-number-first block w-full rounded-md border-0 py-2.5 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-primary sm:text-sm sm:leading-6">
                </template>
            </div>
        </div>
    </div>
</div>
```

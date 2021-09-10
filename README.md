# Xigen Add To Cart Helper

Shortcurt to build add to cart parameters without having worry about template block inheritence

![phpcs](https://github.com/DominicWatts/AddToCart/workflows/phpcs/badge.svg)

![PHPCompatibility](https://github.com/DominicWatts/AddToCart/workflows/PHPCompatibility/badge.svg)

![PHPStan](https://github.com/DominicWatts/AddToCart/workflows/PHPStan/badge.svg)

![php-cs-fixer](https://github.com/DominicWatts/AddToCart/workflows/php-cs-fixer/badge.svg)

## Install instructions

    composer require dominicwatts/addtocart

    php bin/magento setup:upgrade

    php bin/magento setup:di:compile

## Usage instructions

```
$xigenHelper = $this->helper(Xigen\AddToCart\Helper\AddToCart::class);
```

```
$postParams = $xigenHelper->getAddToCartPostParams($_item);
```

Then pthml as normal e.g.

```
<form data-role="tocart-form"
      data-product-sku="<?= $_item->getSku() ?>"
      action="<?= /* @noEscape */ $postParams['action'] ?>"
      method="post">
    <input type="hidden"
           name="product"
           value="<?= /* @noEscape */ $postParams['data']['product'] ?>">
    <?= $block->getBlockHtml('formkey') ?>
    <input type="number"
           name="qty"
           id="qty-<?= $_item->getSku() ?>"
           maxlength="12"
           value="1"
           title="<?php /* @escapeNotVerified */ echo __('Qty') ?>" 
           class="input-text qty form-control" />
    <button type="submit"
            title="<?= /* @noEscape */ __('Add to Basket') ?>"
            class="action tocart primary btn btn-primary">
        <span class="d-none d-lg-inline"><?= /* @noEscape */ __('Add to Basket') ?></span>
        <span class="d-lg-none"><?= /* @noEscape */ __('Add') ?></span>
    </button>
</form>
```

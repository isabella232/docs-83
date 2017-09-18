---
layout: default
title: {{ site.name }}
---

# Templates
Apple has created a set of TVML templates that can be used to create content pages. Each template produces a unique, full-screen display of information. You modify a page by adding or removing elements from a template. For a list of Apple-supplied TVML templates and elements, see [Apple TV Markup Language Reference](https://developer.apple.com/library/tvos/documentation/LanguagesUtilities/Conceptual/ATV_Template_Guide/TextboxTemplate.html#//apple_ref/doc/uid/TP40015064-CH2-SW8).

To create We.Retail ATV we require 5 templates. One template used as the home page, 3 templates for the e-commerce pages (Catalog, Section and Product) and one more template for the cart. We choose the Apple templates that we thought did the best job displaying the content required on each page.

## <a name="home" class="anchor">Home</a>
For the home page we choose the stack template. This template can be used to display groups of products such as displaying different categories of products. Each group of products is displayed directly underneath the previous group. Products can be displayed in different ways using carousel, grid, and shelf elements. 

TVML Template: [Stack Template](https://developer.apple.com/library/tvos/documentation/LanguagesUtilities/Conceptual/ATV_Template_Guide/StackTemplate.html#//apple_ref/doc/uid/TP40015064-CH21-SW4)
![Alt text](images/ATV_stack_template.png)

### AEM Features

Inside of AEM this template has one parsys which allows it to be fully customizable by the author. The author can drag on as many [catalog](components.html#catalog), [product](components.html#productShelf), [mBox](components.html#target), or [carousel](components.html#carousel) shelf components as they wish.

![Alt text](images/home-template.png)

## <a name="catalog" class="anchor">Catalog</a>
The catalog pages uses the showcase template. The showcase template can be used to display a row of images with descriptions associated with each image; for instance, for displaying a set of sections in the catalog. Users can scroll between images. When an image comes into focus, the size of the image is increased to be slightly larger than the other images. 

TVML Template: [Showcase Template](https://developer.apple.com/library/tvos/documentation/LanguagesUtilities/Conceptual/ATV_Template_Guide/ShowcaseTemplate.html#//apple_ref/doc/uid/TP40015064-CH27-SW1) (Catalog Page)
![Alt text](images/ATV_showcase_template.png)

### AEM Features
The primary content on these pages (the sections) are created automatically. This template will loop over the sections in the catalog and display each one on the shelf in the showcase template. Apple doesn't allow much more customization than that. <span style="color:purple">By default the template will look for a banner node under a section node on catalog page for a background image to use</span>. 

<span style="color:red">Authors can also customize the page further by changing the background image or adding music to be played when the page loads. This can be set up in the page properties under the catalog page tab.</span>

![Alt text](images/catalog-template.png)

## <a name="section" class="anchor">Section</a>
The section pages use the product bundle template. The product bundle template can be used to display detailed information about a product bundle; in our case, a catalog section. General information about the section is displayed in the top two-thirds of the screen with a row of related items, such as the products within the section, directly below. 

TVML Template: [Product Bundle Template](https://developer.apple.com/library/tvos/documentation/LanguagesUtilities/Conceptual/ATV_Template_Guide/ProductBundleTemplate.html#//apple_ref/doc/uid/TP40015064-CH38-SW1) (Section Page)
![Alt text](images/ATV_productBundle_template.png)

### AEM Features
Most of the content such as the section title and description is pulled from the section page node in the JCR. The template will loop over all child product pages in the section and display each one in the row of related items.

<span style="color:red">Authors can also customize the page by changing the background image from the default section image.</span> Section pages can also be configured to display and play videos using the Adobe PrimeTime Player. Both the background image and the video are configured in the page properties under the section tab.

![Alt text](images/section_page_properties.png)

At the bottom of the page is a parsys where authors can drag on as many [catalog](components.html#catalog), [product](components.html#productShelf), [mBox](components.html#target), or [carousel](components.html#carousel) shelf components as they wish.

![Alt text](images/section-template.png)

## <a name="product" class="anchor">Product</a>
The product pages uses the product template. The product template can be used to display detailed information about a product. The page displays general information about the product and is visible in the top two-thirds of the screen with a row of related products directly below. The user can scroll down and access detailed information about the product, including critical reviews.

TVML Template: [Product Template](https://developer.apple.com/library/tvos/documentation/LanguagesUtilities/Conceptual/ATV_Template_Guide/ProductTemplate.html#//apple_ref/doc/uid/TP40015064-CH8-SW4) (Product Page)
![Alt text](images/ATV_product_template.png)

### AEM Features
Product information is pulled from the e-commerce system and rendered in the template automatically. The template is also setup to interface with the shopping cart and users can add the product to their shopping cart. 

By default the 1st shelf area below the product information is populated with the other products in the same section as the current product. For example, if you are looking at a product page for a bike, all the products in the parent section "Biking" are displayed below the product information. 

<span style="color:red">The first shelf below the fold will render out any product reviews that exist for that product.</span>

At the bottom of the page is a parsys where authors can drag on as many [catalog](components.html#catalog), [product](components.html#productShelf), [mBox](components.html#target), or [carousel](components.html#carousel) shelf components as they wish.

![Alt text](images/product-template.png)

## <a name="cart" class="anchor">Cart</a>
The cart page uses the compilation template. This template was created to display information about one product that is made up of several distinct pieces; for example, an album and all of the songs that it contains. In our case, the page represents a shopping cart that contains multiple products.

TVML Template: [Compilation Template](https://developer.apple.com/library/tvos/documentation/LanguagesUtilities/Conceptual/ATV_Template_Guide/CompilationTemplate.html#//apple_ref/doc/uid/TP40015064-CH36-SW2) (Cart Page)
![Alt text](images/ATV_compilation_template.png)

### AEM Features
<span style="color:red">The contents of the page are automatically populated with the contents of the user's shopping cart. The subtotal, total, and other shopping cart information is displayed in the header area. The user can also highlight each item in the cart and remove them.</span>

![Alt text](images/cart-template.png)
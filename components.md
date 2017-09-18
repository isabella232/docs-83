---
layout: default
title: {{ site.name }}
---

# Components

## <a name="carousel" class="anchor">Carousel</a>
The carousel element displays images in a row that the user can navigate by swiping left and right on the remote.

![Alt text](images/carousel.png)

### Configuration

Images can be added by opening the configuration dialog and clicking the add field button.

* <b>Image Path:</b> Path to image in DAM.
* <b>Link To:</b> Path selecting the image to be linked.
* <b>Banner Title:</b> Heading overlaid at the bottom of the banner (optional).

![Alt text](images/carousel_settings.png)

## <a name="catalogShelf" class="anchor">Catalog Shelf</a>
The catalog shelf component displays catalog or section elements horizontally. If the contained elements cannot fit on the screen, users can navigate left and right to show more elements.

![Alt text](images/catalogShelf.png)

### Configuration

The catalog shelf can display any set of catalog or section pages. To configure the shelf, open up the components configuration dialog and under "Parent Page" select a parent with either catalogs or sections as its children. The component will loop over all children of the parent. 

By default, this component will look for a node at the path "section/banner" under each child page. This banner node should have a property called fileReference that contains the path to the image used for this child catalog or section.

![Alt text](images/catalog_shelf_settings.png)


## <a name="productShelf" class="anchor">Product Shelf</a>
The product shelf component displays product elements horizontally. If the contained products cannot fit on the screen, users can navigate left and right to show more elements.

![Alt text](images/productShelf.png)

### Configuration

Products can be added to the product shelf by simply dragging them onto the component from the asset finder.


## <a name="productGrid" class="anchor">Product Grid</a>
The product grid will layout elements in a grid pattern. Products inside of the grid are displayed in a row bound by the size of the screen. Items are automatically moved to another row once a row is filled.

![Alt text](images/productGrid.png)

### Configuration

Products can be added to the product grid by simply dragging them onto the component from the asset finder.


## <a name="target" class="anchor">mBox Shelf</a>
The mBox shelf is used to display A/B tests from Adobe Target. More information on this component can be found on the [Adobe Target Integration](target.html) page.

![Alt text](images/target.png)

### Configuration

A/B tests can be set up by opening the configuration dialog and entering the following fields.

* <b>mBox Id:</b> Id of mBox
* <b>Target Page:</b> Target page to be presented if the user selects the A/B test (Optional)

![Alt text](images/target_settings.png)


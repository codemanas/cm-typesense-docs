# Introduction #

Typsense Search for WooCommerce is a premimum addon that provides robust, fast search functionality for WooCommerce products on your website. 

## Features 

* Lightning-fast products search results in miliseconds
* Allow to override WooCommerce product search
* Allow to hijack WooCommerce shop and archive pages
* Provides result in WooCommerce default HTML structure
* Provides all the features for search and filter provided by WooCommerce but in a better and fast way
* Provides shortcodes for adding search in only specific locations.
* Hooks and filters for customizations
* Template Override for design customizations.


## Minimum Requirements

* PHP 7.4 required or greater
* MySQL 5.6 or greater is recommended
* <a href="https://wordpress.org/plugins/search-with-typesense/" target="_blank" rel="no-opener no-follow" >Search with Typsense</a>
* <a href="https://wordpress.org/plugins/woocommerce/" target="_blank" rel="no-opener no-follow" >WooCommerce</a>
---

## Installation
1. After purchasing from [Codemanas](https://codemanas.com/), download the zip file
1. Then on your site's dashboard, go to WordPress Plugins > Add New Search for "Search with Typesense"
2. Click Install and then activate Plugin 
---


## Getting started

### Activate License
After activating the plugin, go to **Typesense->Addons**, then put the license and activate it.

### Indexing products

Then go to **Typsense->Typesense**, 

license page
search post type and index
by default options
backend setting
customizer setting
shortcodes

## Adding custom taxonomy as filters

### Use Case:
Suppose you want to add tags ( or any other custom taxonomy ) filter to the shop/archive page other than the default ones provided by the addon. 

### How to do it:

#### Add field to the schema: 

First you need to add your field to the `$product_fields` array which is added to the schema using the filter `cm_tsfwc_product_fields` like this:

```
add_filter( 'cm_tsfwc_product_fields', function( $product_fields ) {
	$product_fields[] = [ 'name' => 'tags', 'type' => 'string[]', 'facet' => true ];

	return $product_fields;
} );

```

***Note: While adding new field to schema only the `name` should be different. `type` should be `string[]` and `facet` should always be `true` ***



#### Update the document data to be indexed

After you have added the field, data for the field should be provided using the filter `cm_tsfwc_data_before_entry` like below:

```
add_filter( 'cm_tsfwc_data_before_entry', function( $formatted_data, $raw_data, $object_id, $schema_name ) {

	if( $schema_name === 'product' ) { // only add data if the schema is product 

		$product_tags = get_the_terms( $object_id, 'product_tag' );

		$product_tags_arr = [];

		if( ! is_wp_error( $product_tags ) ) {
			foreach( $product_tags as $product_tag ) {
				$product_tags_arr[] = $product_tag->name;
			}
		} else {
			$product_tags_arr = []; // Only array can be pushed to the data. When no data, empty array is the must
		}

		$formatted_data['tags'] = $product_tags_arr;
	}

	return $formatted_data;

}, 10, 4 );

```

***Note: The index for the `$formatted_data` should be same as name of the field added before. For example: name of the field added before is `'tags'` so the index for the `$formatted_data` is also `tags`. ***

***Important: After changing the schema, collection should be deleted and reindexed to work properly.***

### Displaying the filter

To display the filter on the frontend, use the action `cm_tsfwc_custom_attributes` like below:


```
add_action( 'cm_tsfwc_custom_attributes', function() {
	echo '<div data-facet_name="tags" data-title ="' . __( "Filter by Tags", 'storefront' ) . '" class="cm-tsfwc-shortcode-tags-attribute-filters"></div>';
} );

```

`data-facet_name`: It should same as the name of the field added before. 
				   For example: here name of the field added before is `'tags'` so the `data-facet_name` should be `tags`

`data-title`: Title for the filter

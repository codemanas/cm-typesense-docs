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
1. Then on your site's dashboard, go to **WordPress Plugins > Add New > Search for "Search with Typesense"**
2. Click Install and then activate Plugin 
---


## Getting started

### Activate License
After activating the plugin, go to **Typesense->Addons**, then activate the license.

![License Activate](img/license.png)

### Indexing products

First you need to index i.e. push data to Typsense cloud. To do so, follow the below steps:

1. Go to **Typsense->Typesense**
2. Select the **Products** post type from the dropdown in **Select Posts Types to Enable**
3. Then you can set the Products' **label** and **max suggetion** to be listed on autocomplete.
4. After that, click the **Index** button to index. It may take few minutes depending upon the number of products you have.
5. When the indexing is complete, you will get the success message and process is complete.

![Product Indexing](img/indexing.png)

### Settings

The plugin provides the following default settings at **Typesense->WooCommerce**:

1. **Hijack Shop page** - Hijack shop page listing by the instant search

2. **Filters**
	* **Enable category** - Enable category filtering
	* **Enable price** - Enable price filtering
	* **Enable rating** - Enable filtering by rating
	* **Enable attributes** - Enable filter by attributes
	* **Enable sortby** - Enable sortby

3. **Pagination** - Enable pagination

4. **Show featured products first** - Display featured products first while filtering or searching products

5. **Search placeholder** - Change placeholder text on the shop's search

6. **Hijack Product Search** - Hijack WooCommerce search widget and block with Autocomplete.

![Product Setting](img/setting.png)

**Note:** Same settings are provided in **Dashboard->Customize** then **WooCommerce->Typesense Settings** for previewing the live changes.

![Product Customizer Setting](img/customizer.png)

## Shortcodes

`[cm_tsfwc_search cat_filter='show' price_filter='show' rating_filter='show' attribute_filter='show' pagination='show' sortby='show' placeholder='Search products...' show_featured_first='no']`

#### Options:

**cat_filter**

* Value: `show` or `hide`
* Description: Determines the showing or hiding of the category filter
* Default value: "show"

**price_filter**

* Value: `show` or `hide`
* Description: Determines the showing or hiding of the price filter
* Default value: "show"

**rating_filter**

* Value: `show` or `hide`
* Description: Determines the showing or hiding of the rating filter
* Default value: "show"

**attribute_filter**

* Value: `show` or `hide`
* Description: Determines the showing or hiding of the attribute filter
* Default value: "show"

**pagination**

* Value: `show` or `hide`
* Description: Determines the showing or hiding of pagination
* Default value: "show"

**sortby**

* Value: `show` or `hide`
* Description: Determines the showing or hiding of the sortby filter
* Default value: "show"

**placeholder**

* Value: Any string
* Description: Placeholder text for the search input field
* Default value: "Search products"

**show_featured_first**

* Value: `yes` or `no`
* Description: Show the featured products first on the listing while searching or filtering
* Default value: "no"


## Template Overwriting

Overriding the template allows you to change the output for the product listing design as you need to.

The templates are in the plugin `typesense-search-for-woocommerce/templates` and you can override it by copying it to your theme.

To override, copy files from `wp-content/plugins/typesense-search-for-woocommerce/templates/` folder to `wp-content/themes/your-theme/search-with-typesense/woocommerce`. Then you can make the changes as you need.


For example: if you want the filters to show up on the right instead of the left. 

* Copy the file `instant-search.php` from `typesense-search-for-woocommerce/templates/instant-search.php` to `your-theme/search-with-typesense/woocommerce/instant-search.php`. 

* And change the div structure so that `filter-panel` is after `main-panel`.

*End result:*
![Product Indexing](img/result.png)


## Action Hooks & Filter Hooks / Extending Plugin
There are plenty of Hooks and Filters provided by the plugin to allow developers to customize or add additional functionality to the plugin
### Filter Hooks:
Please see [https://developer.wordpress.org/plugins/hooks/filters/](https://developer.wordpress.org/plugins/hooks/filters/) for details of what filters are in WordPress.

**cm_tsfwc_per_page_config**

* Description: Change the per page listing and values
* Arguments: `$per_page_config` Array of configs with label and value	
* Default value:
```
	[
		[ 'label' => 'Per page', 'value' => $atts['per_page'], 'default' => true ],
		[ 'label' => '10 per page', 'value' => 10 ],
		[ 'label' => '20 per page', 'value' => 20 ],
		[ 'label' => '30 per page', 'value' => 30 ],
		[ 'label' => '40 per page', 'value' => 40 ],
		[ 'label' => '50 per page', 'value' => 50 ],
	]
```

**cm_tsfwc_product_fields**

* Description: Add new fields to schema to be indexed.
* Arguments: `$product_fields` Array of fields to be indexed.

**cm_tsfwc_data_before_entry**

* Description: Add the formatted data to the added fields.
* Arguments:
	* `$formatted_data` Array of data to be returned.
	* `$raw_data` Raw data containing product object 
	* `$object_id` Object ID passed
	* `$schema_name` Name of the schema which is `product` in this case.

### Action Hooks:
Please see [https://developer.wordpress.org/plugins/hooks/actions/](https://developer.wordpress.org/plugins/hooks/actions/) for details of what action hooks are in WordPress.


**cm_tsfwc_custom_attributes**

* Description: Hook to add custom attributes HTML to the structure
* Location: `templates/instant-search.php`

## Change per page dropdown values on frontend

### Use Case:
What if you want to change the 10 per page, 20 per page and so on value to your own custom, let's say 50 per page, 100 per page and so on.

### How to do it:
The plugin provides a filter: `cm_tsfwc_per_page_config` to change it.

You can use it like below:

```
add_filter( 'cm_tsfwc_per_page_config', 'your_slug_change_per_page' );

function your_slug_change_per_page( $per_page_config ) {
	$per_page_config = [
		[ 'label' => '50 per page', 'value' => 50, 'default' => true ], // one value should always have 'default' => true
		[ 'label' => '100 per page', 'value' => 100 ],
		[ 'label' => '150 per page', 'value' => 150 ],
		[ 'label' => '200 per page', 'value' => 200 ],
	];
	return $per_page_config;
}
```


## Adding custom taxonomy as filters

### Use Case:
Suppose you want to add tags ( or any other custom taxonomy ) filter to the shop/archive page other than the default ones provided by the addon. 

### How to do it:

#### Add field to the schema: 

First you need to add your field to the `$product_fields` array which is added to the schema using the filter `cm_tsfwc_product_fields` like this:

```
add_filter( 'cm_tsfwc_product_fields', 'your_slug_add_product_fields' );

function your_slug_add_product_fields( $product_fields ) {
	$product_fields[] = [ 'name' => 'tags', 'type' => 'string[]', 'facet' => true ];

	return $product_fields;
}

```

***Note: While adding new field to schema only the `name` should be different. `type` should be `string[]` and `facet` should always be `true` ***



#### Update the document data to be indexed

After you have added the field, data for the field should be provided using the filter `cm_tsfwc_data_before_entry` like below:

```
add_filter( 'cm_tsfwc_data_before_entry', 'your_slug_add_data_before_entry', 10, 4 );

function your_slug_add_data_before_entry( $formatted_data, $raw_data, $object_id, $schema_name ) {

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

}

```

***Note: The index for the `$formatted_data` should be same as name of the field added before. For example: name of the field added before is `'tags'` so the index for the `$formatted_data` is also `tags`. ***

***Important: After changing the schema, collection should be deleted and reindexed to work properly.***

### Displaying the filter

To display the filter on the frontend, use the action `cm_tsfwc_custom_attributes` like below:


```
add_action( 'cm_tsfwc_custom_attributes', 'your_slug_add_custom_attr' );

function your_slug_add_custom_attr() {
	echo '<div data-facet_name="tags" data-title ="' . __( "Filter by Tags", 'storefront' ) . '" class="cm-tsfwc-shortcode-tags-attribute-filters"></div>';
}

```

`data-facet_name`: It should same as the name of the field added before. 
				   For example: here name of the field added before is `'tags'` so the `data-facet_name` should be `tags`

`data-title`: Title for the filter


## Adding static code / widgets to the sidebar

### Use Case:
Suppose you want to add default WooCommerce widgets like *Top Rated Products* below the filters

### How to do it:

#### Use `cm_tsfwc_before_filter_panel_end` hook

```
add_action( 'cm_tsfwc_add_widgets', 'mytheme_add_widgets' );

function mytheme_add_widgets() {
	the_widget( 'WC_Widget_Top_Rated_Products' );
}

```


## Removing attribute filter

### Use Case:
Suppose you want to remove Filter by `size` filter.

#### Use `cm_tsfwc_attribute_facet_skip` hook

```
add_filter( 'cm_tsfwc_attribute_facet_skip', 'mytheme_hide_attribute_facet' );

function mytheme_hide_attribute_facet() {
	return 'book-author';
}
```
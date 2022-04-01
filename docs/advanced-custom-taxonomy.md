# Adding Custom Taxonomy as Collection

## Introduction

Adding custom or additional taxonomy as a collection. From version 1.3.1 - the plugin adds the default post category as an indexable taxonomy option. To add additional/custom taxonomy - the following steps are required

1. [Add as Available Index Type](#add-available-index-type)
2. [Add Schema for Custom Taxonomy](#add-schema-for-custom-taxonomy)
3. Format Document Before Entry (optional)

This example assumes that you have a custom post type called book, and a custom taxonomy called genre

```
/**
 * Create genres for the post type "book".
 *
 * @see register_post_type() for registering custom post types.
 */
function wp_docs_create_book_taxonomies() {
	// Add new taxonomy, make it hierarchical (like categories)
	$labels = array(
		'name'              => _x( 'Genres', 'taxonomy general name', 'textdomain' ),
		'singular_name'     => _x( 'Genre', 'taxonomy singular name', 'textdomain' ),
		'search_items'      => __( 'Search Genres', 'textdomain' ),
		'all_items'         => __( 'All Genres', 'textdomain' ),
		'parent_item'       => __( 'Parent Genre', 'textdomain' ),
		'parent_item_colon' => __( 'Parent Genre:', 'textdomain' ),
		'edit_item'         => __( 'Edit Genre', 'textdomain' ),
		'update_item'       => __( 'Update Genre', 'textdomain' ),
		'add_new_item'      => __( 'Add New Genre', 'textdomain' ),
		'new_item_name'     => __( 'New Genre Name', 'textdomain' ),
		'menu_name'         => __( 'Genre', 'textdomain' ),
	);

	$args = array(
		'hierarchical'      => true,
		'labels'            => $labels,
		'show_ui'           => true,
		'show_admin_column' => true,
		'query_var'         => true,
		'rewrite'           => array( 'slug' => 'genre' ),
	);

	register_taxonomy( 'genre', array( 'book' ), $args );
}

// hook into the init action and call create_book_taxonomies when it fires
add_action( 'init', 'wp_docs_create_book_taxonomies', 0 );
```

## Add Available Index Type

The following code will add the genre option to be selected and configured via Typesense > Typesense admin area. For a taxonomy it is implicitly required to define "type => taxonomy".

```
/** Add the genre option to available index list **/
	function cm_typesense_add_taxonomy( $available_post_types ) {
		$available_post_types['category'] = [ 'label' => 'Post Categories', 'value' => 'category', 'type' => 'taxonomy' ];

		return $available_post_types;
	}
	add_filter( 'cm_typesense_available_index_types', 'cm_typesense_add_taxonomy' );

```
The following code updates taxonomy - any time changes are made to taxonomy
```
	function cm_typesense_add_taxonomy_for_update( $taxonomies ) {
		$taxonomies[] = 'genre';

		return $taxonomies;
	}

	add_filter( 'cm_typesense_enabled_taxonomy_for_post_type', 'cm_typesense_add_taxonomy_for_update' );
```

*** Make sure the value for genre is the same as slug of the taxonomy. ***

## Add Schema for Custom Taxonomy

You can define - your taxonomy schema as any way you want. But to be compatible with the default autocomplete and instant search templates - please use the following base schema.

``` 
function cm_typesense_add_post_category_schema( $schema, $name ) {
		if ( $name == 'genre' ) {
			$schema = [
				'name'                  => 'genre',
				'fields'                => [
					[ 'name' => 'term_id', 'type' => 'string' ],
					[ 'name' => 'id', 'type' => 'string' ],
					[ 'name' => 'taxonomy', 'type' => 'string' ],
					[ 'name' => 'post_title', 'type' => 'string' ],
					[ 'name' => 'post_content', 'type' => 'string' ],
					[ 'name' => 'slug', 'type' => 'string' ],
					[ 'name' => 'posts_count', 'type' => 'int64' ],
					[ 'name' => 'permalink', 'type' => 'string' ],
				],
				'default_sorting_field' => 'posts_count'
			];
		}


		return $schema;
	}

add_filter( 'cm_typesense_schema', 'cm_typesense_add_post_category_schema', 10, 2 );
```

## Format Document Before Entry (optional)

This step is only required if you are adding additional fields or have modified the schema. For example if schema has a thumbnail that you would like to show. Suppose I have added a post thumbnail field via ACF which return image URL. Then the schema would be

``` 
function cm_typesense_add_post_category_schema( $schema, $name ) {
		if ( $name == 'genre' ) {
			$schema = [
				'name'                  => 'genre',
				'fields'                => [
					[ 'name' => 'term_id', 'type' => 'string' ],
					[ 'name' => 'id', 'type' => 'string' ],
					[ 'name' => 'taxonomy', 'type' => 'string' ],
					[ 'name' => 'post_title', 'type' => 'string' ],
					[ 'name' => 'post_content', 'type' => 'string' ],
					[ 'name' => 'slug', 'type' => 'string' ],
					[ 'name' => 'posts_count', 'type' => 'int64' ],
					[ 'name' => 'permalink', 'type' => 'string' ],
					['name'=>'post_thumbnail','type'=>'string']
				],
				'default_sorting_field' => 'posts_count'
			];
		}


		return $schema;
	}

add_filter( 'cm_typesense_schema', 'cm_typesense_add_post_category_schema', 10, 2 );
```
Then we can add the data the following way
```
    function cm_typesense_format_taxonomy_data_before_entry( $formatted_data, $raw_data, $object_id, $schema_name ) {
		if ( $schema_name == 'genre' ) {
			//only need to add the additional data
			$formatted_data['post_thumbnail'] = get_field( 'image', $raw_data ) ?? CODEMANAS_TYPESENSE_ROOT_URI_PATH . '/assets/placeholder.jpg';
		}

		return $formatted_data;
	}

	add_filter( 'cm_typesense_data_before_entry', 'cm_typesense_format_taxonomy_data_before_entry', 10, 4 );
```
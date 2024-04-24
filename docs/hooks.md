## 1.  FILTERS

- ### cm_typesense_available_index_types
$available_index_types

- ### m_typesense_bulk_posts_per_page
10

- ### cm_typesense_post_status
'publish'

- ### cm_typesense_bulk_index_query_args
$args

- ### cm_typesense_bulk_import_skip_post
false, $post

- ### cm_typesense_bulk_posts_per_page
40

- ### cm_typesense_bulk_index_query_args
$args

- ### cm_typesense_bulk_import_skip_post
 false, $term

- ### cm_typesense_enabled_addons
[]

- ### cm_typesense_date_format
get_option( 'date_format' )

- ### cm_typesense_popup_shortcode_params
is_array( $options ) ? wp_parse_args( $options, $defaults ) : $defaults

- ### cm_typesense_locate_template
locate_template( $this->theme_folder . '/' . $file ), $file, $args

- ### cm_typesense_post_status
[ 'publish' ]

- ### m_typesense_post_remove_status
[ 'draft', 'pending' ] 
			    
- ### _typesense_force_remove_post_on_updatecm 
 false, $post 

- ### codemanas_typesense_indexed_post_types 
$this->enablePostTypes 

- ### cm_typesense_enabled_taxonomy_for_post_typehe
[ 'category' ]

- ### cm_typesense_schema
$schema, $name

- ### cm_typesense_html_image_size
'medium'

- ### cm_typesense_data_before_entry
$formatted_data, $raw_data, $object_id, $schema_name 

- ### cm_typesense_autocomplete_search_url
trailingslashit( home_url() ) . '?s=' 

- ### cm_typesense_autocomplete_collections
$collections

- ### cm_typesense_search_autocomplete_settings
[]

- ### cm_typesense_additional_autocomplete_params
[]

- ### cm_typesense_search_facets
$facets[ $schemaName ], $schemaName

- ### cm_typesense_additional_search_params
[]

- ### cm_typesense_additional_config
[]

- ### cm_typesense_routing
$args['routing'] 

- ### cm_typesense_search_facet_label
 $filter_label, $filter, $post_type

- ### cm_typesense_search_facet_title
  sprintf( '%s', esc_html( ucwords( $filter_lab ))), $filter, $post_type

- ### cm_typesense_search_facet_settings
 ['searchable' => false], $filter, $post_type

- ### cm_typesense_filter_type
'refinement', $filter, $post_type

- ### cm_typesense_search_box_settings
[]
 
- ### cm_typesense_search_sortby_items
             [
				[
					'label' => __( 'Most Posts', 'search-with-typesense' ),
					'value' => TypesenseAPI::getInstance()->getCollectionNameFromSchema( $post_type )
				],
				[
					'label' => __( 'Least Posts', 'search-with-typesense' ),
					'value' => TypesenseAPI::getInstance()->getCollectionNameFromSchema( $post_type ) . '/sort/posts_count:asc'
				],
			], $post_type                

- ### cm_typesense_search_sortby_items  
            [
                [
                'label' => __( 'Recent', 'search-with-typesense' ),
					'value' => TypesenseAPI::getInstance()->getCollectionNameFromSchema( $post_type )
				],
				[
					'label' => __( 'Oldest', 'search-with-typesense' ),
					'value' => TypesenseAPI::getInstance()->getCollectionNameFromSchema( $post_type ) . '/sort/sort_by_date:asc'
				],
            ],$post_type            

- ### cm_typesense_search_sortby_settings
['items' => $sortByItems,], $post_type


## 2.  ACTIONS

- ### cm_typesense_bulk_import_on_post_skipped
$post

- ### cm_typesense_bulk_import_on_term_skipped
$term

- ### cm_typesense_before_bulk_index

- ### cm_typesense_after_bulk_index

- ### cm_typesense_licensing_area

- ### cm_typesense_before_instant_search_results_output
$args, $config, $facets, $schemas

- ### cm_typesense_instant_search_results_output
$args, $config, $facets, $schemas

- ### cm_typesense_after_instant_search_results_output
$config, $args

- ### cm_typesense_instant_search_results_before_filter_panel
$facets

- ### cm_typesense_instant_search_results_after_filter_panel
$facets 

- ### cm_typesense_instant_search_results_main_panel_body
$config, $post_type

- ### cm_typesense_instant_search_header
$passed_args, $config, $facets, $schema




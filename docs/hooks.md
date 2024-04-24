## 1.  FILTERS

### cm_typesense_available_index_types
    * Description: 
    * Arguments: $available_index_types

### cm_typesense_bulk_posts_per_page
    * Description:
    * Arguments: 10
                 40

### cm_typesense_post_status
    * Description:
    * Arguments: 'publish'
                 [ 'publish' ]

### cm_typesense_bulk_index_query_args
    * Description:
    * Arguments: $args

### cm_typesense_bulk_import_skip_post
    * Description:
    * Arguments: false
                 $post
                 $term

### cm_typesense_enabled_addons
    * Description:
    * Arguments: []

### cm_typesense_date_format
    * Description:
    * Arguments: get_option( 'date_format' )

### cm_typesense_popup_shortcode_params
    * Description:
    * Arguments: is_array( $options ) ? wp_parse_args( $options, $defaults ) : $defaults

### cm_typesense_locate_template
    * Description:
    * Arguments: locate_template( $this->theme_folder . '/' . $file ), $file, $args

### cm_typesense_post_remove_status
    * Description:
    * Arguments: [ 'draft', 'pending' ] 
    
### _typesense_force_remove_post_on_updatecm 
    * Description:
    * Arguments: 
 false, $post 

### codemanas_typesense_indexed_post_types 
    * Description:
    * Arguments: $this->enablePostTypes 

### cm_typesense_enabled_taxonomy_for_post_typehe
    * Description:
    * Arguments: 
[ 'category' ]

### cm_typesense_schema
    * Description:
    * Arguments: $schema, $name

### cm_typesense_html_image_size
    * Description:
    * Arguments: 'medium'

### cm_typesense_data_before_entry
    * Description:
    * Arguments: $formatted_data, $raw_data, $object_id, $schema_name 

### cm_typesense_autocomplete_search_url
    * Description:
    * Arguments: trailingslashit( home_url() ) . '?s=' 

### cm_typesense_autocomplete_collections
    * Description:
    * Arguments: $collections

### cm_typesense_search_autocomplete_settings
    * Description:
    * Arguments: []

### cm_typesense_additional_autocomplete_params
    * Description:
    * Arguments: []

### cm_typesense_search_facets
    * Description:
    * Arguments: $facets[ $schemaName ]
                 $schemaName

### cm_typesense_additional_search_params
    * Description:
    * Arguments: []

### cm_typesense_additional_config
    * Description:
    * Arguments: []

### cm_typesense_routing
    * Description:
    * Arguments: $args['routing'] 

### cm_typesense_search_facet_label
    * Description:
    * Arguments:  $filter_label, $filter, $post_type

### cm_typesense_search_facet_title
    * Description:
    * Arguments: sprintf( '%s', esc_html( ucwords( $filter_lab )))
                 $filter
                 $post_type

### cm_typesense_search_facet_settings
    * Description:
    * Arguments: ['searchable' => false]
                 $filter
                 $post_type

### cm_typesense_filter_type
    * Description:
    * Arguments: 'refinement'
                  $filter
                  $post_type

### cm_typesense_search_box_settings
    * Description:
    * Arguments: []

### cm_typesense_search_sortby_items
    * Description:
    * Arguments: 
             [
				[
					'label' => __( 'Most Posts', 'search-with-typesense' ),
					'value' => TypesenseAPI::getInstance()->getCollectionNameFromSchema( $post_type )
				],
				[
					'label' => __( 'Least Posts', 'search-with-typesense' ),
					'value' => TypesenseAPI::getInstance()->getCollectionNameFromSchema( $post_type ) . '/sort/posts_count:asc'
				],
			]               
            [
                [
                'label' => __( 'Recent', 'search-with-typesense' ),
					'value' => TypesenseAPI::getInstance()->getCollectionNameFromSchema( $post_type )
				],
				[
					'label' => __( 'Oldest', 'search-with-typesense' ),
					'value' => TypesenseAPI::getInstance()->getCollectionNameFromSchema( $post_type ) . '/sort/sort_by_date:asc'
				],
            ]
            $post_type            

### cm_typesense_search_sortby_settings
    * Description:
    * Arguments: ['items' => $sortByItems,]
                 $post_type


## 2.  ACTIONS

### cm_typesense_bulk_import_on_post_skipped
    * Description:
    * Arguments: $post

### cm_typesense_bulk_import_on_term_skipped
    * Description:
    * Arguments: $term

### cm_typesense_before_bulk_index
    * Description:

### cm_typesense_after_bulk_index
    * Description:

### cm_typesense_licensing_area
    * Description:

### cm_typesense_before_instant_search_results_output
    * Description:
    * Arguments: $args
                 $config
                 $facets
                 $schemas

### cm_typesense_instant_search_results_output
    * Description:
    * Arguments: $args
                 $config
                 $facets
                 $schemas

### cm_typesense_after_instant_search_results_output
    * Description:
    * Arguments: $config
                 $args

### cm_typesense_instant_search_results_before_filter_panel
    * Description:
    * Arguments: $facets

### cm_typesense_instant_search_results_after_filter_panel
    * Description:
    * Arguments: $facets 

### cm_typesense_instant_search_results_main_panel_body
    * Description:
    * Arguments: $config
                 $post_type

### cm_typesense_instant_search_header
    * Description:
    * Arguments: $passed_args
                 $config
                 $facets
                 $schema




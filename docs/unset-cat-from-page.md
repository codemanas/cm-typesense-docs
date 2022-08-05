#Remove category field from Page's schema#

By default, the schema of `page` gets the same schema as `post`. That means `page` will also have `category` and `cat_links` in it's schema. But that is redundent since page does not have categories. So those fields should be removed from page's schema.

To remove the fields, paste the below code in your theme's `functions.php`

```
 add_filter( 'cm_typesense_schema', 'remove_cat_facet_from_page', 10, 2 );

 function remove_cat_facet_from_page( $schema, $name ) {
    if ( $name == 'page' ) {
        foreach( $schema['fields'] as $index => $field ) {
            if( 'category' == $field['name'] || 'cat_link' == $field['name'] ) {
                unset( $schema['fields'][ $index ]);
            }            
        }
    }

    // Should be sorted because unset removes the index number only and leave empty in between
    sort( $schema['fields']);
    return $schema;
}
```

**Note: After implementing this, `page` has to be reindexed by clicking `Delete and Re-index` on settings page**
#Changing Default Widgets
By default, all facets for filtering are shown as [refinementList](https://www.algolia.com/doc/api-reference/widgets/refinement-list/js/).
As of version 1.2.4 developers have the version to add between [menu](https://www.algolia.com/doc/api-reference/widgets/menu/js/), [rangeSlider](https://www.algolia.com/doc/api-reference/widgets/range-slider/js/) or [rangeInput](https://www.algolia.com/doc/api-reference/widgets/range-input/js/).

***Note: For rangeSlider and rangeInput the facet must be int64.***

To do this you can use filer `cm_typesense_filter_type`.
The following code is written in child themes functions.php file.

```
function cm_change_facet_widget_type( $filterType, $filterName ) {
	if ( $filterName == 'category' ) {
		$filterType = 'menu';
	} else if ( $filterName == 'comment_count' ) {
		/*For range slider the schema for field must be int64*/
		$filterType = 'rangeSlider';
	}

	return $filterType;
}

add_filter( 'cm_typesense_filter_type', 'cm_change_facet_widget_type', 10, 2 );
```
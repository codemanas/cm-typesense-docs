# Shortcodes

## Instant Search

###Shortcode
```
[cm_typesense_search post_types="book,post" columns="3" filter="show" per_page="3" sortby="off" placeholder="Search for..."]
```

### Options:
####placeholder
- Values: Any String
- Description: Determines the placeholder for search field
- Default: "Search for"

####columns
- Values: 1 to 5
- Description: Determines how may results to show per row
- Default: 3

####post_types
- Values: Post Slugs e.g. `post,page,book`
- Description: accepts enabled post_type slugs to show in instant search, accepts multiple slugs in comma separated form `post,page,slug`
If multiple sources are enabled - filtering is disabled.
- Default: All enabled post_types

####filter
- Values: `show` or `hide`
- Description: accepts "show" or "hide" - determines if facet/category filtering should be shown.
- Default: `hide`

####per_page
- Description: Determines no of possible/matched results to show per_page
- Default: 3

####sortby
- Values: `show` or `hide`
- Description: Determines whether to provide a sorting option - by default sorting option is according to post published
- Default: `show`

####pagination
- Values: `show` or `hide`
- Description: Determines whether to show or hide the pagination for results
- Default: `show`

##Autocomplete

###Shortcode
```
[cm_typesense_autocomplete placeholder="Search for...""]
```

Description: Add the Autocomplete form wherever you may want to. There are no other options.

### Options:
####placeholder
- Values: Any String
- Description: Determines the placeholder for search field
- Default: "Search for"
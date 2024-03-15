## WP CLI

WP-CLI serves as the command-line interface for WordPress, offering a range of commands for various actions typically executed in the WordPress admin.

Within the framework of the Search With Typesense plugin, our plugin introduces its own set of WP-CLI commands. These commands enable you to index and delete post types, with the flexibility to specify particular IDs. Additionally, the plugin provides an option to assess the health status of the Typesense server.

This is very helpful if you have command line access to your WordPress installation instace on your server.

**Kindly be aware that the subsequent commands will not remove your posts from the WordPress database. Instead, these commands exclusively index or delete the posts on your Typesense Server.**

**Note**: *We intend to incorporate additional commands in the future based on your requests. Your feedback would be highly valuable.*

## Supported Commands

### wp typesense index

Index a specific post type to Typesense server

#### Options

**<post-type>**
	Slug of the post type you want to index.

**[--ids=<post-ids>]**
	The comma separated IDs of the posts of that post type you want to index.

#### Examples

```
# Index all the default posts
$ wp typesense index post
```

```
# Index all only specific posts with IDs: 2,3 and 4 for the custom post type 'books'
$ wp typesense index books --ids=2,3,4
```

### wp typesense delete

Delete a specific post type from Typesense server

#### Options

**<post-type>**
	Slug of the post type you want to delete.

**[--ids=<post-ids>]**
	The comma separated IDs of the posts of that post type you want to delete.

#### Examples

```
# Drop the post collection from server
$ wp typesense delete post
```
**Note: This will drop the post collection from the Typesense server**


```
# delete all only specific posts with IDs: 2,3 and 4 for the custom post type 'books'
$ wp typesense delete books --ids=2,3,4
```

### wp typesense delete-reindex

Delete/drop the collection and reindex the collections with documents

### wp typesense health

Check the health status of your Typesense server.

#### Examples

```
$ wp typesense health
```
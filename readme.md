# Wordpress Custom post type and Taxonomy create

### Description
Create a custom post type with slug in wordpress and create tag and categories for that post type.





#### For Create Custom Post Type with slug
##### Paste the code in function.php
```injectablephp
function my_custom_post_type()
{


    register_post_type(
        'mypost',

        $args = array(
            'labels' => array(
                'name' => __('My Post'),
                'singular_name' => __('my_post'),
                'add_new' => 'Add New Post',
                'edit_item' => 'Edit Post',
                'search_items' => 'Search Post',
            ),
            'supports' => array('title', 'editor', 'custom-fields', 'thumbnail', 'page-attributes', 'post-formats', 'excerpt'),
            'menu_icon' => 'dashicons-schedule',
            'show_tagcloud' => false,
            'rewrite' => array('slug' => 'my_post', 'with_front' => false),
            'taxonomy' => true,
            'query_var' => true,
            'hierarchical' => false,
            'public' => true,
            'show_ui' => true,
            'show_in_menu' => true,
            'menu_position' => null,
            'show_in_admin_bar' => true,
            'show_in_nav_menus' => true,
            'can_export' => true,
            'has_archive' => true,
            'exclude_from_search' => false,
            'publicly_queryable' => true,
            'capability_type' => 'post',

        )


    );


}

add_action('init', 'my_custom_post_type');
```

You can check this link to understand better about post type parameters [Custom post type perametters](https://developer.wordpress.org/reference/functions/register_post_type/)


#### For Create Custom Taxonomy with slug
##### Paste the code in function.php 

```injectablephp
function my_custom_post_type_category_taxonomy()
{
    // Add new taxonomy, make it hierarchical (like categories)
    $labels = array(
        'name' => _x('Genres', 'taxonomy general name', 'textdomain'),
        'singular_name' => _x('Genre', 'taxonomy singular name', 'textdomain'),
        'search_items' => __('Search Genres', 'textdomain'),
        'all_items' => __('All Genres', 'textdomain'),
        'parent_item' => __('Parent Genre', 'textdomain'),
        'parent_item_colon' => __('Parent Genre:', 'textdomain'),
        'edit_item' => __('Edit Genre', 'textdomain'),
        'update_item' => __('Update Genre', 'textdomain'),
        'add_new_item' => __('Add New Genre', 'textdomain'),
        'new_item_name' => __('New Genre Name', 'textdomain'),
        'menu_name' => __('Genre', 'textdomain'),
    );

    $args = array(
        'hierarchical' => true,
        'labels' => $labels,
        'show_ui' => true,
        'show_admin_column' => true,
        'query_var' => true,
        'rewrite' => array('slug' => 'genre'),
    );

    register_taxonomy('genre', array('mypost'), $args);

    unset($args);
    unset($labels);

    // Add new taxonomy, NOT hierarchical (like tags)
    $labels = array(
        'name' => _x('Writers', 'taxonomy general name', 'textdomain'),
        'singular_name' => _x('Writer', 'taxonomy singular name', 'textdomain'),
        'search_items' => __('Search Writers', 'textdomain'),
        'popular_items' => __('Popular Writers', 'textdomain'),
        'all_items' => __('All Writers', 'textdomain'),
        'parent_item' => null,
        'parent_item_colon' => null,
        'edit_item' => __('Edit Writer', 'textdomain'),
        'update_item' => __('Update Writer', 'textdomain'),
        'add_new_item' => __('Add New Writer', 'textdomain'),
        'new_item_name' => __('New Writer Name', 'textdomain'),
        'separate_items_with_commas' => __('Separate writers with commas', 'textdomain'),
        'add_or_remove_items' => __('Add or remove writers', 'textdomain'),
        'choose_from_most_used' => __('Choose from the most used writers', 'textdomain'),
        'not_found' => __('No writers found.', 'textdomain'),
        'menu_name' => __('Writers', 'textdomain'),
    );

    $args = array(
        'hierarchical' => false,
        'labels' => $labels,
        'show_ui' => true,
        'show_admin_column' => true,
        'update_count_callback' => '_update_post_term_count',
        'query_var' => true,
        'rewrite' => array('slug' => 'writer'),
    );

    register_taxonomy('writer', 'mypost', $args);
}

// hook into the init action and call create_book_taxonomies when it fires
add_action('init', 'my_custom_post_type_category_taxonomy', 0);
```

To know details about [custom register taxonomy perameters](https://developer.wordpress.org/reference/functions/register_taxonomy/)
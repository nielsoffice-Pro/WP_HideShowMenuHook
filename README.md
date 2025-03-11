# WP_HideShowMenuHook
Display and hide menu if the user is login or logout WordPress Hook


```PHP

/* Hide menu login in once active session! */
add_filter('wp_nav_menu_items', 'hide_about_menu_item_by_title', 10, 2);
function hide_about_menu_item_by_title($items, $args) {
    // Check if the user is logged in
    if (is_user_logged_in()) {
        // Check if "About" is in the menu items and remove it
        $items = preg_replace('/<li[^>]*><a[^>]*>login<\/a><\/li>/i', '', $items);
        $items = preg_replace('/<li[^>]*><a[^>]*>register<\/a><\/li>/i', '', $items);
        /* ... add more menu names goes here to hide if user is logged in */
    }

    return $items;
}

/* Show menu when the user is login with is lgoout menu */
add_filter('wp_nav_menu_items', 'show_profile_menu_item_only_logged_in', 10, 2);
function show_profile_menu_item_only_logged_in($items, $args) {
    // Check if the user is logged in
    if (is_user_logged_in()) {
        return $items;  // Show the menu as is
    } else {
        // Remove "Profile" menu item if the user is not logged in
        $items = preg_replace('/<li[^>]*><a[^>]*href="[^"]*logout[^"]*"[^>]*>[^<]*<\/a><\/li>/i', '', $items);
 	/* ... add more menu names goes here to hide if user is NOT login ! */
        return $items;
    }
}

```

<h6>Redirect User after Login or once user is login restrict page </h6>

```PHP

/* redirect to home once user is login */
// add_action('template_redirect', 'redirect_logged_in_users_from_specific_page', 15);
function redirect_logged_in_users_from_specific_page() {
    // Check if the current page slug is 'page-name' and the user is logged in
    if (( is_page('login') || is_page('forgot-password') )&& is_user_logged_in()) {
        // Redirect to the homepage
        wp_redirect(home_url());
        exit();
    }
}


```

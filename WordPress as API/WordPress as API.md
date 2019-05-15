The WordPress app can be used to provide endpoints for the frontend app (based on any popular view library) to consume.

In this case, the theme should consist of files that are the required minimum for admin functionality—`functions.php`, `index.php`, `screenshot.png` (optional), and `style.css`.

Usually, `functions.php` contains redirection so that users cannot access the 'php' WordPress front.

```php
add_action( 'template_redirect', 'inf_theme_redirect' );
if ( ! function_exists( 'inf_theme_redirect' ) ) {
  /**
   * Check if the user is logged in or is trying to access the frontend page.
   * In either case, the user should be redirected to the WordPress admin page.
   *
   * @return void
   */
  function inf_theme_redirect() {
    if ( ! is_user_logged_in() ) {
      auth_redirect();
    } elseif ( ! is_admin() ) {
      wp_redirect( site_url( 'wp-admin' ) );
    }
    exit;
  }
}
```

The endpoints for the front end app should be created using either [REST API](https://developer.wordpress.org/rest-api/) or the [Decoupled JSON Content plugin](https://github.com/infinum/decoupled-json-content).

This functionality should be defined in the plugin.

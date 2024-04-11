
# Iris fix for autocomplete on Wordpress old customizer

Wordpress uses Iris for it's colour picker on the customizer. It does this really annoying thing where if you type in a hex code it autocompletes after three characters like 3ab -> 33aabb. 

Iris has this built into it, and we couldn't find a good way to pass settings to disable this feature. So we took Iris and commented out this logic, minified, and boxed it back up.

### Step 1
Add in the iris.min.js file somewhere in your theme folder, for example in my-theme/assets/admin/hs/iris.min.js 

### Step 2
Modify your functions.php file, or wherever you put your functions, to remove the standard iris, and replace it with our new iris.js 

```
 
// Deregister default Iris script and replace with a custom one of our own creation
function replace_default_iris_script() {

    wp_deregister_script( 'iris' );
    wp_deregister_script( 'wp-color-picker' ); 

    wp_register_script( 'iris', '/path/to/iris.js', array( 'jquery-ui-draggable', 'jquery-ui-slider', 'jquery-touch-punch' ), '1.0.0', true );
    wp_enqueue_script( 'iris' );

    wp_register_script( 'wp-color-picker', '/wp-admin/js/color-picker.min.js', array( 'iris' ), '1.0.0', false );
    wp_enqueue_script( 'wp-color-picker' );
}
add_action( 'admin_enqueue_scripts', 'replace_default_iris_script', 9999 );

```

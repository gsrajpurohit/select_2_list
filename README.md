# Select to List
This library allows you to turn select box into ul li list.

### 1. Get a copy of the plugin
You can download the plugin from GitHub.

### 2. Load the required files
In the page's footer, just before, include the required JavaScript files.

```
<script src="js/select.2.list.js"></script>
```

### 3. Create the HTML markup
`<div class="multi col-sm-4" id="multi">
        <select class="gs-selectbox" id="gs-selectbox">
            <option value="1">First Text</option>
            <option value="2">Second Text</option>
            <option value="3">Third Text</option>
            <option value="4">Forth Text</option>
            <option value="5">Fifth Text</option>
            <option value="6">Sixth Text</option>
        </select>
    </div>`

### 4. Instantiate the plugin
```
<script type="text/javascript">
    jQuery( document ).ready(function( $ ) { 
        $.selectedVal = '';
        $('.gs-selectbox').select_2_list({
            easing_time: 500,
            max_height: 150,
            selected_text: 'Select An Option',
            onSelect: function(values) {
                $.selectedVal = values;
            }
        })
        .................
    }); 
</script>
```

### 4. Get selected value
```
<script type="text/javascript">
    jQuery( document ).ready(function( $ ) { 
        .............
        $('#get_values').on('click', function(event) {
            alert($.selectedVal);
        })
    }); 
</script>
```
### Demo
[Demo](https://jsfiddle.net/g_s_rajpurohit/k5o7j3nL/6/).

### Support
If you found a bug or have a feature suggestion, please email me on rajpurohitganpat@gmail.com.
If you need help with implementing the plugin in your project feel free to contact me on rajpurohitganpat@gmail.com.

License The plugin is available under the [MIT license](https://opensource.org/licenses/MIT).



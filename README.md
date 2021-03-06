# waSlideMenu

jQuery plugin that turns big nested (hierarchical) trees into a cool looking multi-level sliding drill down menus. MIT license.

## Demo

* [JSFiddle](http://jsfiddle.net/7LnSY/)
* [demo.webasyst.com](http://demo.webasyst.com/?set_force_theme=default&theme_hash=fe01ce2a7fbac8fafaed7c982a04e229)

## Usage

Link CSS

```html
<link rel="stylesheet" href="/path/to/waslidemenu.css">
```

Link JS *after* jQuery (> 1.7):

```html
<script src="jquery.js" type="text/javascript"></script>
<script src="/path/to/jquery.waslidemenu.js" type="text/javascript"></script>
```

Prepare your HTML

```html
<nav id="mymenu">
	<ul>
		<li>
			<a href="#1">Parent</a>
			<ul>
				<li>
                    <a href="#1.1">Child</a>
                    <ul>
                    	<li>
                    		<a href="#">We need to go deeper</a>
                        </li>
                    </ul>
                </li>
                <li><a href="#1.2">Child</a></li>
            </ul>
        </li>
        <li><a href="#2">Parent</a></li>
        <li><a href="#3">Parent</a></li>
    </ul>
</nav>
```

Init the awesome

```javascript
$(document).ready(function(){
   $('#mymenu').waSlideMenu({});
});
```

## Options

#### Slide speed

```javascript
$('#menu').waSlideMenu({
    slideSpeed: 500
});
```

By default ```400```.

#### Slide effect

```javascript
$('#menu').waSlideMenu({
    slideEasing: 'linear'
});
```

#### Backlink word

```javascript
$('#menu').waSlideMenu({
    backLinkContent: 'Take me back, sir.'
});
```

By default ```Back```.

#### Choose place for backlink (before or after menu)

```javascript
$('#menu').waSlideMenu({
    backOntTop: true
});
```

By default ```false``` - that means 'after' menu.

#### Class for current selected menu element

```javascript
$('#menu').waSlideMenu({
    selectedClass: 'selected-menu'
});
```

By default ```'selected'```.

#### Container selecter, where plugin will load content from menu item url

```javascript
$('#menu').waSlideMenu({
    loadContainer : '#content'
});
```

By default ```''``` - nothing is loading.

#### Minimum menu height

```javascript
$('#menu').waSlideMenu({
    minHeightMenu : 400
});
```

By default ```0``` - no min-height.

#### Menu auto height 

```javascript
$('#menu').waSlideMenu({
    autoHeightMenu : true
});
```

By default ```true```, menu height will adjusts for its content.

#### URL exception

```javascript
$('#menu').waSlideMenu({
    excludeUri : ['/dont-load/', '#pleasedontloadme']
});
```

URLs ```'/dont-load/'``` and ```'#pleasedontloadme'``` will not load in ```loadContainer```. By default ```['/', '#']```. 

#### Load content only latest nested menu items

```javascript
$('#menu').waSlideMenu({
    loadOnlyLatest : true
});
```

By default ```false```. If set to ```true```, then menus will slide without loading content until it reached latest menu item.

#### Menu selector

```javascript
$('#menu').waSlideMenu({
    menuSelector : '.i-am-menu'
});
```

By default ```'ul'```.

#### Menu item selector

```javascript
$('#menu').waSlideMenu({
    itemSelector : '.i-am-menu-item'
});
```

By default ```'li'```.

#### Title for page

```javascript
$('#menu').waSlideMenu({
    setTitle : true
});
```

By default ```false```. After menu item URL loading will set Title tag like menu item link text.

#### Speed of slide up to current menu item

```javascript
$('#menu').waSlideMenu({
    scrollToTopSpeed : 100
});
```

By default ```0```. 
Sometimes after sliding to nested menu or back menu items disappear from visible area. In this case page will slide up to current menu item (selected item).

#### Callbacks

Here ```this``` - plugin instance.

##### After plugin initialization

```javascript
$('#menu').waSlideMenu({
    onInit : function(){
        alert('Here I am!');
    }
});
```

##### After slide to a child submenu

```javascript
$('#menu').waSlideMenu({
    onSlideForward : function(){
        alert('I slide forward (deeper)!');
    }
});
```

##### After slide back to top

```javascript
$('#menu').waSlideMenu({
    onSlideBack : function(){
        alert('I slide back (bubling)!');
    }
});
```

##### After slide animation is completed

```javascript
$('#menu').waSlideMenu({
    afterSlide : function(){
        alert('Yep! I just slide!!');
    }
});
```

##### After click on last node element

```javascript
$('#menu').waSlideMenu({
    onLatestClick : function(){
        alert('Last element clicked: ' + $(this).text());
    }
});
```

Here ```this``` - clicked element.

##### Before load URL

```javascript
$('#menu').waSlideMenu({
    beforeLoad : function(){
        this.html('<img src="myloading.gif">');
    }
});
```

Executes before load starts (async). ```this``` - jQuery object of loadContainer.

##### After load URL (always)

```javascript
$('#menu').waSlideMenu({
    afterLoadAlways : function(){
        alert('You URL request just completed!');
    }
});
```

##### After success load

```javascript
$('#menu').waSlideMenu({
    afterLoadDone : function(){
        alert('Nice URL! 200 OK!');
    }
});
```

##### After fail load

```javascript
$('#menu').waSlideMenu({
    afterLoadFail : function(){
        alert('Bad URL :(');
    }
});
```

#### Event triggers

Following event triggers are available:  ```onInit.waSlideMenu```, ```afterLoadDone.waSlideMenu```, ```afterLoadFail.waSlideMenu```, ```afterLoadAlways.waSlideMenu```.

```javascript
$('#menu').on('onInit.waSlideMenu', function(){
    alert('After INIT waSlideMenu Event');
}).on('afterLoadDone.waSlideMenu', function(){
    alert('After URL load success Event');
}).on('afterLoadFail.waSlideMenu', function(){
    alert('After URL load fails Event');
}).on('afterLoadAlways.waSlideMenu', function(){
    alert('After URL request completed Event');
}).on('onLatestClick.waSlideMenu', function(){
    alert('On last node element click Event');
});;
```

## One more thing

* Doesn't depends on HTML tags. Depends on structure.

```html
<nav id="menu">
    <div class="menu">
        <div class="item">
            <a href="#1">1</a>
            <div class="menu">
                <div class="item"><a href="#1.1">1.1</a></div>
                <div class="item"><a href="#1.2">1.2</a></div>
            </div>
        </div>
        <div class="item"><a href="#2">2</a></div>
        <div class="item"><a href="#3">3</a></div>        
    </div>
</nav>
<script>
    $('#menu').waSlideMenu({
        menuSelector : '.menu',
        itemSelector : '.item'
    });
</script>
```

* Options and callbacks can be set after the initialization

```javascript
var slidemenu = $('#menu').waSlideMenu({});
slidemenu.waSlideMenu({
    slideSpeed : 3000, // veeeeeeeery smooooooth
    afterSlide : function(){
        alert('Yeah!!11 This was coooool smoooth sliiide!');
    }
});
```

* On one page you can set as many sliding menus as you wish

* Can destroy menu at any time (are you sure? :( )

```javascript
$('#menu').waSlideMenu('exec','destroy');
```

## Dependencies

* > jQuery 1.7

## Compatibility

* IE9+
* Google Chrome
* Firefox
* need feedback...

## Issues

Welcome: https://github.com/webasyst/waslidemenu/issues

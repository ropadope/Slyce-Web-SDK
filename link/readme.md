# Getting started

## Parameters

1. **autoInit** - auto init when widget loaded
2. **cid** - client id
3. **selector** - selector for autobinding
4. **imageProp** - element property with product image url
5. **pidProp** - element property with product pid
6. **aTarget** - target attribute for product *a* elements
7. **addCursorStyle** - custom "cursor" style for element after binding
8. **style** - url to css file
9. **theme** - version with custom views


## Auto binding

1. Create elements with **selector** class with widget properties - **imageProp** or **pidProp**
2. Load widget

## Custom
You can use widget without auto binding strategy, for this you need load widget with empty **selector** parameter

After widget loaded they will available as

```javascript
window.LinkWidget
```

And you can use function **searchUrl(url, pid)** like this

```javascript
	$el.on('click', function(evt) {
		var url = $(this).find('img').attr('src');
	    window.LinkWidget.searchUrl(url);
	});
```



## Loading code

```javascript
(function(props) {
            var path = 'cdnw.slycecloud.com/link/loader.js';
            var LinkWiScr = document.createElement('script'); LinkWiScr.type = 'text/javascript'; LinkWiScr.async = true;
            LinkWiScr.src = ('https:' == document.location.protocol ? 'https://' : 'http://') + path;
            var s = document.getElementsByTagName('script')[0];
            s.parentNode.insertBefore(LinkWiScr, s);
            LinkWiScr.onload = function() {
                window.LinkWidgetLoader(props);
            }
        })({
		        autoInit: true,
			    selector: '.linkwidget-btn',
			    imageProp: 'data-image',
			    pidProp: 'data-pid',
			    cid: 'CLIENTID',
			    aTarget: '_blank',
			    addCursorStyle: 'zoom-in',
			    style: 'https://cdnw.slycecloud.com/link/default/style/main.css'
            })
```


## Example

### Binding to element with imageProp (data-image) attribute
Search only by image url, loading screen with image
```
<a href="#" class="linkwidget-btn" data-image="http://s7d9.scene7.com/is/image/BedBathandBeyond/55711143770922p?$">Open</a>
```
### Binding to element with imageProp (data-image) and pidProp (data-pid) attributes
Search by pid, loading screen with image from data-image
```
<a href="#" class="linkwidget-btn" data-image="http://s7d9.scene7.com/is/image/BedBathandBeyond/82170146482259p?$" data-pid="1046482259">Open</a>
```
### Binding to element with imageProp (data-image) attributee
Search by pid, loading screen without image
```
<a href="#" class="linkwidget-btn" data-pid="1046482259">Open</a>
```


# Anchorific.js

Anchorific is a jQuery plugin that automatically generates anchored headings and nested navigations based on header tags. My intention is for it to be used in single-page project documentation.
Project page and demo here: [renaysha.me/anchorific-js](http://renaysha.me/anchorific-js)

## Getting Started
### HTML Structure

You should not skip a level when structuring header tags. H1 should be followed by H2, H2 should be followed by H3 and so on. Anchorific relies heavily on this particular structure when generating the anchor navigation.

``` html
<h1>The Lannisters</h1>
    <h2>Tywin Lanister</h2>
    <h2>Cersei Lannister</h2>
        <h3>Joffrey Baratheon</h3>
        <h3>Myrcella Baratheon</h3>
        <h3>Tommen Baratheon</h3>
    <h2>Jaime Lannister</h2>
    <h2>Tyrion Lannister</h2>
```

Based on the HTML markup above, the plugin will generate nested navigations like this one:

``` html
<ul>
    <li data-tag="1"><a href="#the-lannisters">The Lannisters</a>
        <ul>
             <li data-tag="2"><a href="#tywin-lannister">Tywin Lannister</a></li>
             <li data-tag="2"><a href="#cersei-lannister">Cersei Lannister</a>
                <ul>
                    <li data-tag="3"><a href="#joffrey-baratheon">Joffrey Baratheon</a></li>
                    <li data-tag="3"><a href="#myrcella-baratheon">Myrcella Baratheon</a></li>
                    <li data-tag="3"><a href="#tommen-baratheon">Tommen Baratheon</a></li>
                </ul>
             </li>
             <li data-tag="2"><a href="#jaime-lannister">Jaime Lannister</a></li>
             <li data-tag="2"><a href="#tyrion-lannister">Tyrion Lannister</a></li>
        </ul>
    </li>
</ul>
```

...and it will generate anchored headings like this one:

``` html
<h1>Tywin Lannister</h1>
<!-- This would be turn to -->
<h1 id="tywin-lannister">Tywin Lannister <a href="#tywin-lannister" class="anchor">#</a></h1>
```

#### Existing ID

Any existing ID will be preserved by the plugin:

``` html
<h3 id="what-if-I-already-have-an-id">What about existing ID?</h3>
<!-- This would be turn to -->
<h3 id="what-if-I-already-have-an-id">What about existing ID?<a href="#what-if-I-already-have-an-id" class="anchor">#</a></h3>
```

#### Generate Navigation

Include a div or a nav section where you want the unordered list of anchor navigation to be appended at:

``` html
<nav class='anchorific'></nav>
```

By default, the plugin will append the unordered list under an element with class called anchorific. If you wish to use another class name, you need to specify it in the plugin's option.

### CSS

The nested navigation can be styled easily. Below are the selectors you can use in order to style the generated navigation.

``` css
.anchorific {}
.anchorific ul {}
.anchorific ul li a {}
.anchorific li ul {}
/* active class is generated by the scrollspy */
.anchorific li.active > a {}
.anchorific li.active > ul {}
```

You can also check the [demo](http://renaysha.me/anchorific-js) page's CSS to see how it is done.

### Basic Usage and Options

Use the selector where your headings are located under. And then just call the anchorific method.

``` javascript
$('.content').anchorific();
```

You can call the plugin function with any selector you want as long as it adhere to the HTML structure mentioned above. Options available are as followed:


``` javascript
$('.content').anchorific({
  navigation: '.anchorific', // position of navigation
  headers: 'h1, h2, h3, h4, h5, h6', // headers that you wish to target
	speed: 200, // speed of sliding back to top
	anchorClass: 'anchor', // class of anchor links
	anchorText: '#', // prepended or appended to anchor headings
	top: '.top', // back to top button or link class
	spy: true, // scroll spy
	position: 'append', // position of anchor text
	spyOffset: 0 // specify heading offset for spy scrolling
});
```

Generating navigations, Scroll spy, and 'Back to top' functionality can be disable by assigning false value to the options.

#### Adding 'Back to Top' Button

Just add an element with class top. You can use other class names but it should be specified in the plugin options.

``` html
<a href="#top" class="top">Scroll to top</a>
```

The speed of the scrolling effect can be adjusted by specifying it in the options above.

**Note: remember to add display: none; to the .top styling. It should not be visible when the page first load.**

## Build

Anchorific.js uses Grunt CLI via NodeJS for linting, providing minified of production file, and executing the unit tests of the plugin. Check out the guide on [Grunt's getting started page](http://gruntjs.com/getting-started) to install it.

### Setup

Once you have grunt CLI installed, CD to the project folder and type:

``` bash
$ npm install
```

Execute lint, minification, and unit tests:

``` bash
$ grunt
```

## License

[MIT License](http://opensource.org/licenses/MIT)

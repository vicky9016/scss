<pre>
# scss
Learing SCSS by creating smiple scss file


Refers: https://www.sitepoint.com/8-tips-help-get-best-sass/
Compile to css: http://www.sassmeister.com/

Sassy CSS (SCSS)

SCSS is a CSS pre-processor with syntax advancements. It allows you to use variables, nested rules, mixins, extends and more with CSS-compatible syntax, Style sheets in the advanced syntax are processed by the program, and turned into regular CSS style sheets. 
SCSS is a superset of CSS3’s syntax. This means that every valid CSS3 stylesheet is valid SCSS as well. SCSS files use the extension .scss.  it's not a replacement for CSS, It's an interpreter which spits out CSS in the end. 
Any valid CSS document can be converted to SCSS simply by changing the extension from .css to .scss.

Advantages:
•	Easier to maintain code
•	Cleaner code with re-usability concept
•	Joining of multiple files without HTTP requests
•	compatible with all versions of CSS

Disadvantages:
•	losing benefits of browser's built-in element inspector

Rules and Directives:
Nested Rules:
SCSS allows CSS rules to be nested within one another. The inner rule then only applies within the outer rule’s selector. 
For example:
SCSS:
#main {
  width: 97%;

  p, div {
    font-size: 2em;
    a { font-weight: bold; }
  }

  pre { font-size: 3em; }
}

CSS after compilation:
#main {
 width: 97%;
}
#main p, #main div {
  font-size: 2em;
}
#main p a, #main div a {
  font-weight: bold;
}
#main pre {
  font-size: 3em;
}

Nested Properties:
SCSS:
.title {
  font: {
    family: 'Open Sans', sans-serif;;
    size: 14px;
    weight: 700;
  }
}

CSS after compilation:
.title {
  font-family: 'Open Sans', sans-serif;
  font-size: 14px;
  font-weight: 700;
}


Referencing Parent Selectors:
If you want to have special styles for when that selector is hovered over or for when the body element has a certain class. In these cases, you can explicitly specify where the parent selector should be inserted using the & character.
SCSS:
a {
color: #1a99aa;
&:hover {
text-decoration: underline;
}
}
CSS after compilation:
a {
  color: #1a99aa;
}
a:hover {
  text-decoration: underline;
}

Mixin Directives:
Mixins are used to include a bunch of properties or group declarations together.
SCSS:
@mixin box-radius($arc){
	-moz-border-radius: $arc;
    	-webkit-border-radius: $arc;
   	 border-radius: $arc;  
 }

.box{
	@include box-radius(5px);
Width: 200px;
	Border: 1px solid #ddd;
	background: #d1d1d1;
}

CSS after compilation:
.box {
-moz-border-radius: 5px;
-webkit-border-radius: 5px;
border-radius: 5px;  
width: 200px;
Border: 1px solid #ddd;
background: #d1d1d1;
}

Extend Directive:
You can share properties from one selector to another with this feature.
SCSS:
.title{
font-weight: 700;
color: #575a5a;
}

.heading1{
font-size: 18px;
	@extend .title;
}
.heading2{
font-size: 14px;
	@extend .title;
}

CSS after compilation:
.title, .heading1, .heading2 {
  font-weight: 700;
  color: #575a5a;
}
.heading1 {
  font-size: 18px;
}
.heading2 {
  font-size: 14px;
}

@extend-Only Selectors
Embrace Placeholders selectors look like class and id selectors, except the # or . is replaced by %. They can be used anywhere a class or id could, and on their own they prevent rulesets from being rendered to CSS

SCSS:
%bg-image {
    width: 100%;
    background-position: center center;
    background-size: cover;
    background-repeat: no-repeat;
}
.image-one {
    @extend %bg-image;
   background-image:url("/img/image-one.jpg");
}
.image-two {
    @extend %bg-image;
    background-image:url("/img/image-two.jpg");
}

CSS after compilation:
.image-one, .image-two {
  width: 100%;
  background-position: center center;
  background-size: cover;
  background-repeat: no-repeat;
}
.image-one {
  background-image: url("/img/image-one.jpg");
}
.image-two {
  background-image: url("/img/image-two.jpg");
}

Import Directive:
By using @import you can include the external file in current scss file at the top by using the @import 'filename.scss';

Without the extensions also we can include files
@import “filename”;

For multiple import:
@import "file1", "file2";


Sass Script:
SCSS supports a small set of extensions called SassScript. SassScript allows properties to use variables, arithmetic, and extra functions
SassScript can also be used to generate selectors and property names, which is useful when writing mixins.

Variables:
$link-color: #1a99aa;

@mixin lineargradient($start, $end) {
	background-image: -moz-linear-gradient(top,$start,$end);
	background-image: -o-linear-gradient(top,$start,$end);
	background-image: -webkit-gradient(linear,0 0,0 100%,from($start),to($end));
	background-image: -webkit-linear-gradient(top,$start,$end);
	background-image: linear-gradient($start,$end);
}

a{
	color: $link-color;
}
.btn{
@include lineargradient(#ffffff,#dddddd);
}

Tips for writing SCSS:

Structure Your SCSS
Getting your site structure correct from the beginning is vital for any new scss project. Using partials allows you to break the CSS up into smaller more manageable blocks of code that are easier to maintain and develop.

Partial files are created using an underscore and are not output as separate CSS files. 

Use Sass Variables More Effectively
Variables are one of the more straightforward features of SCSS but are still on occasion used incorrectly. Creating a site-wide naming convention is essential when working with Variables. Without one, they become harder to understand and re-use.

Here are some tips for creating useful variables:

•	Don’t be to vague when naming your Variables.
•	Have and stick to a naming convention (Modular, BEM, etc.)
•	Ensure the variable use is justified.

Example:
$orange: #ffa600; 
$grey: #f3f3f3; 
$blue: #82d2e5;

$link-primary: $orange;
$link-secondary: $blue;
$link-tertiary: $grey;

$radius-button: 5px;
$radius-tab: 5px;


Limit Nesting
Overusing nested rules in SCSS can cause a lot of issues, from complex code to over-specificity and too much reliance on the HTML structure of a page. These things can cause issues further down the line and potentially increase the need for the inclusion of !important, which should generally be avoided.

Here are some golden rules for nesting:

•	Never go more then 3 levels deep.
•	Ensure the CSS output is clean and reusable.
•	Use nesting when it makes sense to, not as a default option.

Reduce Mixin Usage
A mixin is a great way to include sections of code multiple times within a site. However, including a mixin is the same as copying and pasting the styles throughout the CSS file. It creates a mass of duplicate code and can bloat your CSS file.

Embrace Placeholders
Unlike mixins, placeholders can be used multiple times without adding any duplicate code. This makes them a much friendlier option for outputting dry CSS.

Example:
%bg-image {
    width: 100%;
    background-position: center center;
    background-size: cover;
    background-repeat: no-repeat;
}
.image-one {
    @extend %bg-image;
   background-image:url("/img/image-one.jpg");
}
.image-two {
    @extend %bg-image;
    background-image:url("/img/image-two.jpg");
}

Order Your Work
Place all mixins, functions, placeholders and variables in their relevant partial file. Keeping blocks of code together will ensure they are easy to edit and reuse in the future.

Site-wide elements should be kept together in a base folder. The base folder should contain global variables such as fonts and color schemes.
</pre>

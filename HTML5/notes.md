```css
box-sizing: border-box;
```
The box-sizing property allows us to include the padding and border in an element's total width and height. 


* `#RRGGBB` in hexadecimal 
    * Min - 0, Max - ff
    * `#ff0000` - Red
    * `#00ff00` - Green
    * `#0000ff` - Blue

* To show both div's `blog-post` & `other-posts` side by side we can set width in % and use float 
```html
<div class="blog-post"></div>
<div class="other-posts"></div>

<div class="clearfix"></div>
<div class="author-box"></div>
```
```css
.blog-post {
    width: 75%;
    float: left;
    padding-right: 30px;
    position: relative;
}

.other-posts {
    width: 25%;
    float: left;
}
.clearfix:after {
    content: "";
    display: table;
    clear: both;
}
```

* ` border: 1px solid #808080;`
    * width - 1px
    * line type - solid
    * color - `#808080`
    
* Relative vs Absolute
    * All the elements by default will be having `relative` position.
    * Elements with `absolute` can be positioned anywhere we want
    

<hr>


### Rules:
#### Beautiful Typography
1. Use a font-size between 15 and 25 pixels for body text
2. Use (really) big font sizes for headlines
3. Use a line spacing between 120 and 150% of the font size
4. 45 to 90 characters per line
5. Use good fonts
6. Chose a font which reflects the look and feel you want for your website
7. Use only one font

#### Using Colors Like a Pro
1. Use only one base color
2. Use a tool if you want to use more colors
3. Use color to draw attention
4. Never use black in your design
5. Choose colors wisely

#### Working with Images
1. Put text directly on the image
2. Overlay the image
3. Put your text in a box
4. Blur the image
5. The floor fade

#### Working with icons
1. Use icons to list features/steps
2. Use icons for actions and links
3. Icons should be recognizable
4. Label your icons
5. Icons should not take a center stage
6. Use icon fonts whenever possible

#### Spacing and layout
1. Put whitespace between your elements
2. Put whitespace between your groups of elements
3. Put whitespace between you website's sections
4. Define where you want your audience to look first
5. Establish a flow that corresponds to your content's message
6. Use whitespace to build that flow

<br>

1. For body text use b/w 15 and 25 pixels.
2. More font size(90px) cut down the font weight.
3. Use line spacing(vertical distance b/w lines) b/w 120 and 150% of the font size.
4. 45 to 90 characters per line.
5. Use good fonts.
    * `Sans-serif` - More neutral, clean, simple and modern websites
    * `serif(red serifs)` - Traditional purpose, story telling and long reading.
    * some good google sans-serif fonts. 
    * examples:
        1. Open Sans
        2. Lato
        3. Raleway
        4. Monsterrat
        5. PT Sans
    * examples:
        1. Cardo
        2. Merriweather
        3. PT Serif
6. Use good colors.
    * Use only one base color
    * Use below tools:
        1. [color.adobe.com](https://color.adobe.com/create/color-wheel)
        2. [0to255](http://www.0to255.com/)
        3. [flatuicolors](http://flatuicolors.com/)
    * Use color to draw attention
    * Never use black in your design
    * Choose colors wisely, few example what feelings each color can evoke.
        1. Red - Power, passion, strength and excitement
            * Brighter tones are more energetic
            * Darker shades are more powerful and elegant
        2. Orange - cheerfulness and creativity
            * Orange draws attention without being as overpowering as red
        3. Yellow - happiness, brightness and liveliness
        4. Green - Harmony, nature, life and health also Money, Balancing and harmonizing effect
        5. Blue - Patience, peace, turstworthiness and stability
        6. Purple - Power, nobility and wealth
        7. Brown - relaxation and confidence

7. Icons
   * Icons should be recognizable
   * Label your icons
  

<hr>
To make image background cover and position center with gradient on top of image to make text overlay to visible clear
 ```css
header {
     background-image: linear-gradient(rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 0.7)), url(img/hero.jpg);
     background-size: cover;
     height: 100vh;
     background-position: center;
 }
 
.hero-text-box {
    position: absolute;
    width: 1140px;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
 ```












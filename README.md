# More About CSS

## Topics of the day.

1. CSS Resets
2. Cascading
3. Specificity weight of selectors.
4. Combining Selectors
5. Layering styles with multiple classes
6. Common CSS Property & Values
7. Colors
   - Keyword Values:
   - Hexadecimal Values
   - RGB & RGBa values
   - HSL and HSLa value
8. Lengths
   - Absolute Lengths
   - Relative Lengths

## 1. CSS Resets

We have a number of options when it comes to using a browser. We have Chrome, Safari, Opera, Firefox, etc. For a user it's fine, he/she can use any browser. But being a developer its not like that, while coding you need to take care of all the browser out there. Because every browser has default styles for different elements. For example, the way a Chrome browser will display heading elements, in a similar way safari won't. Whatever margin and padding are having for different elements inside Firefox, it may be different in opera.
Being a web developer you'll always want to target your all user. Not just the Chrome or Firefox user. You'll always want to show similar styles to all the user for your websites. To ensure cross-browser similarities CSS resets is widely used.
CSS resets takes all the element and provides unified styles for all browser. It removes all the default sizing, margin, padding and all the additional styles from the element.
There are a bunch of CSS resets, and each has their own styles. One of the most popular is Eric Meyer’s reset.

```
/* http://meyerweb.com/eric/tools/css/reset/
   v2.0 | 20110126
   License: none (public domain)
*/

html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed,
figure, figcaption, footer, header, hgroup,
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
    margin: 0;
    padding: 0;
    border: 0;
    font-size: 100%;
    font: inherit;
    vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure,
footer, header, hgroup, menu, nav, section {
    display: block;
}
body {
    line-height: 1;
}
ol, ul {
    list-style: none;
}
blockquote, q {
    quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
    content: '';
    content: none;
}
table {
    border-collapse: collapse;
    border-spacing: 0;
}
```

In Eric Meyer’s reset, it targets all the elements and provides the same styles. It brings all the element on one level. You'll find whatever the sizing a heading element has, it will be the same for the paragraph elements and for other elements also. So, after using Eric Meyer's reset you'll have to start from zero levels. Depending upon use cases you'll have target individual element and apply your own style. And now that style will be similar for all browser.
One more important point to note here, CSS is Cascading Style Sheet. So whatever styles come at the bottom or later on it has more priority. So always apply CSS reset on top of your stylesheet and then apply your own style below the reset.

## 2. Cascading

Let's see how styles are being rendered when a page is styled. While writing CSS we see that all the styles fall from top to bottom in a stylesheet. This is known as cascading. It allows us to add different styles or override the previous styles as the style sheet keeps on growing. In cascading whatever styles come at the bottom will have more priority than the earlier one. For example,

```
p {
  background: orange;
  font-size: 24px;
}
p {
  background: green;
}
```

Here, at the top we have selected the paragraph element change it's `background-color and font-size`. And again at the bottom, we selected paragraph element and change its background-color to green. When we will see the paragraph in the browser will find that the paragraph is having background `green`, and there won't be any changes in `font-size`, it will remain `24px` from the top selector. It's just because we haven't changed its font-size at the bottom selector. But for the background, we made changes at the bottom. Therefore, the green color will take precedence than orange because it is coming after orange in the stylesheet for the paragraph.
That's how the cascading style sheet works. However sometimes this cascading fails when we use the different selectors to target elements in a style sheet. Let's have a look at how specificity works when we different selectors.

## 3. Specificity weight of selectors.

Last day we have seen the three types of selectors, type, class, and ID. Each selector has a specific weight in CSS. In the specificity table, type selector has the lowest weight, class selectors has medium weight and ID selector has the highest weight. Let's have a look at the table and the point how much each selector hold.

```
  Type: 0-0-1
  Class: 0-1-0
  ID: 1-0-0
```

The important point to note here is that the ID selector has higher specificity weight than the class selector and the class selector has higher specificity weight than the type selector. It means that if an element is selected and styled in a stylesheet using these selectors, then the selector holding more specific point in the table will always get the priority. The higher the specific weight more superiority is given in the stylesheet. Let's understand this with examples.

```
  <p class="food">...</p>

  .food {
    background: green;
  }
  p {
    background: orange;
  }
```

Here, the paragraph is selected using two selectors, type as well as the `class` selector. Although the orange background comes after the background green in the cascading. But the background green will take precedence, it, because it has been applied using class selector and the class selector, is higher specific weight in the table than the type selector. Let's see one more example of using all the three selectors.

```
  <p class="food" id="bread">...</p>

  #bread {
    background: red;
  }
  .food {
    background: green;
  }
  p {
    background: orange;
  }
```

In a similar way, although the class selector and type selector are coming after the ID selector, the background of the paragraph will be red. Because the ID selector has a higher specific weight than the class and type selector. Sometimes, selectors are combined to be more specific. Its time to dig out more about the selectors and let's see how more than one selectors are combined to style an element.

## 4. Combining Selectors

We have seen how all the three selectors work individually, now let's see how they can be used together. To be very specific sometimes we combine the selectors. Let's see a few examples, how do we combine the selectors.

```
  <div class="awesome">
    <p class="child">.....</p>
    <p class="child">.....</p>
  </div>
  <section>
    <p>.....</p>
    <p>.....</p>
  </section>
```

Now, if we select the paragraph element using just type selector, it will select each and every paragraph element in the document. So to become more specific we can combine the selector.

```
  .awesome .child {
    font-size: 32px;
    color: red;
  }
```

Now, the above selector will only select the paragraph element, which will be having `awesome` class as a parent.
When selectors are combined, the rightmost selector is known as the key selector which always sits right before the opening curly braces. The key selector identifies which element will get all the styles inside the curly braces. And the selectors left to the key selector works as references. One more important to note here, if you look at the above code closely will observe that there is a space between the key selector and the reference selector. There is a purpose of the space. For example,

```
  <div class="awesome child">
    <p>.....</p>
    <p>.....</p>
  </div>
  <section>
    <p>.....</p>
    <p>.....</p>
  </section>

  .awesome.child {
    font-size: 32px;
    color: red;
  }
```

It makes a large difference between `.awesome .child` and `awesome.child`. Since there is no space it means it will select the only element which will be having both the classes `awesome` as well as `child`. But if there is no space then it will select the element having the class `child` and its parent is having the class `awesome`.

We can combine different types of selectors to target elements and to be specific on a page. We will see their power as we write different combined selectors.

## 5. Layering styles with multiple classes

In an html document, it is possible that an element can have multiple class attribute value with space separated. At the same time, we can also provide the same class attribute value to multiple elements. Let's have a look.

```
  <button class="btn btn-error">.....</button>
  <button  class="btn btn-success">.....</button>
```

Yes, we can do that. Here, `btn` class is provided for the similar properties which both the element is sharing i.e. `font-size: 16px`. And both the element is also having a different class for different properties.

```
  .btn {
    font-size: 16px;
  }
  .btn-error {
    background: red;
  }
  .btn-success {
    background: green;
  }
```

This one of the best practice of being as modular as possible. It helps in not to repeat yourself again and again for similar properties. It also helps in keeping the specificity weight of the selectors low.
In the beginning, it may feel confusing and it will take time to fully understand it, but with the time and practice, it will get easier and better.

## 6. Common CSS Property & Values

We have been using different properties and values in CSS from the beginning. For applying color we say the color name like `red, blue, green`, etc. Also for applying length, we say values in `pixel(px)`.
In this section mostly we will discuss what are the different values for color and length measurements can be applied.

## 7. Colors

Primarily there are four ways to apply color within CSS: `Keywords, hexadecimal, RGB and HSL` values. Probably we all know that all the colors are a combination of `RGB(red, green, blue)`. So all the four ways are the just the representation of RGB colors. By mixing different shades of RGB colors we can create millions of colors.
Let's discuss all these four ways one by one.

### Keyword Values:

We have been using this approach from the beginning. Keyword values are just to say the name of color which you want to set within CSS. For example, `red, blue, green, black, gray`, etc there are a lot more keyword values which we can apply.

```
  .pending {
    background: orange;
  }
  .success {
    background: green;
  }
```

Although it seems simple to use keyword values, it may get difficult to remember the name of all the colors. That's why we have other options also like hexadecimal, RGB, and HSL.

### Hexadecimal Values

The hexadecimal values are represented in three or six characters and the value always consist `pound or hash (#)` at the beginning. For example,

```
  .pending {
    background: #FF6600;
  }
  .success {
    background: #008000;
  }
```

The first two characters represent red, the third and fourth characters represent green color and the last two characters represent blue color. The character can the numbers 0 through 9 and letters a through f, upper or lower cases. With this combination, we have millions of hexadecimal colors.
Here one thing more we can do that if the first two characters are matching, third and four are matching and the last two characters are matching then instead of six we can represent the color in three characters.

```
.pending {
	background: #F60;
}
```

### RGB & RGBa values:

#### RGB

The RGB colors and are represented with function `rgb()` which stands for red, green and blue colors.

```
.pending {
  background: rgb(255,102,0);
}
.success {
  background: rgb(0, 128, 0);
}
```

It accepts three values in integer with comma separated. The first value represents the red, second green and last value represents blue color. And value can be anything from 0 to 255.

#### RGBa

The RGBa values are represented with function `rgba()`. It's just we are adding alpha values to RGB colors. In RGBa color the last value is alpha values, which must be a number between 0 to 1, it can be decimal. Mostly RGBa colors are defined to provide some transparency to the colors.
If the alpha value is 0 it means the color will be fully transparent means invisible or if the value is 1 then the color will be fully opaque. And if the value is in between 0 to 1 then the color will have some transparency depending upon the value. For example, suppose we want to provide 50% transparency to the background for the pending class.

```
  pending {
    background: rgba(255,102,0, 0.5);
  }
  .success {
    background: rgba(0, 128, 0, 1);
  }
```

### HSL and HSLa value:

#### HSL

HSL colors are represented by `hsl()` function which stands or hue, saturation and lightness.

```
  pending {
    background: hsl(24,100%,50%);
  }
  .success {
    background: hsl(120, 100%, 25.1%);
  }
```

The first value accepts the number between 0 to 360 which identifies the degree of color on the color wheel. The number 0 through 360 represents the color wheel.
The second and third value accept the value in percentage between 0 to 100%. The second value is for saturation of the color, where 0 is the grayscale and 100% means fully saturated. And the last value is for the lightness of the color, where 0 means fully black and 100% means fully white.

#### HSLa

As in RGBa value, 'a' represents alpha values which decide the transparency of the color. In a similar way in we can also add alpha value in HSL color, which is represented by function `hsla()`. The alpha value accepts the number between 0 to 1, where 0 means fully transparent and 1 means fully opaque.

```
  pending {
    background: hsla(24,100%,50%, 0.5);
  }
  .success {
    background: hsla(120, 100, 25.1, 1);
  }
```

We have seen all the ways to apply the value of the color. The most widely and accepted value is the hexadecimal and RGB values. It gives us a wide range of option and supported by almost every browser. The HSL values also give a wide range but as it is the newest color so it is not widely used and accepted by every browser.

## 8. Lengths

Now its time to discuss the what are the ways to define length values in CSS. We have been `pixel(px)` values, is one of the ways to define length. But as color similarly there are also other ways to define the length values.
The length values are categorized into two categories. One is Absolute length and another is Relative length.

### Absolute Lengths

One of the simplest length values used in CSS is the Absolute length. Few absolute lengths are pixel, centimeters, inches, etc. The absolute lengths are always fixed. Whatever the value is defined, it will always remain fixed, unlike relative lengths. It won't respond as the size of the screen increases or decreases.
One of the most common and widely used absolute lengths is pixel(px).

```
  p {
    font-size: 16px;
  }
```

### Relative Lengths

The relative lengths are different from the absolute lengths as they are not the fixed unit. It relies on other units of measurement. The most common relative units are `percentages, EM, REM`.

```
  .col {
    width: 100%;
  }
  .heading {
    font-size: 2em;
  }
  p {
    font-size: 1rem;
  }
```

I am not going in details of relative lengths here, just introducing you with all these types of relative units. But yeah, we will discuss all these relative units in detail once we reach to responsive web design part in HTML & CSS. So mostly relative lengths are used to make the layout responsive for every device.

## Answer the following questions

1. Why do we use CSS reset? And where it should come in the cascading?
2. Order the selectors in ascending order according to their specificity weights?
3. What are the different ways to apply color value in CSS?
4. What are the different ways to apply length measurement in CSS?
5. REM is a relative unit or absolute unit? Why?
6. How do we apply transparency to the color?

## Do the exercise1

## Additional Resources

1. https://learn.shayhowe.com/html-css/getting-to-know-css/

- https://internetingishard.com/html-and-css/hello-css/

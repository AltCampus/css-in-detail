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

## 3. CSS Resets

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

## 4. Cascading

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

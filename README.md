## This is my personal website
Sorry if it's too simple !


### Optimising with cache

A very simple solution to manage cache is by defining a `expires` http header, and using a long expiration date. This ensures the browser will cache static assets. But you now have to versionise these assets. This is why you will find `style2.css` and `m_roubaud1.jpeg`. The html is never cached (or very short term) so you manage automatic updates.
With an Apache server, you can use a `.htaccess` file within your source code:

```apache
    ExpiresByType image/jpg "access plus 13 month"
```


### Responsive design, mobile first

The CSS defines default properties, used for mobiles. Then I define the style for desktops, using media queries. This is a mobile first approach, the desktop styles being more complex but running on a more powerful CPU. Here the breaking point has a pretty random value, depending on your UI.

```css
@media screen and (min-width: 769px) {
    header {
        position: initial;
        padding: 0 10px;
    }
```



### Dark/light themes
This is how I manage the themes : 

- define a default palette using CSS variables:
```css
:root {
    --bg-color: #FFF;
    --primary-color: #3c3752;
}
```

- define an alternative palette for dark theme, this media query follows the browser or OS theme:

```css
@media (prefers-color-scheme: dark) {
    :root {
        --bg-color: #201d2c;
        --primary-color: #FFF;
    }
}
```

- use these variables in your styles:

```css
body {
    margin: 0;
    padding: 0;
    background-color: var(--bg-color);
    color: var(--primary-color);
    font-family: helvetica;
    font-size: 17px;
}
```


### Accessibility (a11y)
I attach a great importance to accessibility. For me it is the new challenge of the web.
There are different rules, one simple and basic is about contrast ratios and text sizes-and it can be very challenging!.
Another is about assistive tools and keyboard usability. So it is important to have a `skip to content` link. See https://css-tricks.com/how-to-create-a-skip-to-content-link/ for how to.

Tools for testing the accessibility of your website : https://accessibe.com/accessscan?website=https://www.roubaud.org/

Another important rule is to enable zoom in your website, this simple meta makes it possible:
```html
<meta name="viewport" content="width=device-width" />
```
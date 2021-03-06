# ani-cursor

A library for rendering Windows Animated Cursor files (`.ani`) in the browser by parsing out the individual frames and constructing a CSS animation.

Built to support `.ani` files in Winamp skins for https://webamp.org.

I wrote a blog post about this library which you can find [here](https://www.notion.so/jordaneldredge/Rendering-Animated-ani-Cursors-in-the-Browser-363bfd3b37044bb192bfbe55739a8c2c).

## Install

```bash
yarn add ani-cursor
```

or

```bash
npm install ani-cursor
```

## Usage Example

```JavaScript
import {convertAniBinaryToCSS} from 'ani-cursor';

async function applyCursor(selector, aniUrl) {
    const response = await fetch(aniUrl);
    const data = new Uint8Array(await response.arrayBuffer());

    const style = document.createElement('style');
    style.innerText = convertAniBinaryToCSS(selector, data);

    document.head.appendChild(style);
}

const h1 = document.createElement('h1');
h1.id = 'pizza';
h1.innerText = 'Pizza Time!';
document.body.appendChild(h1);

applyCursor("#pizza", "https://archive.org/cors/tucows_169906_Pizza_cursor/pizza.ani");
```
# Lazy loading images

Lazy loading images is a technique that defers loading offscreen images until
the user scrolls near them. This saves bandwidth and improves performance.

A basic lazy loading can be done with the `loading="lazy"` attribute on the
image

```html
<img src="image.jpg" loading="lazy" />
```

The downside is that the user will see a blank space where the image should be
until the image is downloaded. To fix this we can use a blurred placeholder
image that are shown until the full image is downloaded.

Use this command to create a blurred placeholder image

```bash
ffmpeg -i imageName.jpg -vf scale=20:-1 imageName-small.jpg
```

This will generate a placeholder image that is 20 pixels wide and the height
will be automatically calculated to maintain the aspect ratio of the original
image.

The next step is to create a div and set the background image of that div to our
super small image. This will be the placeholder image that is shown until the
full image is downloaded. We can add a pulsing animation to the placeholder
image. This will make it even more obvious that the image is loading. The code
will look something like this.

```html
<div class="blurred-img">
  <img src="imageName.jpg" loading="lazy" />
</div>
```

```js
const blurredImageDiv = document.querySelector('.blurred-image')
const img = blurredImageDiv.querySelector('img')
function loaded() {
  blurredImageDiv.classList.add('loaded')
}

if (img.complete) {
  loaded()
} else {
  img.addEventListener('load', loaded)
}
```

```css
.blurred-img {
  background-repeat: no-repeat;
  background-size: cover;
  filter: blur(10px);
}

.blurred-img::before {
  content: '';
  position: absolute;
  inset: 0;
  opacity: 0;
  animation: pulse 2.5s infinite;
  background-color: var(--text-color);
}

@keyframes pulse {
  0% {
    opacity: 0;
  }
  50% {
    opacity: 0.1;
  }
  100% {
    opacity: 0;
  }
}

.blurred-img.loaded::before {
  animation: none;
  content: none;
}

.blurred-img img {
  opacity: 0;
  transition: opacity 250ms ease-in-out;
}

.blurred-img.loaded img {
  opacity: 1;
}
```

More info:

[Speed Up Your Site Instantly With Lazy Loaded Images - Advanced Lazy Loading](https://blog.webdevsimplified.com/2023-05/lazy-load-images/)

# Responsive images 101

Responsive images have two major use cases: resolution switching and art
direction.

## Resolution switching

Resolution switching is the most common use case. It refers to any scenario
where you all you want to do is provide different sizes of an image and you’re
not making any modifications to the content or aspect ratio of the image.

![](https://cloudfour.com/wp-content/uploads/2020/03/summary.png)

## Art direction

Whenever you need to make changes to content or aspect ratio of an image based
on the size of the image in the page, you’re doing art direction. The most
common place I see art direction is for images that contain text. The `picture`
element—the media attribute in particular—is designed to make art direction
easy.

## ![](https://cloudfour.com/wp-content/uploads/2015/03/picture-syntax.png)

## Changing image sizes, high-DPI images, different image types & art direction use case

```html
<picture>
  <source
    media="(min-width: 1280px)"
    sizes="50vw"
    srcset="
      opera-fullshot-200.webp   200w,
      opera-fullshot-400.webp   400w,
      opera-fullshot-800.webp   800w,
      opera-fullshot-1200.webp 1200w,
      opera-fullshot-1600.webp 1600w,
      opera-fullshot-2000.webp 2000w
    "
    type="image/webp"
  />
  <source
    sizes="(min-width: 640px) 60vw, 100vw"
    srcset="
      opera-closeup-200.webp   200w,
      opera-closeup-400.webp   400w,
      opera-closeup-800.webp   800w,
      opera-closeup-1200.webp 1200w,
      opera-closeup-1600.webp 1600w,
      opera-closeup-2000.webp 2000w
    "
    type="image/webp"
  />
  <source
    media="(min-width: 1280px)"
    sizes="50vw"
    srcset="
      opera-fullshot-200.jpg   200w,
      opera-fullshot-400.jpg   400w,
      opera-fullshot-800.jpg   800w,
      opera-fullshot-1200.jpg 1200w,
      opera-fullshot-1600.jpg 1800w,
      opera-fullshot-2000.jpg 2000w
    "
  />
  <img
    src="opera-closeup-400.jpg"
    alt="The Oslo Opera House"
    sizes="(min-width: 640px) 60vw, 100vw"
    srcset="
      opera-closeup-200.jpg   200w,
      opera-closeup-400.jpg   400w,
      opera-closeup-800.jpg   800w,
      opera-closeup-1200.jpg 1200w,
      opera-closeup-1600.jpg 1600w,
      opera-closeup-2000.jpg 2000w
    "
  />
</picture>
```

**Explanation:**

For browser windows with a width of 1280 CSS pixels and wider, a full-shot photo
with a width of 50% of the viewport width is used; for browser windows with a
width of 640-1279 CSS pixels, a photo with a width of 60% of the viewport width
is used; for less wide browser windows, a photo with a width that is equal to
the full viewport width is used. In each case, the browser picks the optional
image from a selection of images with widths of 200px, 400px, 800px, 1200px,
1600px and 2000px, keeping in mind image width and screen DPI. These photos are
served as WebP to browsers that support it; other browsers get JPG.

---

Utils:

Linter for Responsive Images -
[https://ausi.github.io/respimagelint/](https://ausi.github.io/respimagelint/)

---

More info:

[Responsive Images the Simple Way](https://cloudfour.com/thinks/responsive-images-the-simple-way/)

[Responsive Images 101](https://cloudfour.com/thinks/responsive-images-101-definitions/)

[Responsive Images: Use Cases and Documented Code Snippets to Get You Started](https://dev.opera.com/articles/responsive-images/)

[The anatomy of responsive images](https://jakearchibald.com/2015/anatomy-of-responsive-images/)

[Halve the size of images by optimising for high density displays](https://jakearchibald.com/2021/serving-sharp-images-to-high-density-screens/)

[The modern way of serving images](https://kurtextrem.de/posts/modern-way-of-img)

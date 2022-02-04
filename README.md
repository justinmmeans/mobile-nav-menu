# phillycommunitywireless.org

Source code for the Philly Community Wireless website, [phillycommunitywireless.org](https://phillycommunitywireless.org) (or [pcw.fi](https://phillycommunitywireless.org)). The site is built using the [Hugo](https://gohugo.io) static site generator and hosted with [GitHub Pages](https://pages.github.com/).

# Theme

The site's theme is a fork of [gohugo-theme-ananke](https://github.com/theNewDynamic/gohugo-theme-ananke) with major modifications.

## Custom CSS

Custom CSS lives in `/assets/pcw-hugo-theme/css/custom.css` 

## Segments

This theme supports a `segments` front matter parameter for all normal pages, which allows for composing layouts from "stackable components". The `segments` param is a YAML list of objects, each of which will correspond to one of these components. Each type of segment uses a pre-written HTML template to render a component, like a full-width photo, a video, or a call-to-action, to the page it's used on. Segments are all full-width and can usually be customized right from the YAML.

### Example

Here is an example of some typical [Hugo front matter](https://gohugo.io/content-management/front-matter/), along with the `segments` param. This would render a single full-width image followed by a volunteering call-to-action:

```yml
---
title: Home
segments:
  - type: image
    src: images/antenna.jpg
    alt: An image of an antenna mounted on a brick wall.
  - type: call-to-action
    text: Volunteer!
    link:
      href: https://example.com/volunteer
      text: Get involved
---
```

### Segment types

A segment consists of a `type` string that determines which HTML template is used, as well as a series of other mandatory and optional params to serve as props/options for the component. These are the currently supported types:

#### `markdown`
A section of markdown text.
```yml
- type: markdown
  url: The url of the markdown file, relative to your content directory.
  # Optional
  class: Classes (space separated) to add to the container element. Useful for e.g. font settings, background color, etc.
```

#### `heading`
A simple full-width heading (`h1`).
```yml
- type: heading
  text: The text to display in the heading.
  # Optional
  divider: false # Set to `true` to display a dotted divider above the heading. 
```

#### `image`
A full-width responsive image.
```yml
- type: image
  src: Image source
  alt: Alt text
  # Optional
  class: Classes to add to the <img> element.
```
<!--
### `gallery`
A layout of up to 6 images
```yml
- type: gallery
  images:
    - src: First image source
      alt: First image alt text
    - src: Second image source
      alt: Second image alt text
    - src: Third image source
      alt: Third image alt text
      ... Can include up to 6
  # Optional
  class: Classes to add to the container element.
```
-->
#### `video`
A full-width responsive embedded video.
```yml
- type: image
  src: Image source
  title: Title of the video (mandatory)
  # Optional
  class: Classes to add to the container element.
```

#### `call-to-action`
A highlighted section with (optionally) a header and some text, followed by a big visible link.

```yml
- type: call-to-action
  text: Text to display above the link. Markdown can be used here (but not shortcodes).
  link:
    href: The URL the link should point to.
    text: The text to display on the link.
  # Optional
  heading: A heading above the text.
  class: Classes to add to the container element.
```
![A screenshot of the call-to-action template on a website.](./assets/readme/call-to-action.png)


#### `call-to-action-image`
Same as above, but split vertically with an image on the right side. 
```yml
- type: call-to-action-image
  # Same as above, with the addition of:
  image:
    src: Image source
    alt: Image alt text
  # Optional
  reverse: false # Set to `true` to display the image on the left instead.
```
![A screenshot of the call-to-action-image template on a website.](./assets/readme/call-to-action-image.png)

#### `icons`
A responsive layout featuring three font-awesome icons with optional text labels. Supports [Font Awesome 5](https://fontawesome.com/v5.0/icons) icons.
```yml
- type: icons
  icons:
    - icon: fas fa-example-1 # The Font Awesome class for your icon.
      text: Label text 1
    - icon: fas fa-example-2
      text: Label text 2
    - icon: fas fa-example-3
      text: Label text 3
  # Optional
  class: Classes to add to the container element.
```

![A screenshot of the call-to-action-image template on a website.](./assets/readme/icons.png)

### Adding new segment types

You can create a new segment type by creating a `<type-name>.html` file in the `theme/pcw-hugo-theme/layouts/partials/segments` directory. This template will automatically be used to render segments with this title. The [context](https://gohugo.io/content-management/front-matter/) passed to the partial will be the segment object from the YAML (you can access the global site variable as `site`).

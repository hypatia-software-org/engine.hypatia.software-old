---
title: Contributing to the website
---

This page is a work in progress.

## Image gallery

To add an image to the image gallery, place the image in the `assets/` folder, and then edit the `_data/gallery.yml` file, adding the following data:

```
-
  image: /assets/your_image.png
  title: Image Title
  desc: Image Description (optional)
```

## Wiki pages

The wiki is stored in the `wiki/` subfolder. Wiki pages are individual Markdown files in this folder.

The wiki's sidebar is stored in the `_includes/wiki_sidebar.html` file, and editing this lets you add pages to the sidebar.

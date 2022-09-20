# no style, please!
## Notes On Usage

You can edit `_config.yml` file to customize your blog. You can change things such as the name of the blog, the author, the appearance of the theme (light, dark or auto), how dates are formatted, etc. Customizable fields should be straightforward to understand. Still, `_config.yml` contains some comments to help you understand what each field does.

For further customization (e.g. layout, CSS) see the [official Jekyll's documentation](https://jekyllrb.com/docs/themes/#overriding-theme-defaults) on customizing gem-based themes.

### Customize the menu

In order to add/edit/delete entries from the main menu, you have to edit the `menu.yml` file inside `_data` folder. Through that file you can define the structure of the menu. Take a look at the default configuration to get an idea of how it works and read on for a more comprehensive explanation.

The `menu.yml` file accepts the following fields:

- `entries` define a new unordered list that will contain menu entries
- each entry is marked by a `-` at the beginning of the line
- each entry can have the following attributes:
    - `title`, which defines the text to render for this menu entry (**NB: you can also specify HTML!**)
    - `url`, which can be used to specify an URL for this entry. If not specified, `title` will be rendered as-is; otherwise `title` will be sorrounded by a link tag pointing to the specified URL. Note that the URL can either be relative or absolute. Also note that you can get the same result by placing an ```<a>``` tag in the `title` field.
    - `post_list`, which can be set either to `true` or to an object. If it is true, the entry will have a list of all posts as subentries. This is used to render your post list. If you want to customize which posts to render (e.g. by category), you can add one or more of the following attributes under `post_list`:
        - `category`, which can be set to a string. It is used to render a list of posts of the specified category only. If you don't set it, then posts of all categories will be rendered.
        - `limit`, which can be set to a number. It specifies the number of posts to show. If not set, all posts will be rendered.
        - `show_more`, which can be true. If it is true and if the number of posts to show is greater than the specified `limit`, render a link to another page. To specify the URL and the text of the link, you can set `show_more_url` and `show_more_text` attributes, which are documented below.
        - `show_more_url`, which can be a string. It specifies the URL for the show more link. Use only if `show_more` is true. This will usually redirect to a page containing all posts, which you can easily create using an archive page (see [create archive pages](#create-archive-pages) section)
        - `show_more_text`, which can be a string. It specifies the text for the show more link. Use only if `show_more` is true.
    - `entries`, yes, you can have entries inside entries. In this way you can create nested sublists!

### Create archive pages

A so-called archive page is a page that shows a list of posts (see [this](https://riggraz.dev/no-style-please/all-posts) for an example). You can create an archive page by creating a page and putting the following frontmatter:

```
---
layout: archive
title: The title of the page here
which_category: name-of-category
---
```

`which_category` is optional: if you don't put it, then all posts of the blog will be listed; on the other hand, if you specify a category, only posts of that category will be shown.

This feature is particularly useful if used together with the `show_more` attribute in the menu. For example, if you want to limit the number of posts shown in the home page to 5 but add a link to view them all, then you can create an archive page using the method showed above and link to it using the `show_more_url` attribute in `menu.yml`. See [this example](https://github.com/riggraz/no-style-please/blob/master/_data/menu.yml) if you're in doubt.

### Customize the index page

The `index.md` page should use layout `home`, which is the layout that displays the menu. If you want to have some content after the menu, you can just add that content in the `index.md` file, and it will automatically show under the menu.

Another thing you can do to customize the index page is show the description of your blog between the title and the menu. To do this, just edit `_config.yml` and change `theme_config.show_description` to `true`.

#### Dark mode for images

This theme provides dark mode by inverting all colors of light mode throught the CSS `invert()` function. This approach would also invert the color of all images, but, since this is not the behaviour one would expect, images are not inverted by default.

However, if you would like to force the color inversion on a specific image you can do so by applying `class="ioda"` to that image ("ioda" stands for "invert on dark appearance"). See the image in the [overview post](https://github.com/riggraz/no-style-please/blob/master/_posts/2020-07-07-overview-post.md) for an example of this approach. Note that color inversion will take place only when the theme has dark appearance!

For example, if you have a black and white image it could make sense to invert it in dark mode. On the other hand, a colorful image will probably look bad if inverted.

## Credits

Inspired by elly's site, http://tilde.town/~elly/
Themed by riggraz, https://github.com/riggraz/no-style-please


## License

The theme is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).


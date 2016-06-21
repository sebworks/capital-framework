The cf-pagination component provides a responsive approach to multipage page navigation.


## Dependencies
- cf-core
- cf-buttons
- cf-icons


## Variables

Theme variables for setting the color and sizes. Color variables are from 18F's [US Web Design Standards](https://github.com/18F/web-design-standards/blob/18f-pages-staging/src/stylesheets/core/_variables.scss). Overwrite them in your own project by duplicating the variable `@key: value`.


### Color variables

Pagination text color.
```
@pagination-text-color: #75787B;
```

Pagination form background color.
```
@pagination-bg-color:   #F0F1F1;
```


### Sizing variables

The font size of pagination text.
```
@pagination-font-size__px:          16px;
```


## Default pagination

Default pagination consists of "Previous" and "Next" links, styled as buttons, and an inline form (input, submit button) that allows users to navigate to specific pages by number.

To enable the component to jump directly to the paginated content, place `#pagination_content` directly above your paginated content.

### Example
<div id="o-filterable-list-controls"></div>

<!-- Paginated content here -->

<nav class="m-pagination" role="navigation" aria-label="Pagination">
    <a class="btn
              btn__super
              m-pagination_btn-prev"
       href="?page=1#o-filterable-list-controls">
        <span class="cf-icon cf-icon-left btn_icon__left "></span>
        Newer
    </a>
    <a class="btn
             btn__super
             m-pagination_btn-next"
       href="?page=3#o-filterable-list-controls">
        Older
        <span class="cf-icon cf-icon-right btn_icon__right"></span>
    </a>
    <form action="#o-filterable-list-controls">
        <label for="m-pagination_current-page">
            Page
            <span class="u-visually-hidden">
                number 2 out of 149 total pages
            </span>
        </label>
        <input id="m-pagination_current-page" name="page" type="number" min="1" max="2" pattern="[0-9]*" inputmode="numeric" value="1">
        <span class="m-pagination_label">
            of 149
        </span>
        <button class="btn btn__link" id="m-pagination_submit-btn" type="submit">
            Go
        </button>
    </form>
</nav>

### Markup

```
<div id="o-filterable-list-controls"></div>

<!-- Paginated content here -->

<nav class="m-pagination" role="navigation" aria-label="Pagination">
    <a class="btn
              btn__super
              m-pagination_btn-prev"
        href="?page=1#o-filterable-list-controls">
        <span class="cf-icon cf-icon-left btn_icon__left "></span>
        Newer
    </a>
    <a class="btn
              btn__super
              m-pagination_btn-next"
       href="?page=3#o-filterable-list-controls">
        Older
        <span class="cf-icon cf-icon-right btn_icon__right"></span>
    </a>
    <form action="#o-filterable-list-controls">
        <label for="m-pagination_current-page">
            Page
            <span class="u-visually-hidden">
                number 2 out of 149 total pages
            </span>
        </label>
        <input id="m-pagination_current-page" name="page" type="number" min="1" max="2" pattern="[0-9]*" inputmode="numeric" value="1">
        <span class="m-pagination_label">
            of 149
        </span>
        <button class="btn btn__link" id="m-pagination_submit-btn" type="submit">
            Go
        </button>
    </form>
</nav>
```

## Responsive behavior

- `@bp-xs-max`: On small screens, the pagination links display next to each other, stacked on top of the form.

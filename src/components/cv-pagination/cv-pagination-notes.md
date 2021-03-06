# cv-pagination

A Vue implementation of a Carbon Components pagination

http://www.carbondesignsystem.com/components/pagination/code

## Usage

```html
<cv-pagination
  backwards-text="Previous page"
  forwards-text="Next page"
  page-number-label="Page number"
  page-sizes-label="Number of items per page:"
  :number-of-items="103"
  :page-sizes="[10, { value: 20, selected: true }, 30, 40, 50]"
  @change="onChange"
></cv-pagination>
```

Minimal
<cv-pagination>

## Attributes

- backwards-text: Aria label on page down arrow. Optional defaults to "Previous page"
- forwards-text: Aria label on page up arrow. Optional defaults to "Next page"
- page-number-label: Hidden label for page number select. Defaults to "Page number"
- page-sizes-label: label for page size select. Defaults to "Number of items per page:"
- number-of-items: Number of items accross all pages, defaults to Infinity
- page-sizes: Array of page size values.
  Defaults to [10, 20, 30, 40, 50]
  - By default the first page size is selected. This can be augmented by passing an object instead of a number e.g.
    [10, { value: 20, selected: true }, 30, 40, 50]

Methods
value: returns object indicating the start and length of the page - { start, length }

## Events

Change - Contains value - { start, length }

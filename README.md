# Sass Basic

## Color palette

### [Default Page](https://neczpal.github.io/scss-color-palette/)

### [Colorful Page](https://neczpal.github.io/scss-color-palette/index-colorful.html)

### [Monochrome Page](https://neczpal.github.io/scss-color-palette/index-monochrome.html)

### How to Build

* #### Install sass `npm install -g sass`

* `npm run build` - Builds the [`style.scss`](https://github.com/neczpal/scss-color-palette/blob/master/src/scss/style.scss)

### How to Run

* Open the index.html in `dist/index.html`

### MAP OPERATIONS

```SCSS
$colors: (
        success: green,
        warning: orange,
        danger: red
);

$base-colors: (
        black: black,
        white: white
);
```

* `map.get($map: $colors, $key: success)` => `green`
* `map.has-key($map: $colors, $key: success)` => `true`
* `map.keys($map: $colors)` => `success, warning, danger`
* `map.merge($colors, $base-colors)` => `(success: green, warning: orange, danger: red, black: black, white: white)`
* `map.remove($colors, success)` => `(warning: orange, danger: red)`
* `$colors` => `(success: green, warning: orange, danger: red)`

### LIST OPERATIONS

```SCSS
$padding: 0.5rem, 1rem, 2rem;
```

* `list.nth($padding, 2)` => `1rem`
* `list.append($padding, 3rem)` => `0.5rem, 1rem, 2rem, 3rem`
* `list.length($padding)` => `3`
* `list.separator($padding)` => `comma`
* `list.join($padding, (4rem, 5rem))` => `0.5rem, 1rem, 2rem, 4rem, 5rem`
* `list.index($padding, 2rem)` => `3`

### FUNCTION EXAMPLES

```SCSS
@function sum($a: 0, $b: 0) {
  @if type-of($a) != number {
    @error "First number is not a number";
  }
  @if type-of($b) != number {
    @error "Second number is not a number";
  }

  @return $a + $b;
}
```

* `sum(1, 2)` => `3`
* `sum(1)` => `1`

```SCSS
@use "sass:list";
@function sum2($numbers...) {
  $sum: 0;
  @for $i from 1 through list.length($numbers) {
    $value: list.nth($numbers, $i);
    @if type-of($value) != number {
      @error "The " + $i + "th element: '"+ $value + "' is not a number!";
    }
    $sum: $sum + $value;
  }

  @return $sum;
}
```

* `sum2(1, 1, 2, 3, 5)` => `12`

```SCSS
@use "sass:list";
@function splice($list, $start, $count: 1) {
  $length: list.length($list);

  @if ($length < $start) {
    @error "Element not exists!";
  }

  $new-list: ();
  $end: $start + $count;
  @for $i from 1 through $length {
    @if ($start > $i or $i >= $end) {
      $new-list: list.append($new-list, list.nth($list, $i));
    }
  }

  @return $new-list;
}
```
```SCSS
$list: 2, 3, 4, 5;
```

* `splice($list, 2, 2)` => `2 5`

### Documentation

* [list](https://sass-lang.com/documentation/values/lists)
* [map](https://sass-lang.com/documentation/values/maps)
* [@function](https://sass-lang.com/documentation/at-rules/function)

### Further resources

* #### [Sass playground](https://www.sassmeister.com/)
* #### [Sass documentation](https://sass-lang.com/documentation)
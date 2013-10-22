![Custom Grid System](https://raw.github.com/luizgamabh/custom.gs/master/assets/img/logo.png)

Custom Grid System is a new Sass (and Less ASAP) based grid system that combines best practices of:

* [Grid960](http://960.gs)
* [Bootstrap](http://getbootstrap.com)
* [Unsemantic](http://unsemantic.com)
* [Semantic](http://semantic.gs)

Custom.gs works with columns rather than percentages, anyway you can set-up many columns as you need.

## How it works?

### UNSEMANTIC MODE

Let's look at `custom.sass` file:
```sass
$semantic: false
```

```html
<div id="main" class="container_52">
    <section class="grid_32">
        First column
    </section>
    <aside class="grid_20">
        Second Column
    </aside>
</div>
```

### SEMANTIC MODE (same result without many classes messing your code)

`custom.sass`
```sass
$semantic: true
```

`my_website.sass`:
```sass
@import "custom"

div#main
  +container_52

section
  +grid_32

aside
  +grid_20
```

```html
<div id="main">
    <section>
        First column
    </section>
    <aside>
        Second column
    </aside>
</div>
```

## Information

### Option variables:

* `$semantic`: boolean, default: true. Description: Generates (if false) or not (if true, semantic mode) css classes.
* `$container-max-width`: measure in px. Description: Max width of container
* `$base-resolution`: measure in px. Description: Container max width will get 100% from this resolution
* `$number-of-columns`: integer. Description: Grid columns amount
* `$gutter`: measure in px. Description: Space between columns
* `$fixed-gutter`: boolean, default: true Description: Gutter will not resize within fluid columns
* `$ie7-support`: boolean, default: true. Description: Supports wtf IE7- version


## Recomendations

### Increase the accuracy of the relative measures

It is highly recommended that you work with precision when dealing with measures. At your `compass.rb` or `config.rb` file, add the following line:

```ruby
Sass::Script::Number.precision = 10
```
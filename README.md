![Custom Grid System](https://raw.github.com/luizgamabh/custom.gs/master/assets/img/logo.png)
# [http://custom.gs](http://custom.gs)

Custom Grid System is a new Sass (and Less ASAP) based grid system that combines best practices of:

* [Grid960](http://960.gs)
* [Bootstrap](http://getbootstrap.com)
* [Unsemantic](http://unsemantic.com)
* [Semantic](http://semantic.gs)

Custom.gs works with columns rather than percentages, anyway you can set-up many columns as you need.

## How it works?

> **There are two types of people:** Those that use semantic grid and those that do not.

### Unsemantic way (for wimps)

Let's look at `custom.sass` example:
```sass
$semantic: false
$number-of-columns: 10
```

So, our `page.html` can be:
```html
<main class="main" class="container_10">
    <section class="grid_6">
        Bolinha
    </section>
    <aside class="grid_4">
        Second Column
    </aside>
</main>
```

### Semantic way (for fuckers)

Same result without many classes messing your code. This is our `custom.sass`:
```sass
$semantic: true
$number-of-columns: 10
```

`your_nice_component.sass`:
```sass
@import "custom"

.main
  +container(10)

section
  +grid(6)

aside
  +grid(4)
```

```html
<main class="main">
    <section>
        First column
    </section>
    <aside>
        Second column
    </aside>
</main>
```

### NESTED GRIDS

`Unsemantic`:
```html
<div class="grid_10 grid_parent">
    <div class="grid_5"></div>
    <div class="grid_5"></div>
</div>
```

`Semantic`:
```sass
.parent
  +grid(5)
  +grid_parent
  .nested
    +grid(5)
```

## Information

### Option variables:

* `$base-resolution`: measure in px (>= $container-max-width). **Container width will get a percent from this resolution**
* `$container-max-width`: measure in px. **Container max width**
* `$min-resolution`: measure in px or ++false++. **Defines (or not) a minimum container width**
* `$number-of-columns`: integer. **Grid columns amount**
* `$fluid`: boolean. **Fluid columns? If true grid will be responsive, else not!**
* `$gutter`: measure in px. **Space between columns**
* `$fixed-gutter`: boolean. **If true, gutter width will not squeeze when using fluid columns**
* `$semantic`: boolean. **It true do not generate many classes. Please say true :D**

### Mixins:

#### +container( [ $clear: false ] )
Defines your container

###### Optional params
`$clear`: Default: **false** | Clear the container (can be used to disable the container in some breakpoint).

Example:
```sass
.main
  +container
@media only screen and (max-width: 768px)
  .main
    +container(true)
```

#### +grid( $columns, [ $context: $number-of-columns, $options ] )
Defines your grid column

###### Mandatory params
`$columns`: number of columns (integer)

###### Optional params
`$context`: Default: **$number-of-columns** | Defines a new reference overwriting the $number-of-columns just for this specific element.

###### Helper options
`'direction'`: 'ltr'
`'gutter'`: measure in px. Change the default gutter size.
`'clear'`: boolean. If true add a `clear: left` for nth-child(xn+1) columns of your grid preventing shoddy breaks.
`'release'`: false. Release the `clear: left` for nth-child(xn+1)

Examples:
```sass
.main
  +container
  .contents
    +grid(6)
    +grid_parent
    .gallery__list-item
      +grid(1, 4, ('clear': true))
  .side
    +grid(4)
```

#### +prefix( $left, [ $context: $number-of-columns ] )
Insert empty space before a grid unit.

###### Mandatory params
`$left`: integer | Add x columns (just blank space) on left of your element.

###### Optional params
`$context`: integer | Defines a new reference overwriting the $number-of-columns just for this specific element.

Example:
```sass
.my_indented_element
  +left(1)
  +grid(9)
```

#### +suffix( $right, [ $context: $number-of-columns ] )
Insert empty space before a grid unit.

###### Mandatory params
`$right`: integer | Add x columns (just blank space) on right of your element.

###### Optional params
`$context`: integer | Defines a new reference overwriting the $number-of-columns just for this specific element.

Example:
```sass
.my_indented_element
  +right(1)
  +grid(9)
```

#### +push( $left )
Rearrange element position.

###### Mandatory params
`$left`: integer | Repositions the element x grid columns right.

Example:
```sass
.send_me_to_right
  +grid(5)
  +push(5)
```

#### +pull( $right )
Rearrange element position.

###### Mandatory params
`$left`: integer | Repositions the element x grid columns left.

Example:
```sass
.send_me_to_left
  +grid(5)
  +pull(5)
```

#### +gutter( $gutter )
Insert just the defined grid gutter on any element.

###### Optional params
`$gutter`: measure in px | Changes the predefined gutter.

Example:
```sass
.omg_i_must_have_the_same_grid_gutter
  +gutter
```

#### +clear()
Clear floated elements

Example:
```sass
.i_am_a_motherfucker_element_and_i_will_break_this_grid
  +clear
```

#### +clearfix()
Inserts a clearfix. **Everybody knows what is that!**

Example:
```sass
.please_i_wanna_see_my_size
  +clearfix
```

#### ~~+grid_sidebar($size, $position: 'left', $class-view: 'view', $class-sidebar: 'sidebar', $grid_parent: true)~~
Creates a column of your grid with fixed width. Don't want to resize your sidebar?
Ps.: New mixing. Please do not use before I document it. **Pass here tomorrow. :p**

## Recomendations

### Increase the accuracy of relative measures, or an evil goat will eat your socks!

It is highly recommended that you work with precision when dealing with measures. At your `compass.rb` or `config.rb` file, add the following line:

```ruby
Sass::Script::Number.precision = 10
```
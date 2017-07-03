![Custom Grid System](https://raw.github.com/luizgamabh/custom.gs/master/assets/img/logo.png)
# [http://custom.gs](http://custom.gs)

Custom Grid System is a new grid system completely customizable for any need.

## How it works?

`your_nice_component.sass`:
```sass
@import "custom"

main
  +container(1024px)

section
  +grid(6, 10)

aside
  +grid(4, 10)
```

`your_nice_component.html`:
```html
<main>
    <section>
        First column
    </section>
    <aside>
        Second column
    </aside>
</main>
```

### NESTED GRIDS

```sass
.parent
  +grid(1, 2, $parent: true)
  .child
    +grid(1, 3)
```

## Documentation

### General grid options:

* `$default-container-with`: ==100% !default== `width measure with unit` - Website width limits
* `$default-gutter`: ==24px !default== `width measure with unit` - Space between columns
* `$default-cols`: ==12 !default== `integer` - Default amount of columns
* `$default-direction`: =='ltr' !default== `string` - **ltr**: Left-to-right or **rtl**: Right-to-left
* `$default-edges`: ==true !default== `boolean` - Enable gutter on edges (extremities)?

### Mixins:

#### +container( [ $optional_params ] )
Defines your container with desired width, if ommited uses `$default-container-width` general variable.

###### Optional params
`$clear`: Default: **false** | Clear the container (can be used to disable the container in some breakpoint).
`$width`: Container width
`$margin`: Container margin
`$padding`: Container padding

Example:
```sass
.main
  +container
.footer
  +container(1024px)
@media only screen and (max-width: 768px)
  .main
    +container($clear: true)
```

#### +grid($cols, [ $total, $helpers] )
Defines your grid column

###### Mandatory params
`$cols`: number of columns (integer)

###### Optional params
`$total`: Default: **$default-cols** | Defines a new reference overwriting the $default-cols just for this specific element.

###### Helper options
`$gutter`: width measure with unit. Overrides $default-gutter variable.
`$edges`: boolean. Overrides $default-edges variable.
`$cycle`: integer. Forces a breakpoint after `x` elements.
`$uncycle`: integer. Removes cycle breakpoints.
`$direction`: string (ltr or rtl). Overrides $default-direction variable.
`$prefix`: integer. Prefix with an empty space of `x` columns.
`$suffix`: integer. Suffix with an empty space of `x` columns.
`$push`: integer. Pushes the column `x` times.
`$pull`: integer. Pulls the column `x` times.
`$parent`: boolean. Remove margins when $edges are enabled.

Examples:
```sass
$default-edges: true
$default-cols: 10

.header
  +container

  .header__title
    +grid(1, 2, $push: 1)

  .header__menu
    +grid(1, 2, $pull: 1)

.main
  +container

  .gallery__list
    +grid(10, 16, $parent: true)

    .gallery__list-item
      +grid(1, 4, $cycle: 4)

  .side
    +grid(6, 16)

.footer
  +container

  .footer__left,
  .footer__right
    +grid(5)
```

#### +expand()
Forces a full window column inside container, extrapolating the container width.
> Uses viewport units and does not work on IE8

Examples:
```sass
.main
  +container
  .full-column
    +expand
```

#### +prefix( $cols, [ $total: $number-of-columns ] )
Insert empty space before a grid column.

###### Mandatory params
`$cols`: integer | Prefixes the current column with blank space equivalent to x columns.

###### Optional params
`$total`: integer | Defines a new reference overwriting the $number-of-columns just for this specific element.

###### Helper params
`$gutter`: integer | Defines a new reference overwriting the $number-of-columns just for this specific element.
`$edges`: integer | Defines a new reference overwriting the $number-of-columns just for this specific element.

Example:
```sass
$default-cols: 10

.my_indented_element
  +grid(9, $prefix: 1)

.alone_and_depressive_element
  +grid(1, 5, $prefix: 4)

.another_alone_element
  +grid(1, 5)
  +prefix(4, 5)
```

#### +suffix( $cols, [ $total: $number-of-columns ] )
Insert empty space after a grid column.

###### Mandatory params
`$cols`: integer | Suffixes the current column with blank space equivalent to x columns.

###### Optional params
`$total`: integer | Defines a new reference overwriting the $number-of-columns just for this specific element.

###### Helper params
`$gutter`: integer | Defines a new reference overwriting the $number-of-columns just for this specific element.
`$edges`: integer | Defines a new reference overwriting the $number-of-columns just for this specific element.

Example:
```sass
$default-cols: 10

.my_outdented_element
  +grid(9, $suffix: 1)

.centralized_alone_and_depressive_element
  +grid(1, 5, $prefix: 2, $suffix: 2)

.another_alone_element
  +grid(1, 5)
  +prefix(2, 5)
  +suffix(2, 5)
```

#### +push( $cols, [ $total, $relative ] )
Rearrange element position.

###### Mandatory params
`$cols`: integer | Repositions the element x `$cols` after.

###### Optional params
`$total`: integer | Defines a new reference overwriting the $default-cols just for this specific element.
`$relative`: boolean | Adds `position: relative;` property to element, default ==true==.

Example:
```sass
$default-cols: 10

.send_me_to_right
  +grid(5)
  +push(5)

#### +pull( $cols, [ $total, $relative ] )
Rearrange element position.

###### Mandatory params
`$cols`: integer | Repositions the element x `$cols` before.

###### Optional params
`$total`: integer | Defines a new reference overwriting the $default-cols just for this specific element.
`$relative`: boolean | Adds `position: relative;` property to element, default ==true==.

Example:
```sass
$default-cols: 10

.send_me_to_right
  +grid(5)
  +push(5)

.send_me_to_left
  +grid(5)
  +pull(5)

.send_me_to_left_encapsulated_way_same_result
  +grid(5, $pull: 5)
```

#### +gutter([ $edges ])
Insert default gutter on any element.

###### Optional params
`$edges`: boolean | Enable or disable edges overriding $default-edges

Example:
```sass
.omg_i_must_have_the_global_grid_gutter
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

## Recomendations

### Increase the accuracy of relative measures, or an evil goat will eat your socks!

It is highly recommended that you work with precision when dealing with measures. At your `compass.rb` or `config.rb` file, add the following line:

```ruby
Sass::Script::Number.precision = 10
```

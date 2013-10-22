![Custom Grid System](https://raw.github.com/luizgamabh/custom.gs/master/assets/img/logo.png)

Custom Grid System is a new Sass (and Less ASAP) based grid system that combines best practices of:

* [Grid960](http://960.gs)
* [Bootstrap](http://getbootstrap.com)
* [Unsemantic](http://unsemantic.com)
* [Semantic](http://semantic.gs)

Custom.gs works with columns rather than percentages, anyway you can set-up many columns as you need. Eg.:

UNSEMANTIC MODE:


```html
<div class="container_52">
    <div class="grid_32">
        First column
    </div>
    <div class="grid_20">
        Second Column
    </div>
</div>
```

SEMANTIC MODE (same result without many classes messing your code):

    div#main
      +container_52

    section
      +grid_32

    aside
      +grid_20

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

### Options

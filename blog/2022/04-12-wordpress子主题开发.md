---
title: "wordpress子主题开发"
date: "2022-04-12"
categories: 
  - "front-end"
tags: 
  - "php"
  - "wordpress"
---

### 需求场景

如果购买了一个wordpress主题，并且以此作为基础二次开发，后面该主题更新，希望同步更新的情况下，需要子主题。如果不需要同步原主题的开发就不要子主题，直接修改就完事。

### 子主题的优势

同步原主题的更新，更新主题的同时不会覆盖自己的定制修改。

### 子主题的缺点

对于css文件会加载2份，1份是父主题，1份子主题。子主题的css覆盖父主题的样式实现修改的功能。这样做就会导致css代码的冗余，如果子主题css加载慢，甚至会出现先展示父主题的css样式再变成子主题的修改效果。不如直接修改父主题来的优雅简洁。

### 子主题开发

假定父主题为_Twenty Twenty-Two_，目录为twentytwentytwo。

- 步骤一：同级新建twentytwentytwo-child目录
- 步骤二：在twentytwentytwo-child目录下，新建style.css文件，代码如下，顶部的注释是必须的。

styles.css头部注释文档：[https://developer.wordpress.org/themes/basics/main-stylesheet-style-css/](https://developer.wordpress.org/themes/basics/main-stylesheet-style-css/)

```css
/*
 Theme Name:   Twenty Twenty-Two Child
 Template:     twentytwentytwo
 Version:      1.0.0
*/
```

- 步骤三：在twentytwentytwo-child目录下，新建functions.php,代码如下。

详细文档：[https://developer.wordpress.org/themes/advanced-topics/child-themes/](https://developer.wordpress.org/themes/advanced-topics/child-themes/)

```php
<?php
add_action( 'wp_enqueue_scripts', 'my_theme_enqueue_styles' );
function my_theme_enqueue_styles() {
    wp_enqueue_style( 'child-style', get_stylesheet_uri(),
        array( 'parenthandle' ), 
        wp_get_theme()->get('Version')
    );
}
```

- 步骤四：在wordpress后台启用twentytwentytwo-child子主题

### 最佳实践

- template修改

在子主题下，新建和父主题同名模板文件，全覆盖父级模板并调整。

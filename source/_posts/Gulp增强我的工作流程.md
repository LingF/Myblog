title: "Gulp增强我的工作流程"
date: 2016-02-29 20:39:55
tags: [gulp, 提升]
---

## gulp
gulp是什么？从宏观来讲，他是JavaScript流构建系统，从微观说就是一个基于流的自动化构建工具。他让我们更灵活的操作流。
### 流
流是什么呢？流就是一种数据移动的抽象说法，当一个文件中的数据通过某些‘管道’，序列地去向另一个地方，我们把他形象的说成流，认为他是源源不断的在移动。比较普及的概念有‘流媒体’、‘网络流量’，其实这些都大同小异。
### 应用
当然，这里不再赘述[gulp如何使用](http://www.gulpjs.com.cn/)，不了解的自行百度。
反思工作，有这么几个痛点：

1. F5刷新是我们最常规的操作
2. 资源图片的压缩
3. css的兼容(低版本浏览器/css3)、css的语法增强(构建自己的css预处理器，简化代码)

#### 干掉这些痛点，用gulp！
gulp这类工具强大就在于他有许多插件，能让立马解决一些需求。
对应上面的问题，我们一一使用插件：

1. [browser-sync](http://www.browsersync.cn/) (这是一个单独的工具，独立于gulp，但我们用gulp使用他)
2. gulp-imagemin、imagemin-pngquant、gulp-cache
3. gulp-postcss、autoprefixer-core

以上一些插件及使用都能从[github](https://github.com/)上搜到，就不多做介绍了。下面直接上代码。

配置、插件的导入：
``` javascript
    /* config */
    var config  = require('./config/config.js');    //配置文件中可以保存一些变量，便于以后扩展
    var baseDir = config.baseDir;
    var path    = config.path;
    /* config end */

    var gulp = require('gulp');

    /* browserSync */
    var browserSync = require('browser-sync').create();
    var reload      = browserSync.reload;
    /* browserSync end */

    /* imagemin */
    var imagemin = require('gulp-imagemin');
    var pngquant = require('imagemin-pngquant');
    var cache    = require('gulp-cache');
    /* imagemin end*/

    /* postcss */
    var postcss      = require('gulp-postcss');
    var autoprefixer = require('autoprefixer-core');
    /* postcss end */
```

默认任务(最后执行，browserSync的初始化，watch所有文件的变化后自动刷新)：
``` javascript
    gulp.task('default', ['images', 'postcss', 'js', 'html'], function() {
        browserSync.init({
            server: {
                baseDir: config.baseDir
            }
        });
        gulp.watch(path.IMG[0], ['images']);
        gulp.watch(path.CSS[0], ['postcss']);
        gulp.watch(path.JS[0], ['js']);
        gulp.watch(path.HTML[0], ['html']);
        gulp.watch(path.HTML[0]).on('change', reload);
    });
```

图片的处理(cache会缓存没有修改的图片，只输出改动的图片)：
``` javascript
    gulp.task('images', function () {
        return gulp.src(path.IMG[0])
            .pipe(cache(imagemin({
                progressive: true,
                svgoPlugins: [{removeViewBox: false}], //不要移除svg的viewbox属性
                use: [pngquant()]                      //使用pngquant深度压缩png图片的imagemin插件
            })))
            .pipe(gulp.dest(path.IMG[1]))
            .pipe(browserSync.stream());
    });
```

css的处理(下一代css + 自定义预处理器)：
``` javascript
    gulp.task('postcss', function () {
        var processors = [
            require('postcss-cssnext'),
            require('cssgrace'),
            require('postcss-mixins'),
            require('postcss-simple-vars'),
            require('postcss-nested')
        ];
        return gulp.src(path.CSS[0])
            .pipe(postcss(processors))
            .pipe(gulp.dest(path.CSS[1]))
            .pipe(browserSync.stream());
    });

```

扩展(js的压缩、合并、添加MD5等)：
``` javascript
    //js、html便于之后扩展，这里只是单纯的复制到输出目录
    gulp.task('js', function() {
        return gulp.src(path.JS[0])
            .pipe(gulp.dest(path.JS[1]))
            .pipe(browserSync.stream());
    });

    gulp.task('html', function() {
        return gulp.src(path.HTML[0])
            .pipe(gulp.dest(path.HTML[1]))
            .pipe(browserSync.stream());
    })
```

>processors中postcss插件都可从[github](https://github.com/)中找到，这里的组合基本构成了一个简易的预处理器。从中可窥postcss的强大，
>见上一篇[PostCSS初探](http://www.zlycy.com/20151225/PostCSS%E5%88%9D%E6%8E%A2/)。

### 总结
gulp解决了自己工作中的痛点，通过他轻轻松松地提高了效率和开发质量，这个还是非常happy的~


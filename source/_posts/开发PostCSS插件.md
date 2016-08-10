title: "开发PostCSS插件"
date: 2016-01-08 16:09:30
tags: [PostCSS, 产出]
---

# postcss-mbrem


写[postcss-mbrem](https://github.com/LingF/postcss-mbrem)这个插件启发于一个简单的手机端需求。
开发中需要使用rem的适配方案，但在拿到设计稿后,我们测量元素尺寸、位置等得到的像素值每次需要通过计算再写入css，这样相当麻烦。
在使用了[hotcss](https://github.com/imochen/hotcss)这个结解决方案后，省去了计算提高了开发效率。不过随之带来了新的问题，每次需要带入自定义的sass方程_rem2px_，受此影响，我想何不创造一种新的单位来直接书写，免去方程的书写，也汲取单位的换算在新的单位中，省时省力。所以通过PostCSS写了这个简单的插件。

## Install

With npm do:


    npm install --save-dev postcss-mbrem


### Input

``` css
.box {
  width: 100mm;
  height: 200mm;
  margin: 10mm 20mm;
}
```

### Output

``` css
.box {
  width: 2.13333rem;
  height: 4.26667rem;
  margin: 0.21333rem 0.42667rem;
}
```

## Options

  * width - 设计稿宽度(默认：750)
  * median - 中间值(默认：320/20)

### Example

``` javascript
  var gulp = require('gulp');

  var postcss = require('gulp-postcss'),
      mbrem = require('postcss-mbrem');

  gulp.task('default', function() {
    var processors = [
          mbrem({width: 1125})
        ];
    return gulp.src(["./src/c/*.css"])
        .pipe(postcss(processors))
        .pipe(gulp.dest("./dest/c/"));
    });
```

## Other
如果使用时报错，缺少模块则需要安装：

    npm install --save-dev postcss underscore

本插件依赖2个模块：

  * postcss
  * underscore
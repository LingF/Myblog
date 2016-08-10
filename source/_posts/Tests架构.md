title: 构建自己的Cocos2d-JS Tests架构
date: 2016-04-14 23:34:56
tags: [JavaScript, Cocos, 产出]
---

Cocos引擎中有一个自带的Tests架构，他能帮助我们理解引擎中自带的Demo，也方便组织自己在学习中写的Demo。我比较不满意的是他只有主列表，当同一块内容中有许多不同的Demo时，Demo就不能很好地也以列表形式呈现，为了更好地使用，我打算改良一下。

## Tests架构
这个测试架构大致分为3层：

* BaseLayer
* DemoBaseLayer
* Demo1/Demo2/...

从上到下依次继承，BaseLayer则继承cc.Layer。

### *BaseLayer*做了4件事：

1. 定义 3个实例切换的接口（不同Demo之间切换）
2. 定义 3个Label说明的接口（中英文标题，说明3段文字）
3. 实现 MainMenu按钮（返回列表）
4. 加载 界面元素

### *DemoBaseLayer*：

1. 重写 3个实例切换的接口（通过DEMO_IDX标记不同Demo，用数组arrayDemo组织所有Demo）

### *Demo*：

1. 重写 3个Label（填充当前Demo的信息）
2. 实现不同的功能（主体）

### 当然这里整体的切入点是主列表（MainMenu）：
他是一个列表，就如同书本的目录，有不同单元（Unit），你进入某一单元就能看到这个单元下的Demo。

* 定义 一个 MainMenuScene 的场景，场景中有一个 MainMenuLayer 列表层。
* 通过对存放单元信息的数组 testNames 获取单元数和标题，渲染一个主列表（用来选择不同单元），并处理点击，判断进入不同（单元）场景。
* （单元）场景中构建自己的 Demo。

关系如下：
进入游戏 -> MainMenuScene[ MainMenuLayer (Menu) ] -click-> UnitScene(Demo1/Demo2/...) 

## 如何改良
我们来看看用起来不爽的地方：

1. 不能很好地定位到某一个Demo，也不知道某单元到底有多少个Demo，只能上下切换。
2. 添加Demo需要修改多处地方（最好能统一管理，以类似config的形式存在方便添加）。

## 自己的Tests架构
针对以上2点，我们就有了修改的方向。

### 添加 Demo 列表
我们修改当点击Menu后不再直接进入Demo，而是进入另一个场景（Demo列表），取名为 LessonMenu。LessonMenu 添加层 LessonMenuLayer，他主要实现类似于MainMenuLayer。同样包含一个Menu，点击能进人LessonScene，这个场景根据信息渲染不同的Demo。

``` javascript  LessonMenu.js
var LessonMenuLayer = cc.LayerColor.extend({
    _lessons: null
  , ctor: function(args) {
      this._super();
      this._lessons = args;
    }
  , onEnter : function(){
      this._super(cc.color(0, 0, 0));

      // 菜单
      var itemMenu = new cc.Menu();
      var lessonNames = this._lessons;

      // 遍历所有的示例
      for (var i = 0; i < lessonNames.length; i++) {
        var label = new cc.LabelTTF(lessonNames[i].title, 'Arial', 64);
        var menuItem = new cc.MenuItemLabel(label, this.onMenuCallback, this);
        itemMenu.addChild(menuItem, i + 10000);
        menuItem.setPosition(GC.w2, GC.h - (i + 1) * LINE_SPACE);
      }

      // 菜单属性配置
      itemMenu.setContentSize(GC.w, (lessonNames.length + 1) * LINE_SPACE);
      itemMenu.setPosition(0, 0);
      this.addChild(itemMenu);
    },

    onMenuCallback : function(sender){

      var lessonNames = this._lessons;
      // TODO 根据层级区分当前的菜单item
      var idx = sender.getLocalZOrder() - 10000;
      DEMO_IDX = idx;
      var testCase = lessonNames[idx];
      var layer = arrayDemo[UNIT_IDX][idx];
      var scene = new LessonScene(layer);
      cc.director.runScene(scene);

      // 如果需要加载资源
      // if (false){
      //   var res = testCase.resource || [];
      //   cc.LoaderScene.preload(res, function () {
      //     var scene = testCase.getScene();
      //     cc.director.runScene(scene);
      //   }, this);
      // }
    }
});

var LessonMenu = cc.Scene.extend({
    _lessons: null  //保存Demo列表信息
  , ctor: function(args) {
    this._super();

    this._lessons = args;
  }
  , onEnter : function(){
    this._super();

    var layer = new LessonMenuLayer(this._lessons);
    this.addChild(layer);
  }
});

var LessonScene = cc.Scene.extend({
  _layer: null  //保存需要渲染的Demo
, ctor: function(args) {
    this._super();

    this._layer = args;
  }
, onEnter: function() {
    this._super();
    
    // 直接渲染Demo
    var layer = new this._layer();
    this.addChild(layer);
  }
});
```

>这里需要传递一个参数，就是点击了哪个Unit，我们在LessonMenuLayer中渲染对应的Lesson。

### 配置化Demo
分别用 testNames 存放 Unit 和 Demo 的标题，arrayDemo 存放实际的 Demo：
``` javascript  Data.js
// Demo 名称列表
var testNames = [
  {
    title: 'Unit1',
    lessons: [
      {title: 'lesson01'},
      {title: 'lesson02'},
      {title: 'lesson03'},
      {title: 'lesson04'},
      {title: 'lesson05'},
      {title: 'lesson06'}
    ]
  },
  {
    title: 'Unit2',
    lessons: [
      {title: 'lesson06'},
      {title: 'lesson05'},
      {title: 'lesson04'},
      {title: 'lesson03'},
      {title: 'lesson02'},
      {title: 'lesson01'}
    ]
  },
  {
    title: 'Unit3',
    lessons: [
      {title: 'Lesson03'},
      {title: 'Lesson04'},
      {title: 'Lesson06'}
    ]
  },
  {
    title: 'Unit4',
    resource: null,  // 如果需要资源
    lessons: [
      {title: 'Lesson01'}
    ]
  },
  {
    title: 'Unit5',
    resource: null,
  }
];

// 数组[Demo集合]
var arrayDemo = [
  [
    Demo1,
    Demo2,
    Demo3,
    Demo4,
    Demo5,
    Demo6
  ],
  [
    Demo6,
    Demo5,
    Demo4,
    Demo3,
    Demo2,
    Demo1
  ],
  [
    Lesson03Layer,
    Lesson04Layer,
    Lesson06Layer
  ],
  [
    Lesson01Layer
  ]
]
```

这样每次添加新 Demo 时，我们直接修改 Data.js 和引入新的 Demo 就可以了。

### Tests结构
最终我们改良后的Tests的目录：

* res (资源)
* src
    - config 
        + gameConfig.js
        + resource.js
    - lib
    - main
        + BaseLayer.js
        + BaseDemo.js
        + MainMenu.js
        + LessonMenu.js
    - unit
        + Data.js
        + Unit01.js
        + ...
* index.html
* main.js
* project.json 

## 结语
这样一个改良后的Tests就完成了，然后就可以开开心心地添加Demo，统一管理方便自己查找啦。当然，这个还不是很完美，比如当Demo多时，列表就需要更好地组织显示，现在只是纵向的一列。还可以添加其他的按钮，比如返回Demo列表页，而不是直接返回主列表等等。充实Demo库的同时，我们也需要不断优化自己的Tests。最后附上完整代码[myTests](https://github.com/LingF/Cocos2d-JS-MyTests)

---
layout: post
title: 'javascript链式调用的实现'
category: 文档
tags:javascript 
---

# javascript 链式调用的实现

---
在我们所用到的库中，可以看到很多诸如

    $(window).addEvent('load', function(){
        $('test').show().setStyle('color', 'red').addEvent('click', function(e){
            $(this).setStyle('color', 'yellow');
        });
    });

 的链式调用，那么这样的链式结构是怎么实现的呢，下面我们利用代码来探讨一番：

 

 先分解下，我们队$函数已经很熟悉了，他通常返回一个HTML元素或者HTML元素的集合，如下所示：

    function $(){
        var elements = [];
        for(var i = 0, len = arguments.length; i < len; i++){
            var element = els[i];
            if(typeof element === 'string'){
                element = document.getElementById(element);
            }
            elements.push(element);
        }
        return elements;
    }

 但是，如果把这个函数改造为一个构造器，把那些元素作为数组保存在一个实例属性中，并让所有定义在构造器函数的prototype属性所指对象中的方法都返回用以调用放方法的那个实例的引用，那么他就具有了进行链式调用的能力。

 

先别说的太远，我们首先需要把这个$函数改为一个工厂函数，他负责创建支持链式调用的对象。

    (function(){
    
        function _$(els){
            this.element = [];
            for(var i = 0, len = els.length; i < len; i++){
                var element = els[i];
                if(typeof element === 'string'){
                    element = document.getElementById(element);
                }
                this.element.push(element);
            }
            return this;
        }
        window.$ = function(){
            return new _$(arguments);
        }
    })();      

 
由于所有对象都会继承其原型对象的属性和方法，所以我们可以让定义原型对象中的那几个方法都返回用以调用方法的实例对象的引用，这样既可以对那些方法进行链式调用，想好这一点，我们现在就动手在_$这个私用构造函数的prototype对象那个中添加方法，以便实现链式调用。

 

    (function(){
    
        function _$(els){
            this.element = [];
            for(var i = 0, len = els.length; i < len; i++){
                var element = els[i];
                if(typeof element === 'string'){
                    element = document.getElementById(element);
                }
                this.element.push(element);
            }
            return this;
        }
    
        _$.prototype = {
            each: function(fn){
                for(var i = 0, len = this.element.length; i < len; i++){
                    fn.call(this, this.element[i]);
                }
                return this;
            },
    
            setStyle: function(prop, val){
                this.each(function(el){
                    el.style[prop] = val;
                });
                return this;
            },
    
            show: function(){
                var that = this;
                this.each(function(el){
                    that.setStyle('display', 'none');
                });
                return this;
            },
    
            addEvent: function(type, fn){
                var add = function(el){
                    if(window.addEventListener){
                        el.addEventListener(type, fn, false);
                    }else if(window.attachEvent){
                        el.attachEvent('on' + type, fn);
                    }
                };
                this.each(function(el){
                    add(el);
                });
            }
        };
    
        window.$ = function(){
            return new _$(arguments);
        }
    })();

 

 看看该类每个方法的最后一行，你会发现他们都是以"return this;"结束，这样将用以调用方法的对象传给调用链上的下一个方法。

-----
#第二篇文章
------
链式调用
    链式调用其实只不过是一种语法招数。它能让你通过重用一个初始操作来达到用少量代码表达复杂操作的目的。该技术包括两个部分：
一个创建代表HTML元素的对象的工厂。
一批对这个HTML元素执行某些操作的方法。
调用链的结构
$函数负责创建支持链式调用的对象
 代码如下:

    (function() {
        /*
         * 创建一个私有class
         * @param {Object} els  arguments 所有参数组成的类数组
         */
        function _$(els) {
            this.elements = [];             //存放HTML元素
            for(var i=0, len=els.length; i<len; i++) {
                var element = els[i];
                if(typeof element === 'string') {
                    element = document.getElementById(element);
                }
                this.elements.push(element);
            }
        }
        //对HTML元素可执行的操作
        _$.prototype = {
            each: function() {},
            setStyle: function() {},
            show: function() {},
            addEvent: function() {},
        };    
        //对外开放的接口
        window.$ = function() {
            return new _$(arguments);
        };   
    })();

由于所有对象都会继承其原型对象的属性和方法，所以我们可以让定义在原型对象中的那些方法都返回用以调用方法的实例对象的引用，这样就可以对那些方法进行链式调用了。
 代码如下:

    (function() {
        /*
         * 创建一个私有class
         * @param {Object} els  arguments 所有参数组成的类数组
         */
        function _$(els) {
            //...
        }
        //对HTML元素可执行的操作
        _$.prototype = {
            each: function(fn) {        //fn 回调函数
                for(var i=0; i<this.elements.length; i++) {
                    //执行len次，每次把一个元素elements[i]作为参数传递过去
                    fn.call(this, this.elements[i]);
                }
                return this;
            },
            setStyle: function(prop, value) {
                this.each(function(el) {
                    el.style[prop] = value;
                });
                return this;
            },
            show: function() {
                var that = this;
                this.each(function(el) {
                    that.setStyle('display', 'block');
                });
                return this;
            },
            addEvent: function(type, fn) {
                var addHandle = function(el) {
                    if(document.addEventListener) {
                        el.addEventListener(type, fn, false);
                    }else if(document.attachEvent) {
                        el.attachEvent('on'+type, fn);
                    }
                };
                this.each(function(el) {
                    addHandle(el);
                });
                return this;  
            }
        };
        //对外开放的接口
        window.$ = function() {
            return new _$(arguments);
        }
    
    })();
    //----------------------- test --------
    $(window).addEvent('load', function() {
        $('test-1', 'test-2').show()
        .setStyle('color', 'red')
        .addEvent('click', function() {
            $(this).setStyle('color', 'green');
        });
    })

链式调用的方法获取数据
    使用回调函数从支持链式调用的方法获取数据。链式调用很适合赋值器方法，但对于取值器方法，你可能希望他们返回你要的数据而不是**this(调用该方法的对象)**.解决方案：利用回调技术返回所要的数据.
 代码如下:

    window.API = window.API || function() {
        var name = 'mackxu';
        //特权方法
        this.setName = function(name0) {
            name = name0;
            return this;
        };
        this.getName = function(callback) {
            callback.call(this, name);
            return this;
        };
    };
    //------------- test ---
    var obj = new API();
    obj.getName(console.log).setName('zhangsan').getName(console.log);

设计一个支持方法链式调用的JS库
JS库特征：
事件： 添加和删除事件监听器、对事件对象进行规划化处理
DOM： 类名管理、样式管理
Ajax： 对XMLHttpRequest进行规范化处理
 代码如下:

    Function.prototype.method = function(name, fn) {
        this.prototype[name] = fn;
        return this;
    };
    (function() {
        function _$(els) {
            //...
        }
        /*
         * Events
         *      addEvent
         *      removeEvent
         */
        _$.method('addEvent', function(type, fn) {
            //...  
        }).method('removeEvent', function(type, fn) {
    
        })
        /*
         * DOM
         *      addClass
         *      removeClass
         *      hover
         *      hasClass
         *      getClass
         *      getStyle
         *      setStyle
         */
        .method('addClass', function(classname) {
            //...
        }).method('removeClass', function(classname) {
            //...
        }).method('hover', function(newclass, oldclass) {
            //...
        }).method('hasClass', function(classname) {
            //...
        }).method('getClass', function(classname) {
            //...
        }).method('getStyle', function(prop) {
            //...
        }).method('setStyle', function(prop, val) {
            //...
        })
        /*
         * AJAX
         *      ajax
         */
        .method('ajax', function(url, method) {
            //...
        });
    
        window.$ = function() {
            return new _$(arguments);
        };
        //解决JS库命名冲突问题
        window.installHelper = function(scope, interface) {
            scope[interface] = function() {
                return _$(arguments)
            }
        }  
    })();

小结：
    链式调用有助于简化代码的编写工作，并在某种程度上可以让代码更加简洁、易读。很多时候使用链式调用可以避免多次重复使用一个对象变量，从而减少代码量。如果想让类的接口保持一致，让赋值器和取值器都支持链式调用，那么你可以在取值器中使用回调函数来解决获取数据问题。



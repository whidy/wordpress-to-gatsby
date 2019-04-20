---
author: whidy
comments: true
date: 2017-08-12 08:02:13+00:00
excerpt: 关于我最近学习PostCSS的一些相关心得和总结
template: post
link: http://www.whidy.net/postcss-study-1.html
slug: /postcss-study-1
title: PostCSS学习指南（一）
wordpress_id: 2956
category: '音乐'
tags:
- nodejs
- 技术
---

(推荐访问github上面的Markdown排版的介绍[PostCSS学习指南（一）](https://github.com/whidy/postcss-study/blob/master/PostCSS学习指南.md))


## [](https://github.com/whidy/postcss-study/blob/master/PostCSS%E5%AD%A6%E4%B9%A0%E6%8C%87%E5%8D%97.md#postcss介绍)PostCSS介绍


[PostCSS](https://github.com/postcss/postcss)是一个利用JS插件来对CSS进行转换的工具，这些插件非常强大，强大到无所不能。其中，[Autoprefixer](https://github.com/postcss/autoprefixer)就是众多PostCSS插件中最流行的一个。

截至目前（2017年7月）PostCSS已经有**超过200**个插件，你可以[插件列表](https://github.com/postcss/postcss/blob/master/docs/plugins.md)查找有没有你所需要的插件。如果你想自己写个插件，据说这是一个不错的主意，而且非常简单，你可以试着[搞点事](https://github.com/postcss/postcss/blob/master/docs/writing-a-plugin.md)。

看到这里，你可能没有发现它的强大之处，甚至我自己都没有被我翻译的这段官方文字所打动。~~因为没(wǒ)有(yě)对(bù)比(tài)就(huì)没(yòng)有(zhè)伤(wán)害(yì)。~~好了，是时候启动装逼模式了。

维基百科，阿里巴巴，谷歌，Wordpress，Twitter等网站均有使用，大佬们都在用你有什么理由不跟上步伐。

再来看看这张PostCSS下载数量的npm-stat统计表（数据证明一切）：

![PostCSS下载数量](https://github.com/whidy/postcss-study/raw/master/src/images/postcss-00.png?raw=true)

学习PostCSS之前需要了解一些事情：



 	
  1. PostCSS插件的处理方式类似那些CSS预处理器，而非预处理器和后处理器（[PostCSS is Not a *Pre-*processor and Not a *Post-*processor either](https://webdesign.tutsplus.com/tutorials/postcss-deep-dive-what-you-need-to-know--cms-24535)）

 	
  2. PostCSS is Not “Future Syntax”（不是新式语法？不知道怎么翻译）

 	
  3. PostCSS本身并非整理或优化CSS的工具

 	
  4. PostCSS可以完成很多意想不到的事情，例如用[postcss-rtl](https://github.com/vkalinichev/postcss-rtl)恶搞一下![:yum:](https://assets-cdn.github.com/images/icons/emoji/unicode/1f60b.png)


那么它还有一些特性，例如创建了一个插件功能极强的生态系统，具有模块化需要什么用什么（[precss](https://github.com/jonathantneal/precss)就是一个集成了类似SASS的包），相比其他的CSS预处理器它的优势主要体现在以下几个方面：



 	
  1. 拥有极高的处理性能（[3倍以上的处理速度](https://github.com/postcss/benchmark)）

 	
  2. 你既可以写正常的CSS，也可以结合LESS或者SASS一起编写

 	
  3. 对Source Map支持更好

 	
  4. 他的插件真的太多太强大太便利了


其他对比SASS和LESS的区别在于他们内置了大量的方法，而也许你只需要用到几个变量而已，大材小用。而PostCSS则可制定个人需求的一套解决方案（仅安装需要的插件）。这也就是他高性能的主要原因。几乎SASS和LESS有的功能全都有！

总之好处太多了。这里就不一一列举了。迫不及待的你已经等不及安装使用了吧。

<!-- more -->


## [](https://github.com/whidy/postcss-study/blob/master/PostCSS%E5%AD%A6%E4%B9%A0%E6%8C%87%E5%8D%97.md#postcss安装及使用)PostCSS安装及使用


PostCSS一般是结合自动化工具使用，如果要单独使用可以安装[PostCSS CLI](https://github.com/postcss/postcss-cli)，这里我先对PostCSS CLI的安装使用讲解下。Windows下安装（文中操作全部基于WINDOWS环境）：

~~`npm i -g postcss-cli`~~或者`npm i --save-dev postcss-cli`

CLI是否建议全局安装?（这样包括其对应的插件都要全局了？如果不全局就失去了CLI的意义了？）。全局安装完成后，试着输入PostCSS，出现以下结果，说明安装OK

![安装成功](https://github.com/whidy/postcss-study/raw/master/src/images/postcss-01.png?raw=true)

不过我个人习惯仅安装在项目中，于是我没有选择安装CLI，而是直接在项目中安装PostCSS，`npm i --save-dev postcss`，我这里有个[例子](https://github.com/whidy/postcss-study)可以看看

接下来，我们还做不了什么，我们需要安装一些插件配合PostCSS，例如，我现在安装一个autoprefixer

`npm install --save-dev autoprefixer`，并参考例子中的[style01.css](https://github.com/whidy/postcss-study/blob/master/src/style01.css)，我要通过PostCSS对它进行处理。这里两个方法：



 	
  1. 通过`cd node_modules/.bin/`进入node_modules/.bin/目录内再执行`postcss ../../src/style01.css -o ../../dist/output_style01.css -u autoprefixer`

 	
  2. 通过修改package.json中的scripts，增加一条postcss命令`"postcss:style01": "postcss ./src/style01.css -o ./dist/output_style01.css -u autoprefixer"`然后再回到根目录（postcss-study目录）下执行`npm run postcss:style01`


两者效果相同，当然我倾向于后者啦。完成后一条鲜亮的绿色的让人安全感十分强列的提示语出现了*√ Finished ...*前面还有个sweet的勾勾，请看编译后的[output_style01.css](https://github.com/whidy/postcss-study/blob/master/dist/output_style01.css)聪明的你一定能举一反三的。做出更多惊奇的事情的~

另外我们可以同样的采用Parser插件来编译样式文件，我的[DEMO](https://github.com/whidy/postcss-study)里面请参考[style02.sss](https://github.com/whidy/postcss-study/blob/master/src/style02.sss)文件的编译。这里就不多说了。


<blockquote>还有一种预先写好配置文件，这个就稍微先进一些，也不会看起来很乱。我们创建一个**[postcss.config.js](https://github.com/whidy/postcss-study/blob/master/postcss.config.js)**文件：

> 
> 

>     
>     <span class="pl-c1">module</span>.<span class="pl-smi">exports</span> <span class="pl-k">=</span> {
>       parser<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>sugarss<span class="pl-pds">'</span></span>,
>       plugins<span class="pl-k">:</span> [
>         <span class="pl-c1">require</span>(<span class="pl-s"><span class="pl-pds">'</span>autoprefixer<span class="pl-pds">'</span></span>)
>       ]
>     }
> 
> 

> 
> 
不过这种经过我个人测试，**仅适用于全局安装了PostCSS-CLI和sugarss的情况**下再该配置文件目录下执行`postcss ./src/style02.sss -o ./dist/test.css`命令就好了。这里个人不是很推荐。关于CLI下的一些方法暂时就不多说了，如有错误请各位大佬指正~![:joy:](https://assets-cdn.github.com/images/icons/emoji/unicode/1f602.png)</blockquote>




## [](https://github.com/whidy/postcss-study/blob/master/PostCSS%E5%AD%A6%E4%B9%A0%E6%8C%87%E5%8D%97.md#postcss主要插件说明和介绍)PostCSS主要插件说明和介绍


官方对于插件根据用途做了分类，主要有以下几个类别：

解决全局CSS问题

使用未来的CSS语法

编写可读性更好的CSS

用于图片和字体

CSS语法检查

其他

以上内容主要是用来熟悉一下PostCSS的。接下来说点实际的，如何利用PostCSS结合自动化工作在项目中使用。


## [](https://github.com/whidy/postcss-study/blob/master/PostCSS%E5%AD%A6%E4%B9%A0%E6%8C%87%E5%8D%97.md#postcss结合webpack应用)PostCSS结合Webpack应用


关于webpack基础配置的相关内容这里就不多说了~前面已有大神写了有兴趣可以[膜拜一下](http://git.oschina.net/janking/Infinite-f2e/issues/IDOHZ)。

我们先来创建一个项目目录，结构如下：（style0*.css作为我测试的文件，后面可能增加）

    
    ```
    |– dist
    |– src
    | |– images
    | | |– postcss-00.png
    | | |– postcss-01.png
    | – index.js
    | – index.html
    | – style04.sss
    |– postcss.config.js
    |– webpack.config.js
    |– package.json
    ```


接下来安装依赖包：

`npm i -D postcss-loader style-loader css-loader webpack webpack-dev-server`

然后修改已下文件，请仔细阅读![:stuck_out_tongue_closed_eyes:](https://assets-cdn.github.com/images/icons/emoji/unicode/1f61d.png)

package.json




    
    <span class="pl-s"><span class="pl-pds">"</span>scripts<span class="pl-pds">"</span></span><span class="pl-k">:</span> {
      <span class="pl-s"><span class="pl-pds">"</span>start<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>webpack-dev-server<span class="pl-pds">"</span></span>,
      <span class="pl-s"><span class="pl-pds">"</span>build<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>webpack<span class="pl-pds">"</span></span>
    },





先来个简单的试试：

webpack.config.js




    
    <span class="pl-k">var</span> path <span class="pl-k">=</span> <span class="pl-c1">require</span>(<span class="pl-s"><span class="pl-pds">'</span>path<span class="pl-pds">'</span></span>);
    <span class="pl-c1">module</span>.<span class="pl-smi">exports</span> <span class="pl-k">=</span> {
      entry<span class="pl-k">:</span> {
        index<span class="pl-k">:</span> <span class="pl-smi">path</span>.<span class="pl-en">resolve</span>(<span class="pl-c1">__dirname</span>, <span class="pl-s"><span class="pl-pds">'</span>src/index.js<span class="pl-pds">'</span></span>)
      },
      output<span class="pl-k">:</span> {
        filename<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>[name].js<span class="pl-pds">'</span></span>,
        path<span class="pl-k">:</span> <span class="pl-smi">path</span>.<span class="pl-en">resolve</span>(<span class="pl-c1">__dirname</span>, <span class="pl-s"><span class="pl-pds">'</span>dist<span class="pl-pds">'</span></span>)
      },
      module<span class="pl-k">:</span> {
        rules<span class="pl-k">:</span> [{
          test<span class="pl-k">:</span><span class="pl-sr"> <span class="pl-pds">/</span><span class="pl-cce">\.</span>sss<span class="pl-k">$</span><span class="pl-pds">/</span></span>,
          exclude<span class="pl-k">:</span><span class="pl-sr"> <span class="pl-pds">/</span>node_modules<span class="pl-pds">/</span></span>,
          use<span class="pl-k">:</span> [{
              loader<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>style-loader<span class="pl-pds">'</span></span>,
            },
            {
              loader<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>css-loader<span class="pl-pds">'</span></span>,
              options<span class="pl-k">:</span> {
                importLoaders<span class="pl-k">:</span> <span class="pl-c1">1</span>,
              }
            },
            {
              loader<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>postcss-loader<span class="pl-pds">'</span></span>
            }
          ]
        }]
      },
      devServer<span class="pl-k">:</span> {
        contentBase<span class="pl-k">:</span> <span class="pl-c1">__dirname</span>,
        compress<span class="pl-k">:</span> <span class="pl-c1">true</span>,
        port<span class="pl-k">:</span> <span class="pl-c1">9000</span>,
        inline<span class="pl-k">:</span> <span class="pl-c1">true</span>,
        hot<span class="pl-k">:</span> <span class="pl-c1">true</span>,
        host<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>0.0.0.0<span class="pl-pds">'</span></span>,
        disableHostCheck<span class="pl-k">:</span> <span class="pl-c1">true</span>
      }
    }





postcss.config.js




    
    <span class="pl-c1">module</span>.<span class="pl-smi">exports</span> <span class="pl-k">=</span> {
      parser<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>sugarss<span class="pl-pds">'</span></span>,
      plugins<span class="pl-k">:</span> [
        <span class="pl-c1">require</span>(<span class="pl-s"><span class="pl-pds">'</span>precss<span class="pl-pds">'</span></span>),
        <span class="pl-c1">require</span>(<span class="pl-s"><span class="pl-pds">'</span>autoprefixer<span class="pl-pds">'</span></span>)
      ]
    }





读完了应该发现此刻运行肯定会出错的~因为还没有安装其他跟PostCSS相关的插件呢，于是继续安装：

`npm i -D sugarss precss autoprefixer`

（插件简单介绍，[sugarss](https://github.com/postcss/sugarss)是比较特别的css语法，我尚未了解到这样写的好处，仅供大家学习参考。[precss](https://github.com/jonathantneal/precss)功能就很强悍了，类似sass的一些功能。[autoprefixer](https://github.com/postcss/autoprefixer)就不用多说啦！）

index.html




    
    <!DOCTYPE html>
    <<span class="pl-ent">html</span> <span class="pl-e">lang</span>=<span class="pl-s"><span class="pl-pds">"</span>en<span class="pl-pds">"</span></span>>
    <<span class="pl-ent">head</span>>
      <<span class="pl-ent">meta</span> <span class="pl-e">charset</span>=<span class="pl-s"><span class="pl-pds">"</span>UTF-8<span class="pl-pds">"</span></span>>
      <<span class="pl-ent">meta</span> <span class="pl-e">name</span>=<span class="pl-s"><span class="pl-pds">"</span>viewport<span class="pl-pds">"</span></span> <span class="pl-e">content</span>=<span class="pl-s"><span class="pl-pds">"</span>width=device-width, initial-scale=1.0<span class="pl-pds">"</span></span>>
      <<span class="pl-ent">meta</span> <span class="pl-e">http-equiv</span>=<span class="pl-s"><span class="pl-pds">"</span>X-UA-Compatible<span class="pl-pds">"</span></span> <span class="pl-e">content</span>=<span class="pl-s"><span class="pl-pds">"</span>ie=edge<span class="pl-pds">"</span></span>>
      <<span class="pl-ent">title</span>>这是一个用于PostCSS测试的页面</<span class="pl-ent">title</span>>
    </<span class="pl-ent">head</span>>
    <<span class="pl-ent">body</span>>
      <<span class="pl-ent">div</span> <span class="pl-e">class</span>=<span class="pl-s"><span class="pl-pds">"</span>test<span class="pl-pds">"</span></span>>
        <<span class="pl-ent">p</span> <span class="pl-e">class</span>=<span class="pl-s"><span class="pl-pds">"</span>multiline<span class="pl-pds">"</span></span>>this is a container</<span class="pl-ent">p</span>>
      </<span class="pl-ent">div</span>>
      <<span class="pl-ent">script</span> <span class="pl-e">src</span>=<span class="pl-s"><span class="pl-pds">"</span>../dist/index.js<span class="pl-pds">"</span></span>><span class="pl-s1"><</span>/<span class="pl-ent">script</span>>
    </<span class="pl-ent">body</span>>
    </<span class="pl-ent">html</span>>





style04.sss




    
    <span class="pl-smi">$blue</span>: <span class="pl-c1">#056ef0</span>
    
    .test 
      box<span class="pl-c1">-</span>sizing: border<span class="pl-c1">-</span>box
      padding:<span class="pl-c1"> 50</span><span class="pl-k">px</span>
      border:<span class="pl-c1"> 10</span><span class="pl-k">px</span> <span class="pl-c1">solid</span> <span class="pl-smi">$blue</span>
      width:<span class="pl-c1"> 200</span><span class="pl-k">px</span>
      height:<span class="pl-c1"> 200</span><span class="pl-k">px</span>
    
    .multiline,
    .selector
      box<span class="pl-c1">-</span>shadow:<span class="pl-c1"> 1</span><span class="pl-k">px</span><span class="pl-c1"> 0 9</span><span class="pl-k">px</span> <span class="pl-c1">rgba</span>(<span class="pl-c1">0, 0, 0</span>,<span class="pl-c1"> .4</span>),
    <span class="pl-c1">              1</span><span class="pl-k">px</span><span class="pl-c1"> 0 3</span><span class="pl-k">px</span> <span class="pl-c1">rgba</span>(<span class="pl-c1">0, 0, 0</span>,<span class="pl-c1"> .6</span>)





基本工作大功告成，开两个终端跑两条命令试试看。

`npm run start`

`npm run build`

一切运行OK，接下来访问[http://localhost:9000/src/，看起来也都还不错。当然写到这里只是介绍了如何结合webpack使用PostCSS。而实际项目应用中，我目前还在探索更多实用的插件，构建一个基本可以替代SASS，LESS等](http://localhost:9000/src/%EF%BC%8C%E7%9C%8B%E8%B5%B7%E6%9D%A5%E4%B9%9F%E9%83%BD%E8%BF%98%E4%B8%8D%E9%94%99%E3%80%82%E5%BD%93%E7%84%B6%E5%86%99%E5%88%B0%E8%BF%99%E9%87%8C%E5%8F%AA%E6%98%AF%E4%BB%8B%E7%BB%8D%E4%BA%86%E5%A6%82%E4%BD%95%E7%BB%93%E5%90%88webpack%E4%BD%BF%E7%94%A8PostCSS%E3%80%82%E8%80%8C%E5%AE%9E%E9%99%85%E9%A1%B9%E7%9B%AE%E5%BA%94%E7%94%A8%E4%B8%AD%EF%BC%8C%E6%88%91%E7%9B%AE%E5%89%8D%E8%BF%98%E5%9C%A8%E6%8E%A2%E7%B4%A2%E6%9B%B4%E5%A4%9A%E5%AE%9E%E7%94%A8%E7%9A%84%E6%8F%92%E4%BB%B6%EF%BC%8C%E6%9E%84%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%9F%BA%E6%9C%AC%E5%8F%AF%E4%BB%A5%E6%9B%BF%E4%BB%A3SASS%EF%BC%8CLESS%E7%AD%89)

参考文献：

[webpack官方说明：postcss-loader](https://webpack.js.org/loaders/postcss-loader/)


## [](https://github.com/whidy/postcss-study/blob/master/PostCSS%E5%AD%A6%E4%B9%A0%E6%8C%87%E5%8D%97.md#postcss结合gulp应用)PostCSS结合Gulp应用


Gulp我用的很少，不是很熟悉，这里结合官方一些和自己尝试的DEMO进行说明。

我基于之前的代码来继续补充内容。

安装Gulp相关的包：

`npm run i -D gulp gulp-postcss gulp-sourcemaps`

增加Gulp配置文件[gulpfile.js](https://github.com/whidy/postcss-study/blob/master/gulpfile.js)，页面[index2.html](https://github.com/whidy/postcss-study/blob/master/src/index2.html)，样式[style05.css](https://github.com/whidy/postcss-study/blob/master/src/style05.css)，修改package.json的script如下：

[gulpfile.js](https://github.com/whidy/postcss-study/blob/master/gulpfile.js)




    
    <span class="pl-k">var</span> postcss <span class="pl-k">=</span> <span class="pl-c1">require</span>(<span class="pl-s"><span class="pl-pds">'</span>gulp-postcss<span class="pl-pds">'</span></span>);
    <span class="pl-k">var</span> gulp <span class="pl-k">=</span> <span class="pl-c1">require</span>(<span class="pl-s"><span class="pl-pds">'</span>gulp<span class="pl-pds">'</span></span>);
    
    <span class="pl-smi">gulp</span>.<span class="pl-en">task</span>(<span class="pl-s"><span class="pl-pds">'</span>css<span class="pl-pds">'</span></span>, <span class="pl-k">function</span> () {
      <span class="pl-k">var</span> postcss <span class="pl-k">=</span> <span class="pl-c1">require</span>(<span class="pl-s"><span class="pl-pds">'</span>gulp-postcss<span class="pl-pds">'</span></span>);
      <span class="pl-k">var</span> sourcemaps <span class="pl-k">=</span> <span class="pl-c1">require</span>(<span class="pl-s"><span class="pl-pds">'</span>gulp-sourcemaps<span class="pl-pds">'</span></span>);
    
      <span class="pl-k">return</span> <span class="pl-smi">gulp</span>.<span class="pl-en">src</span>(<span class="pl-s"><span class="pl-pds">'</span>src/style05.css<span class="pl-pds">'</span></span>)
        .<span class="pl-en">pipe</span>(<span class="pl-smi">sourcemaps</span>.<span class="pl-en">init</span>())
        .<span class="pl-en">pipe</span>(<span class="pl-en">postcss</span>([<span class="pl-c1">require</span>(<span class="pl-s"><span class="pl-pds">'</span>precss<span class="pl-pds">'</span></span>), <span class="pl-c1">require</span>(<span class="pl-s"><span class="pl-pds">'</span>autoprefixer<span class="pl-pds">'</span></span>)]))
        .<span class="pl-en">pipe</span>(<span class="pl-smi">sourcemaps</span>.<span class="pl-c1">write</span>(<span class="pl-s"><span class="pl-pds">'</span>.<span class="pl-pds">'</span></span>))
        .<span class="pl-en">pipe</span>(<span class="pl-smi">gulp</span>.<span class="pl-en">dest</span>(<span class="pl-s"><span class="pl-pds">'</span>dist/<span class="pl-pds">'</span></span>));
    });





[index2.html](https://github.com/whidy/postcss-study/blob/master/src/index2.html)




    
    <!DOCTYPE html>
    <<span class="pl-ent">html</span> <span class="pl-e">lang</span>=<span class="pl-s"><span class="pl-pds">"</span>en<span class="pl-pds">"</span></span>>
    <<span class="pl-ent">head</span>>
      <<span class="pl-ent">meta</span> <span class="pl-e">charset</span>=<span class="pl-s"><span class="pl-pds">"</span>UTF-8<span class="pl-pds">"</span></span>>
      <<span class="pl-ent">meta</span> <span class="pl-e">name</span>=<span class="pl-s"><span class="pl-pds">"</span>viewport<span class="pl-pds">"</span></span> <span class="pl-e">content</span>=<span class="pl-s"><span class="pl-pds">"</span>width=device-width, initial-scale=1.0<span class="pl-pds">"</span></span>>
      <<span class="pl-ent">meta</span> <span class="pl-e">http-equiv</span>=<span class="pl-s"><span class="pl-pds">"</span>X-UA-Compatible<span class="pl-pds">"</span></span> <span class="pl-e">content</span>=<span class="pl-s"><span class="pl-pds">"</span>ie=edge<span class="pl-pds">"</span></span>>
      <<span class="pl-ent">title</span>>这是一个用于PostCSS测试的页面(gulp)</<span class="pl-ent">title</span>>
      <<span class="pl-ent">link</span> <span class="pl-e">href</span>=<span class="pl-s"><span class="pl-pds">"</span>../dist/style05.css<span class="pl-pds">"</span></span> <span class="pl-e">rel</span>=<span class="pl-s"><span class="pl-pds">"</span>stylesheet<span class="pl-pds">"</span></span>>
    </<span class="pl-ent">head</span>>
    <<span class="pl-ent">body</span>>
      <<span class="pl-ent">div</span> <span class="pl-e">class</span>=<span class="pl-s"><span class="pl-pds">"</span>test<span class="pl-pds">"</span></span>>
        <<span class="pl-ent">p</span> <span class="pl-e">class</span>=<span class="pl-s"><span class="pl-pds">"</span>box<span class="pl-pds">"</span></span>>this is a box</<span class="pl-ent">p</span>>
        <<span class="pl-ent">p</span> <span class="pl-e">class</span>=<span class="pl-s"><span class="pl-pds">"</span>box<span class="pl-pds">"</span></span>>this is another box</<span class="pl-ent">p</span>>
      </<span class="pl-ent">div</span>>
    </<span class="pl-ent">body</span>>
    </<span class="pl-ent">html</span>>





[style05.css](https://github.com/whidy/postcss-study/blob/master/src/style05.css)




    
    <span class="pl-c">/* gulp下测试 */</span>
    <span class="pl-v">$blue</span>: <span class="pl-c1">#056ef0</span>;
    <span class="pl-e">.test</span> {
      <span class="pl-c1">display</span>: <span class="pl-c1">flex</span>;
      <span class="pl-c1">color</span>: <span class="pl-v">$blue</span>;
      <span class="pl-e">.box</span> {
        <span class="pl-c1">flex</span>:<span class="pl-c1"> 1</span>;
      }
    }





[package.json](https://github.com/whidy/postcss-study/blob/master/package.json)的scripts部分如下




    
    <span class="pl-s"><span class="pl-pds">"</span>scripts<span class="pl-pds">"</span></span><span class="pl-k">:</span> {
      <span class="pl-s"><span class="pl-pds">"</span>start<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>webpack-dev-server<span class="pl-pds">"</span></span>,
      <span class="pl-s"><span class="pl-pds">"</span>build<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>webpack<span class="pl-pds">"</span></span>,
      <span class="pl-s"><span class="pl-pds">"</span>gulp<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>gulp css<span class="pl-pds">"</span></span>
    },





一切就绪后，我们来执行伟大的命令了：

`npm run gulp`

我的电脑等待了约1.26s<del>1.29s，提示finish啦</del>

和之前相同，我这里依旧采用了webpack-dev-server启动的服务器（当然这个又依赖webpack配置，除非你将配置直接写入package.json内），那么你当然也可以使用其他自己喜欢的服务器（例如[http-server](https://github.com/indexzero/http-server)），我们依旧先启动服务器npm run start，然后访问本地[http://localhost:9000/src/index2.html就可以看到效果了。或者你也可以直接去看dist目录内生成出来的style05.css文件，一切都是那么美好](http://localhost:9000/src/index2.html%E5%B0%B1%E5%8F%AF%E4%BB%A5%E7%9C%8B%E5%88%B0%E6%95%88%E6%9E%9C%E4%BA%86%E3%80%82%E6%88%96%E8%80%85%E4%BD%A0%E4%B9%9F%E5%8F%AF%E4%BB%A5%E7%9B%B4%E6%8E%A5%E5%8E%BB%E7%9C%8Bdist%E7%9B%AE%E5%BD%95%E5%86%85%E7%94%9F%E6%88%90%E5%87%BA%E6%9D%A5%E7%9A%84style05.css%E6%96%87%E4%BB%B6%EF%BC%8C%E4%B8%80%E5%88%87%E9%83%BD%E6%98%AF%E9%82%A3%E4%B9%88%E7%BE%8E%E5%A5%BD)~


## [](https://github.com/whidy/postcss-study/blob/master/PostCSS%E5%AD%A6%E4%B9%A0%E6%8C%87%E5%8D%97.md#postcss学习心得及总结)PostCSS学习心得及总结


因为这次学习，纯粹是根据“教科书”来学，来讲解的，因此也就没有什么真正的精髓，我也是才开始接触PostCSS，文中有错误之处还请指正。我希望以后在项目中尽可能的用好PostCSS，再次带来一篇简短而有力的文章分享给大家。因时间和精力有限希望这篇文章能给大家带来些帮助。目前能想到的，还有一些未来需要补充的内容包括：



 	
  1. sourcemaps

 	
  2. 是否有移动端基于PostCSS的自适应解决方案

 	
  3. 自己写个可能会比较实用的插件

 	
  4. 结合[postcss-sass](https://github.com/AleshaOleg/postcss-sass)究竟有什么好处

 	
  5. postcss对图片和字体等资源文件处理


暂时想到这些，如果你还有一些想到的欢迎在下面留言哦![:kissing_heart:](https://assets-cdn.github.com/images/icons/emoji/unicode/1f618.png)


<blockquote>其他参考文献汇总：

**[PostCSS Deep Dive](https://webdesign.tutsplus.com/series/postcss-deep-dive--cms-889)**（强烈推荐！我看完了才发现有部分译文：[PostCSS深入学习](http://www.w3cplus.com/PostCSS/postcss-deep-dive-what-you-need-to-know.html)）

[PostCSS深入学习: PostCSS和Sass、Stylus或LESS一起使用](https://www.w3cplus.com/PostCSS/using-postcss-together-with-sass-stylus-or-less.html)

[PostCSS 是个什么鬼东西？](https://segmentfault.com/a/1190000003909268)

[PostCSS一种更优雅、更简单的书写CSS方式](http://www.cnblogs.com/givebest/p/4771154.html)

[PostCSS及其常用插件介绍](http://www.css88.com/archives/7317)

[PostCSS – A Comprehensive Introduction](https://www.smashingmagazine.com/2015/12/introduction-to-postcss/)

[http://www.cnblogs.com/terrylin/p/5229169.html](http://www.cnblogs.com/terrylin/p/5229169.html)

相当不错的PPT形式

[https://ai.github.io/about-postcss/en/](https://ai.github.io/about-postcss/en/)

postcss的优势

[From Sass to PostCSS](https://pawelgrzybek.com/from-sass-to-postcss/)

[PostCSS – Sass Killer or Preprocessing Pretender?](https://ashleynolan.co.uk/blog/postcss-a-review)</blockquote>

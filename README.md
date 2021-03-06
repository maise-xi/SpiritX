<h1>SpiritXJs（α）</h1>
<ul>
    <li>背景</li>
    <li>快速使用</li>
    <li>基本思想</li>
    <li>类与目录</li>
    <li>相关工作</li>
    <li>未来</li>
</ul>

<h2>背景</h2>
<ul>
    <li>
        <p>什么是SpiritXJs？</p>
        <p>一种可维护的前端解决方案，核心为一个轻量级的JS框架以及一些基础组件库（我们更倾向于表述为一种代码风格）。</p>
    </li>
    <li>
        <p>为什么使用SpiritXJs？</p>
        <p>SpiritXJs的原始动机是为了解决处于快速迭代阶段的大型Web应用的可维护性问题。相比于AngularJS、React.js等目前流行的前端解决方案，虽然都采用了组件化等类似的思想，SpiritXJs的出发点是对前端业务逻辑的抽象。即其主要解决两个问题——JS与html的关系、组件的抽象模型（组件是什么？）</p>
        <p>SpiritXJs参考了AngularJS以及React.js的主要优势，以及ES6与Angular2.0的基本思想，完成了对前端业务逻辑的基本抽象。其主要有以下几个特性：</p>
        <ul>
            <li>以组件为中心</li>
            <li>数据驱动</li>
            <li>面向对象的代码风格</li>
        </ul>
        <p>面向构建易于维护的（迅速响应快速变化的需求）大型、单页Web应用。</p>
    </li>
</ul>

<h2>快速使用</h2>
<h3><a href="http://182.92.1.178:8080/demo/js/spirits/biz/demo/SampleBootstrap/index.html">示例</a></h3>
<h3>开始</h3>
<ul>
<li>
    <p>环境配置</p>
    <p>建立如下目录结构</p>
<pre>
<code>
    - demo
      - js
        - lib
          - BF     // SpiritXJs 基础库
        - spirits
          - biz    // 业务逻辑
          - component
          - widget
        - static   // 静态文件目录
      plugin-text.js
      sea.js
      seaconfig.js
</code>
</pre>
    <p>上面的目录结构不是必须的，就目前而言，我们所需要的一些资源为
    <ol>
        <li>spirit基础库文件夹BF</li>
        <li>jquery</li>
        <li>
            <p>sea.js以及其配置文件seaconfig.js</p>
            <p>seaconfig.js</p>
<pre>
<code>
    seajs.config({
        base: '/demo/js/',
        paths : {
            bf: 'lib/BF',
            widget: 'spirits/widget',
            component: 'spirits/component',
            biz: 'spirits/biz'
        }
    });
</code>
</pre>
            <p>这里我们需要指定spirit基础库的路径bf</p>
        </li>
    </ol>
    </p>
</li>

<li>
    <p>创建第一个Spirit</p>
    <p>SampleBootstrap.js</p>
<pre>
<code>
define(function(require, exports, module) {
    var BFView = require('bf/BFBase/BFView');
    var __tpl__ = require('biz/demo/SampleBootstrap/SampleBootstrap.tpl');

    var SampleBootstrap = function (container, model, tpl) {
        tpl = tpl == null ? __tpl__ : tpl;
        this.__proto__ = new BFView(container, model, tpl);
        var self = this.profile.instance = this;
    }

    module.exports = SampleBootstrap;
});
</code>
</pre>
    <p>SampleBootstrap.tpl</p>
<pre>
<code>
    &lt;div id="{$DOM_ID}"&gt;
        &lt;p style="font-size: 48px; text-align: center;"&gt;hello, egg&lt;/p&gt;
        &lt;p style="font-size: 48px; color: #efefef; text-align: center;"&gt;最大的不同，即是处处都不同&lt;/p&gt;
        &lt;div class="bui-info"&gt;
            &lt;label class="bui-column bui-label-large pt5"&gt;组件示例&lt;/label&gt;
            &lt;div class="bui-row"&gt;
                &lt;label class="bui-column-thin bui-label tr"&gt;可搜索下拉框：&lt;/label&gt;
                &lt;div style="width: 250px; position: relative;" bf-container="SampleSearchSelect"&gt;&lt;/div&gt;
            &lt;/div&gt;
            &lt;div class="bui-row"&gt;
                &lt;label class="bui-column-thin bui-label tr"&gt;表格：&lt;/label&gt;
                &lt;div style="width: 600px;" bf-container="SampleTable"&gt;&lt;/div&gt;
            &lt;/div&gt;
        &lt;/div&gt;
        &lt;div class="bui-info"&gt;
            &lt;label class="bui-column bui-label-large pt5"&gt;数据绑定示例&lt;/label&gt;
            &lt;div class="bui-row"&gt;
                &lt;label class="bui-column-thin bui-label tr"&gt;Input1：&lt;/label&gt;
                &lt;input class="w250" type="text" bf-dom="input1"&gt;
            &lt;/div&gt;
            &lt;div class="bui-row"&gt;
                &lt;label class="bui-column-thin bui-label tr"&gt;Input2：&lt;/label&gt;
                &lt;input class="w250" type="text" bf-dom="input2"&gt;
            &lt;/div&gt;
            &lt;div class="bui-row"&gt;
                &lt;label class="bui-column-thin bui-label tr"&gt;span1：&lt;/label&gt;
                &lt;span bf-dom="span1"&gt;&lt;/span&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
</code>
</pre>
    <p>index.html</p>
<pre>
<code>
    &lt;!DOCTYPE html&gt;
    &lt;html&gt;
    &lt;head&gt;
        &lt;title&gt;SpiritX&lt;/title&gt;
        &lt;link rel="stylesheet" type="text/css" href="/demo/js/static/css/mobase.css"&gt;
        &lt;link rel="stylesheet" type="text/css" href="/demo/js/static/css/global.css"&gt;
        &lt;link rel="stylesheet" type="text/css" href="/demo/js/static/css/hui_iconfont_v1.0.6/iconfont.css"&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;script src="http://apps.bdimg.com/libs/jquery/1.11.1/jquery.min.js"&gt;&lt;/script&gt;
        &lt;!--&lt;script src="/demo/js/sea.js"&gt;&lt;/script&gt;--&gt;
        &lt;script src="//cdn.bootcss.com/seajs/2.0.0/sea.js"&gt;&lt;/script&gt;
        &lt;script src="/demo/js/plugin-text.js"&gt;&lt;/script&gt;
        &lt;script src="/demo/js/seaconfig.js"&gt;&lt;/script&gt;
        &lt;script&gt;
            seajs.use('biz/app/MyApp', function(MyApp) {
            window.myApp = myApp = new MyApp();
            myApp.run().then(function (ret) {
            seajs.use('biz/demo/SampleBootstrap/SampleBootstrap', function(SampleBootstrap) {
                var sampleBootstrap = new SampleBootstrap($('body'), {});
                sampleBootstrap.render();
                });
            });
        });
        &lt;/script&gt;
    &lt;/body&gt;
    &lt;/html&gt;
</code>
</pre>
    <p>好了，使用本地服务器（例如phpStorm编辑器内置的）打开index.html看看效果吧！</p>
</li>
<li>
    <p>加载一些Spirit</p>
    <p>修改SampleBootstrap.js</p>
<pre>
<core>
define(function(require, exports, module) {
    /**
     * base
     */
    var BFView = require('bf/BFBase/BFView');
    var __tpl__ = require('biz/demo/SampleBootstrap/SampleBootstrap.tpl');

    /**
     * css
     */
    require('biz/demo/SampleBootstrap/SampleBootstrap.css');

    /**
     * spirit
     */
    var BUISearchSelect = require('bf/BUIComponent/BUISearchSelect/BUISearchSelect');
    var BUIPaginTable   = require('bf/BUIComponent/BUIPaginTable/BUIPaginTable');
    var SwitchOnOff     = require('component/SwitchOnOff/SwitchOnOff');
    var TableOpList     = require('widget/TableOpList/TableOpList');

    var SampleBootstrap = function (container, model, tpl) {
        tpl = tpl == null ? __tpl__ : tpl;
        this.__proto__ = new BFView(container, model, tpl);
        var self = this.profile.instance = this;


        self.buildDomModelSet = function () {
            self.bindDomModel('self.profile.model.input1', 'input1', 'value');
            self.bindDomModel('self.profile.model.input1', 'input2', 'value');
            self.bindDomModel('self.profile.model.input1', 'span1', 'html');
        }

        self.buildSpiritSet = function () {
            var container = self.findDom('bf-container', 'SampleSearchSelect');
            var sampleSearchSelect = new BUISearchSelect(container, {1: 'gray', 2: 'ly'});
            sampleSearchSelect.render();
            sampleSearchSelect.setValueByKey(2);
            self.addSpirit('sampleSearchSelect', sampleSearchSelect);

            var container = self.findDom('bf-container', 'SampleTable');
            var model = {
                delegate: self.getInstance(),
                pagination: {
                    totalCount: 3,
                    currentPage: 1,
                    pageSize: 10
                },
                table: {
                    title: [
                        {
                            orderBy: 1,
                            content: 'name',
                            activeOrderBy: true,
                            width: '100px'
                        },
                        {
                            content:'city'
                        }, {
                            orderBy: -1,
                            content: 'order'
                        }],
                    itemList: [
                        ['coco', 'sh', 'a'],
                        ['ly', {
                            class: SwitchOnOff,
                            key: 'switch_ly',
                            model: {delegate: self.getInstance(), value: 'on'}
                        }, 'b'],
                        ['gray', {
                            class: SwitchOnOff,
                            key: 'switch_gray',
                            model: {delegate: self.getInstance(), value: 'off'}
                        }, 'c'],
                    ]
                }
            }
            var sampleTable = new BUIPaginTable(container, model);
            sampleTable.setKey('sampleTable');
            sampleTable.render();
            self.addSpirit('sampleTable', sampleTable);
        }

        self.onSwitchClick = function (spirit, value) {
            alert(spirit.getKey() + ' now is ' + value);
        }

        self.onPageRefreshed = function (spirit, page) {
            alert('page ' + page);
        }

        self.onTableOrderBy = function (spirit, index, value) {
            var order = value === 1 ? 'desc' : 'asc';
            alert('column ' + index + ' ' + order);
        }
    }

    module.exports = SampleBootstrap;
});
</core>
</pre>
    <p>刷新一下index.html看看有什么变化！</p>
    <p>【Spirit的构造与渲染】具体地，以下三行代码即可加载一个Spirit</p>
<pre>
<code>
    var container = self.findDom('bf-container', 'SampleSearchSelect');
    var sampleSearchSelect = new BUISearchSelect(container, {1: 'gray', 2: 'ly'});
    sampleSearchSelect.render();
</code>
</pre>
    <p>第一行获取Spirit的挂载点，在模板文件中通过<code>bf-container="SampleSearchSelect"</code>来指定挂载点及key，bf-container的值仅需要在spirit自身的tpl下确保唯一；第二行构造Spirit；第三行渲染Spirit。</p>
	<p>【Spirit的委托与代理】上述三行代码我们构造并渲染了一个可搜索下拉框。对于其它一些Spirit（例如表格或开关），除了构造与渲染，我们还需要实现对应的代理方法。例如：</p>
<pre>
<code>
    self.onSwitchClick = function (spirit, value) {
        alert(spirit.getKey() + ' now is ' + value);
    }
</code>
</pre>
	<p>上面三行代码实现了BUISearchSelect（开关Spirit）的onSwitchClick方法，该代理方法在BUISearchSelect实例的on/off状态改变时被调用，宿主Spirit（这里即是SampleBootstrap）通过BUISearchSelect的getKey方法判断是哪一个开关Spirit的实例（通过setKey方法指定一个spirit的key）。需要强调的是，这种思想（委托-代理）在SpiritXJs中被广泛使用。</p>
	<p>【Spirit集合】BFView维护一个spiritSet集合，其中包含了该Spirit的所有sub Spirit。下面几行代码演示了spiritSet的相关操作：</p>
<pre>
<code>
    self.addSpirit('sampleSearchSelect', sampleSearchSelect); //添加一个sub spirit
    self.getSpirit('sampleSearchSelect');      //获取一个 sub spirit
    self.removeSpirit('sampleSearchSelect');   //移除一个 sub spirit
</code>
</pre>
    <p>注意，removeSpirit方法将会结束一个spirit的生命周期。更具体的内容参考【类与目录】章节。</p>
    <p>【模板变量】在tpl文件中，通过{$xxx}的语法形式声明模板变量，使用BFUtil.replaceTpl方法进行模板变量的替换。Spirit的模板文件中第一行的{$DOM_ID}不可省略。该模板变量为每个Spirit的实例动态生成全局唯一的id。</p>
    <p>需要注意的是，在SpiritX中，模板只是用于确定Spirit在dom树上的布局（Spirit的层次结构），并不承载实际的业务逻辑。因此SpiritX的模板变量只是用于初始化，不应当被滥用。</p>
</li>
</ul>

<h2>基本思想</h2>
<ul>
    <li>
        <p>基本概念</p>
        <p>前端特殊性：html与JS的分离</p>
        <p>前端业务逻辑：一段html片段的业务逻辑是其所有交互事件及其处理逻辑的总和</p>
        <p>可维护性：业务逻辑的可复用性与可扩展性</p>
    </li>
    <li>
        <p>基本定义</p>
        <p>【Spirit】是对一段html片段及其业务逻辑的抽象</p>
        <p>【Spirit】标准构造函数</p>
<pre>
<code>
    var BFView = function (container, model, tpl)
</code>
</pre>
    </li>
    <li>
        <p>Spirit</p>
        <p>生命周期</p>
        <ul>
            <li>
                <p>构造（new）</P>
                <p>initModel<p>
            </li>
            <li>
                <p>渲染（render）<p>
                <p>initModel</p>
                <p>BuildDomSet</p>
                <p>BuildDomModelSet</p>
                <p>BuildSpirit</p>
            </li>
            <li>
                <p>移除（remove）</p>
            </li>
        </ul>

        <p>通信</p>
        <ul>
            <li>广泛使用委托-代理</li>
        </ul>
        <p>Spirit开发流程</p>
        <ul>
            <li>确定边界</li>
                <ul>
                    <li>model</li>
                    <li>接口</li>
                    <li>委托</li>
                </ul>
            <li>业务逻辑实现
                <ul>
                    <li>tpl设计</li>
                    <li>spirit选择</li>
                    <li>生命周期方法</li>
                        <ul>
                            <li>initModel</li>
                            <li>BuildDomSet</li>
                            <li>BuildDomModelSet</li>
                            <li>BuildSpirit</li>
                        </ul>
                    <li>业务逻辑实现（代理、接口、委托）</li>
                </ul>
            </li>
        </ul>
    </li>
</ul>
<h2>类与目录</h2>
<ul>
    <li>BFView
		<ul>
			<li>initModel</li>
			<li>render</li>
			<li>replaceTpl</li>
			<li>buildDomSet</li>
			<li>buildDomModelSet</li>
			<li>buildSpiritSet</li>
			<li>bindDomModel</li>
			<li>getContainer</li>
			<li>addDom</li>
			<li>removeDom</li>
			<li>getSpirit</li>
			<li>addSpirit</li>
			<li>removeSpirit</li>
			<li>updateModel</li>
			<li>onModelUpdated</li>
			<li>getSubDom</li>
			<li>remove</li>
			<li>getDID</li>
			<li>getDom</li>
			<li>getKey</li>
			<li>setKey</li>
			<li>getInstance</li>
			<li>getModel</li>
			<li>findDom</li>
		</ul>
	</li>
</ul>
<h2>相关工作</h2>
<ul>
    <li>
        <p>AngularJS</p>
    </li>
    <li>
        <p>React.js</p>
    </li>
    <li>
        <p>ECMAScript 6（ES6）</p>
    </li>
    <li>
        <p>Angular2.0</p>
    </li>
</ul>
<h2>未来</h2>
<ul>
    <li>交互逻辑层的抽象</li>
    <li>Spirit模型完善</li>
    <li>Spirit生命周期完善</li>
    <li>Spirit级别的数据流</li>
    <li>样式</li>
    <li>编译与构建</li>
</ul>
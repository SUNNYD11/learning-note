## 2018-4-12
1. 安装环境：oh my zsh是一个拓展工具集，提供主题配置，插件机制，便捷操作。设置主题：ZSH_THEME="主题名"。homebrew，macOS软件包管理。git：分布式版本控制系统。nvm：node版本管理工具，区别于n作为一个node的模块，nvm是一个独立于node的外部shell脚本。npm：node包管理器。nrm：npm源管理器，用于切换npm下载源到指定到源。tnpm，阿里内幕npm。hpm：用于ios模拟器调试。

## 2018-4-16
1. 学习ES6：
- let：声明变量，只在代码块内有效。没有变量提升，应为绑定块级作用于，如果在声明变量前使用变量，该变量不可用，会暂时性死区，不允许重复声明，代替var。
- const：保证变量窒息指向到那个内存地址不得改动。简单类型到数据，值就保存在内存地址，等于常量。复合类型数据内存地址保存到只是一个指针，const只能保证这个指针是固定到，指向到数据结构是可变到。let和const尽量使用const。可以提醒别人该变量不能改变，同时编译器会对const进行优化，有利于提高运行效率
- set/map：set用于生成类似数组的数据结构，成员的值是唯一的。map结构提供了值-值对应，对于键值对对数据结构，map比object（只提供字符串-值对对应）更合适。等用法和规范。
参考：http://es6.ruanyifeng.com/
2. 了解git基本操作和分支。
参考：https://git-scm.com/book/zh/v2

## 2018-4-17
1. JSX：一种js对语法拓展。可以在jsx中任意使用js表达式。
2. less.js：css预处理语言，拓展了css，增加了变量、mixin、函数等特性，更易维护和扩展。允许使用变量：@color：red➡a{color：@color}。可以将一个定义好的class a引入另一个class b中，还可以类似函数那样带参数调用。可以通过嵌套来实现继承。提供运算操作。
3. bx-mobile，移动端组件库。bx-util，保险工具集合。bx-sdk，保险业务功能组件。

## 2018-4-18
1. git远程仓库操作：
- 添加 remote add shortname url
- 查看 remote -v
- 抓取 fetch origin
- 推送 push origin branch-name（先拉取合并再推送）/push -f
2. React（虚拟DOM，组建化，单向数据流）: 
- JSX语法生成react元素，ReactDOM.render()渲染。
- this.props表示定义了就无法改变的特性（父级分发下来的属性）。当rect遇到当元素是自定义组件，会将jsx属性作为单个对象传给该组件，对象成为props。react组件必须想纯函数一样使用props，同样的输入同样的输出。this.state表示可随用户互动产生改变的特性（组建内部自行管理的状态）。
- keys表示哪个项被修改添加移除，数组中 对每一个元素都应该有一个唯一不变的keys标示（降低算法复杂度）。
- 生命周期：
  - componentDidMount() 组建插入真实DOM以后执行
  - componentWillMount() 组建插入真实DOM之前执行
  - update() 正在重新渲染
  - unmount() 移出真实DOM
- 首次挂载流程：createclass创建自定义组件入口方法，负责管理生命中期中的getdafaultprops，该方法只执行一次，所有实例初始化的props将会被共享➡通过mountcomponent挂载组件，状态为mounting，利用getinitialstate获取初始化state，初始化更新队列。➡有componentwillmount就执行，调用setstate，进行state合并➡render获取更新后的this.state数据。➡有componentdidmount就执行。
- 可变状态使用setState()方法更新。
参考：https://zhuanlan.zhihu.com/p/20312691
3. Redux:解决React数据总是从顶层向下分发问题，作为顶层state分发给React应用。

## 2018-4-19
1. dva: 
- app=dva() 创建dva实例
- app.model namespace   命名，全局state属性
- state             设置初始值，表示状态数据，只能通过reducers改变
- reducers       设置修改state操作，通过action触发
- action           普通js对象，通过dispatch函数调用，改变相应数据，通过type属性指明具体行为
- dispach函数  触发action的方式，通过props访问dispatch，model外调用，添加type
- effects          异步行为触发effects 然后通过reducers改变state
- app.router
- app.start 启动

## 2018-4-23
1. 完成一次简单发布：
- git pull 拉到本地，checkout切换到代码分支,创建新分支进行修改
- 修改完代码，push origin将分支上传review。
2. 浏览团队文档,开发规范

## 2018-4-24
1. 学习DNS原理和解析过程：查找本地hosts→本地DNS解析器→本地DNS服务器→转发模式，上一级DNS服务器→上上级服务器，以此循环→返回本地DNS→客户机/非转发模式，请求发至13台根服务器，从顶级域→第二层域→子域，直到找到域名主机
2. HTTP缓存：
- pragma：设为no-cache表示不对资源缓存
- expires：设置缓存时间GMT
- cache-control：解决本地域服务器时间不统一问题，设置max-age设置缓存有效时间
- last-modified：判断缓存过期后，服务器有没有更新过资源，如果没有更新，返回304直接使用缓存
- etag：解决last-modified不准确（被修改，但是内容没有发生改变），给资源一个唯一标志符，更好                      判断资源是否被修改过。
3. 继续浏览团队文档

## 2018-4-25
1.学习了解node异步，内存控制，buffer，红黑树
2.mockjs：name|rule:value
2.浏览dva+react文档
3.继续浏览团队文档

## 2018-4-26
1. 修改页面：
- tnpm run mock，app服务器调到开发aaa,拉取迭代分支到本地并创建新分支。
- 利用flex根据sketch要求修改样式。
2. 理解代码：
- 入口初始化dva，引入models里到model
- model设置初始state，改变初始state到reducers
- effects从获取mock数据并触发reducers
- app.js设置dispatch触发reducers
- getdata获取数据后插入JSX语句中，react插入DOM节点生成页面

## 2018-4-27
1. 学习修改mock数据，不能随意修改字段，代码格式要规范
2. commit --amend修改最后一次提交
   push后需要新建分支再提交
   route：再用户操作无需请求服务器时，通过路由修改逻辑达到目的，根据url分配到对应到处理程序。
3. 不太清楚ali.call是什么

## 2018-4-28
1. 事件绑定：
- DOM直接绑定
- JS绑定
- 事件监听：addEventListen(event,function,usecapture(true捕获，false冒泡)
                     attachEvent(event(加on),function)
                     可以绑定多个事件，可接触事件，可为动态DOM元素动态添加事件
2. ali.call:还在研究中

## 2018-5-2
1. 函数调用：
- 方法调用，this绑定对象
- 正常函数调用，this绑定全局对象
- 构造函数调用，this绑定创建的新对象
- call/apply原型自带方法，第一个参数绑定this值，第二个参数传递参数，立即调用。
- bind类似call，生成新函数可随时调用。
2. super调用父类constructor，继承父类this对象。只能在子类构造函数中用，无法调用父类实例上的方法和属性，静态方法中指向父类，普通方法指向父类原型对象。
3. ail.toast会先把数据处理一下再执行ail.call(toast,...)
4. Hybrid模式：
- 弱化对网络链路对依赖，增强对设备能力对支持，增强用户体验
- H5基本类库zepto，antbridge提供和native之间的桥梁，将容器提供的接口封装，antUI提供UI组件
- Nebula：jsbridge通过console.log调用native的通讯避免兼容问题和页面假死。监听H5生命周期的事件，注入bridgejs，减少运行时间。魔术参数通过url带特定参数提前加载，优化用户体验。虚拟域名代替file路径。预渲染机制，先加载页面，后现实，优化用户体验。
- 离线方式，代码本地运行，数据走RPC。打包机制，将整个代码压缩成一个压缩包，应用平台通过拉取压缩包到本地后，读取里面内容。通过将tar直接读到内存中读取里面页面。
- 离线包渲染过程：加载全局包，解包到内存，判断是否安装该版本离线包，是的话解压进内存，不是则下载离线包再解包，webview加载url，加载前查询内存是否存在页面数据，存在则直接返回内存数据到页面上，不存在failback（将离线包所有文件音色和到cdn上，如果本地包是老得，就直接访问对应cdn地址）到线上地址，再加载数据到离线包页面上。
- preRPC机制，当页面需要rpc数据时，并发请求页面和rpc数据，加速网页显示。

## 2018-5-3
1. 浏览chair，埋点文档
2. 新建页面：lengjing.config.js中增加页面配置，执行npm run init生成文件夹，index.js作为主入口，尽量简洁，app.js承载和UI洁面相关的组件。
3. ||前面为false输出后面的值，前面为true输出前面的值。&&前面是false返回前面的值，前面是true返回后面的值

## 2018-5-4
1. 修改编辑保单页：
- 增加字段
- 添加滑动开关：通过在组件中添加bool类型，按type值进行不同的渲染
- 查看图片组件：引入previewImagesByURL,添加onclick属性

## 2018-5-7
1. 页面修改：
- 通过settitile设置弹窗的title值。
- 把变量映射写到commen中，在通过应用变量名改变背景。
- backer还没完成，添加了backer以后弹窗不显示。
2. export规定模块的对外借口，import使用{}引用。import在编译时处理，无法在运行时加载模块
   export default输出默认函数，import引用时任意命名，不用{}，一个模块只能有一个默认处输出

## 2018-5-8
1. 页面修改：
- 弹窗添加返回劫持，backer中只能放一个标签
- 数组过滤，filter
- 通过find查找是否存在滑块元素来判断是否需要添加滑块属性。
2. 继续学习ES6文档

## 2018-5-9
1. 页面修改：添加处理事件,修改reducer，添加effect
2. 通过tnpm run lint检查格式，查看编码规约。当通过变量访问属性时使用中括号[]。

## 2018-5-10
1. TypeScript 设置对变量对类型控制，取值范围
2. 通过global修改antd默认样式
3. checkout master->pull->checkout feat->rebase
4. 修改代码

## 2018-5-11
1. 修复backer劫持不取消问题
2. 学习原型链和继承，ES6扩展，浏览git文档

## 2018-5-14
1. 根据后端修改字段，加大宽度占比，防止字段溢出缩略
2. 学习ES6数组，对象拓展
3. 学习symbol，主要用来确保属性的唯一性
4. proxy，通过get，set来设置对外部访问对对象读写对拦截，过滤，改写
   apply拦截函数调用，call，apply

## 2018-5-16
1. webpack：
- entry表示使用哪一个模块，构建内部依赖
- output表示输出的路径，文件
- loader用于处理文件，将匹配到的文件进行转换成能处理的有效模块
- plugins用于解决loader无法实现的事情
- 流程：entry-options option初始化（options作为返回结果，包含了之后构建阶段所需对重要信息）➡compile 开始编译（compiler.run触发compile，构建compliation对象：负责组织整个大宝过程，包含每个构建环节及输出环节所对应对方法。内部存放着所有module，chunk，生成对asset和用来生成最后大宝文件对template信息）➡make 从入口点分析模块及其依赖点模块，创建这些模块对象（compiler触发，并调用compilation.addEntry方法，通过options对象的entry字段找到入口js文件，然后调用_addMouleChain：根据模块类型获取对应的模块共创并创建模块。构建模块。）➡build-module 构建模块（调用各leader处理模块之间的依赖。调用acorn解析经loader处理后的源文件生成的抽象语法树AST。遍历AST，构建该模块所依赖的模块）➡after-compile 完成构建➡seal 封装构建结果（调用各插件对构建后对结果进行封装，对每个module和chunk进行整理，生成编译后对源码，合并，拆分，生成hash。进行代码优化和功能添加哦）➡emit 把各个chunk输出到结果文件➡after-emit 完成输出

## 2018-5-17
1. chair：
- 中间件：基于koa实现，都是基于洋葱圈模型。编写完以后需要手动挂载
- Router：用于描述请求URL和具体承担执行动作的controller的对应关系。router描述URL和controller地址，当用户执行时，controller里当方法就会执行
- Controller：负责解析用户当输入，处理后返回相应的结果（获取用户通过HTTP传递过来的请求参数➡效验、组装参数➡调用service处理业务，必要时处理转换service的返回结果，适应用户的需求➡通过HTTP将结果响应给用户）
- Query用于获取URL后面的参数，通常为GET类型，只取key第一次出现的值。过长或者敏感数据通过请求中的body部分传递参数，content-type用于表述body格式，内置bodyparser中间件把body解析为object挂载到request.body上。还可以通过header传参，用session存储用户身份信息，加密后放在cookie中。借助validate提供的参数效验机制，完成各种复杂的参数校验，第一个参数设置rule，第二个参数默认ctx.request.body，validator.addrule添加自定义效验规则。
- 调用service（对业务逻辑封装），减少controller层实现的业务逻辑，提高复用性，也可以更好对测试业务逻辑。
- 完成业务逻辑之后，将处理结果通过HTTP响应发送给用户。设置status状态码，每个状态码都有特定含义，让响应更符合语义。返回的数据通过body发送给请求方，配套的content-type表示解析方式。ctx.body是ctx.response.body的简写。
- Service：用于做业务逻辑封装的抽象层，能够保持controller逻辑简介，保持业务逻辑的独立性，复用性，更容易写测试用例。例如通过this.ctx.curl发起网络调用，this.ctx.otherservice调用其他service，this.ctx.db调用数据库。

## 2018-5-18
1. Redux：
- Store：负责接受views传来的action（通过调用dispatch方法，传入action对象作为形参）➡根据action.type和payload对store里对数据进行修改（修改逻辑写在reducer中，store实例创建时，会被传递一个reducer作为形参，这样就可以通过reducer的返回值更新内部数据）➡最后通知views获取最新数据（每次dispatch（action）时，触发subscrib方法注册的回调（内含setstate），从而实现重新渲染）➡通过setState重新渲染组件。
- Reducer：纯函数，用于修改store数据。redux的单一数据源原则，导致数据结构嵌套太深，数据访问变得繁琐，一次采用数据拆解进行访问，通过定义多个reducer对数据进行拆解或者修改（对数据对修改，其实是对object tree对叶子结点value对修改，因此为每一个叶子结点创建一个reducer，并将叶子结点对value直接传给该reducer，这样每一个reducer直接对应store对某一个字段，这样修改就会简单很多），再通过combinereducers将数据拼装回去（将一个个reducer自上而下合并，得到一个rootreducer）。通过shouldcomponentupdate判断是否对组件进行更新，防止性能浪费。为了对对象引用进行比较，引入不可变数据（一个数据被创建了，就不可以被改变），所以reducer修改数据对时候，都是返回一个新的引用.
- Middleware:对数据进行流式处理，针对action的特征，采取不同的操作，传递给下一个中间件，也可以直接dispatch（action）。通过store enhancer，使用applyMiddleware给store实例附加上执行中间件的能力。

## 2018-5-21
1. redux-saga：一个redux中间件，用于集中处理redux副作用问题，实现为generator。将获取数据的业务逻辑转移到saga中，让dispatch的参数为一个纯粹的action，用同步书写的方法处理异步逻辑，让代码更易读。
- call:有阻塞的调用saga或返回promise的函数。
- fork：无阻塞的调用。
- put：作用类似redux的dispatch。
- select：作用类似redux thunk的getstate。
2. 强化了解react生命周期，见4-18日报。

2018-5-22
1. react-redux：
- 封装的react专用库。分为UI组件和容器组件。UI组件：只负责UI呈现，不带有业务逻辑，没有状态，数据又this.props提供，纯粹又参数决定它的值。容器组件：负责管理数据和业务逻辑。UI组件由用户提供，容器组件由react-redux自动生成。
- connect：用于从UI组件生成容器组件，将两个组件连起来。接受两个参数：mapstatetoprops，mapdispatchtoprops。前者负责输入逻辑，将state映射到UI组件的参数props。建立一个从外部state对象到UI组件到props对象到映射关系，会订阅store，每当state更新到时候，就会自动执行，重新机选UI组件参数。后者负责输出逻辑，将用户对UI组件对操作映射成action。建立UI组件的参数到store.dispatch方法到映射，定义了哪些用户到操作应该当作action，传给store。
- provider：让组件拿到state对象。在根组件外包一层，这样所有子组件就默认拿到了state。

## 2018-5-23
1. 学习chair文档，ES6文档

## 2018-5-24
1. interator:为各种不同的数据结构提供统一的访问机制。只要部署了接口，就能完成遍历。可用for...of循环。本质是指针对象，通过next方法指向下一个成员。
2. generator：状态机，封装了多个内部状态。调用以后，生成一个指向内部状态的指针对象，通过next移到下一个状态，next恢复执行，yield暂停操作。next可以带参数作为上一个yield表达式的返回值。yield*用户在一个generator函数中执行另一个generator函数。协程：可以并行执行，交换执行权的线程。
3. thunk函数：传名调用，将参数放到一个临时函数（thunk函数）中，再将临时函数传入函数体。将多参数函数，替换成一个只接受回调函数作为参数的单参数函数。
4. 学习盒子模型

## 2018-5-28---6-1
1. JS运行机制：主线程执行同步任务，异步任务会先挂起，等待IO设备返回结果，IO设备完成一项任务，就在任务队列里添加一个事件，表示相关异步任务可以进入执行栈了。主线程上的同步任务执行完以后，再去读取任务队列，如果里面有异步任务可以执行了，就结束等待，进入主线程开始执行（执行对应的回调函数）。
- Event Loop事件循环：主线程从任务队列里读取事件，是不断循环的。主线程运行时，产生堆栈，栈中代码调用外部api在任务队列里加入例如click，load等事件。当主线程代码执行完毕，回去读任务队列，然后一次执行事件所带的回调函数。
- 定时器：将事件插入任务队列，在规定时间后执行。同样等主线程执行完当前执行栈后执行其回调，如果当前代码执行时间很长，没办法保证会按时执行。
- node事件循环：V8引擎解析JS脚本➡解析后代码调用nodeAPI➡libuv负责API执行，将不同任务分配给不同线程，形成事件循环，异步将执行结果返回给V8引擎➡V引擎将结果返回给用户。
- node setTimeout方法：在当前任务队列尾部添加事件，指定等任务总在下个Event Loop时执行。
参考：http://www.ruanyifeng.com/blog/2014/10/event-loop.html
2. 编写静态回访问卷页：
- PS切图，将所需要的图片从psd图片中导出。
- 运用css制作网页。
- 通过控制台打印检查代码，元素修改样式。    
3. 数据获取，通过rpc获取的数据在mock的时候要用规范接口。从凤蝶获取使用getH5Data获取凤蝶数据，数据模版需要设置，然后具体数据由设计提供。
4. 线下线上环境切换：切换网关aaa➡客户端聚➡返回切换自定义模式➡将地址aaa改为dev01/02/03➡再客户端聚焦➡打开应用助手➡开关关闭JSAPI效验➡tnpm start。（了解mock和线上数据获取方式区别）
5. 回访页面逻辑编写总结：JSX只能使用JS表达式，不能用语句（if/for），灵活使用对象和数组的方法，注意const无变量提升，多使用console.log。

## 2018-6-4
1. 修改回访问卷：代码逻辑要合理，便于维护，不用取巧到方法。不必要的参数不要传递。自定义函数的名字不要和内置的类似。

## 2018-6-14---6-15
1. CSS不要写死高度样式。absolute:绝对定位，相对于static定位外的第一个父元素进行定位。relative：相对定位，相对正常位置进行定位。margin-top代替top，height自适应。

# fed-e-task-03-02
vue-02
一、简答题
1、请简述 Vue 首次渲染的过程。
答：
    1、首先 执行 vue 实例的 _init 函数。
    2、_init 函数给当前实例 注入 父子关系、响应事件、h 函数、执行 钩子函数、设置数据的响应式、注入provide。
    3、挂载 整个页面，如果传入 render 函数的话，获取 render 函数，如果没有的话，就 将 template 或者 el 的outerHTML 编译成 render 函数，同时 生成 当前组件的 渲染 Watcher ，将 render 函数 传入。
    4、渲染 Watcher 被创建的时候，就会开始执行 对应的 get ，也就是 render 函数。
    5、在 render 函数中，会获取当前 data 中的数据，这样就会触发 数据响应式中的 getter 函数，进行依赖收集。
    6、这样在以后的数据更新中，就会执行 对应的 渲染watcher 了 。

2、请简述 Vue 响应式原理。
答：
    1、在 Vue 中模板编译过程中的指令或者数据绑定都会实例化一个 Watcher 实例，实例化过程中会触发 get() 将自身指向 Dep.target;
    2、data在 Observer 时执行 getter 会触发 dep.depend() 进行依赖收集;依赖收集的结果：
        1. data在 Observer 时闭包的dep实例的subs添加观察它的 Watcher 实例；
        2. Watcher 的deps中添加观察对象 Observer 时的闭包dep的指令或者数据绑定都会实例化一个 Watcher 实例，实例化过程中会触发 get() 将自身指向 Dep.target;
    3、data在 Observer 时执行 getter 会触发 dep.depend() 进行依赖收集;依赖收集的结果：
        1. data在 Observer 时闭包的dep实例的subs添加观察它的 Watcher 实例；
        2. Watcher 的deps中添加观察对象 Observer 时的闭包dep；
    4、当data中被 Observer 的某个对象值变化后，触发subs中观察它的watcher执行 update() 方法，最后实际上是调用watcher的回调函数cb，进而更新视图。

3、请简述虚拟 DOM 中 Key 的作用和好处。
答：
    key值的作用是为了给每个组件有唯一的一个识别身份，主要是为了vue精准的追踪到每一个组件，高效的更新虚拟DOM。

4、请简述 Vue 中模板编译的过程。
答：
    1、解析器(parse) - 将 模板字符串 转换成 element ASTs
    2、优化器(optimize) - 对 AST 进行静态节点标记，主要用来做虚拟DOM的渲染优化
    3、代码生成器(generate) - 使用 element ASTs 生成 render 函数代码字符串


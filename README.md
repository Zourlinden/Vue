# Vue
    1、vue初体验，了解vue的基本结构，mvvm原理

## Vue的指令与过滤器
    vue中的指令按照不同的用途可以分为6大类
        1、 内容渲染指令
        2、属性绑定指令
        3、事件绑定指令
        4、双向绑定指令
        5、条件渲染指令
        6、列表渲染指令

## Vue指令
    1、内容渲染指令
        1.v-text 指令的缺点：会覆盖元素内原有的内容
        2.{{ }} 插值表达式：在实际开发中用的最多，只是内容占位符
        3.v-html 指令的作用:可以把带有标签的字符串，渲染成真正的HTML内容！
    2、属性绑定指令
        注意：插值表达式只能用在元素的内容节点中，不能用在元素的属性节点中
        在vue中，可以使用 v-bind：指令，为元素的属性动态绑定值
        简写是英文的:
        在使用 v-bind 属性绑定期间，如果绑定的内容需要进行动态拼接，则字符串的外面应该包裹单引号
    3、事件绑定指令
        v-on进行事件绑定，且在实例里的methods里添加方法
        v-on的简写是@
        vue提供了内置变量，名字叫$event,它就是原生 DOM 的事件对象 e
            <button @click="add(1,$event)"></button>
        vue中提供了事件修饰符，
            prevent表示阻止默认行为
            stop表示阻止事件冒泡
            capture表示以捕获模式触发当前的事件处理函数
            once表示绑定的事件只执行一次
            self表示只在event.target是当前元素自身时触发事件处理函数
                <a href="https://www.baidu.com" @click.prevent="add">
        vue中提供了按键修饰符
            enter指的是enter被按下时执行方法
            esc值得是esc键被按下时执行方法
                <input type="text" @keyup.enter="submit">
    4、双向数据绑定指令
        v-model常用于
            1.input输入框
                type="radio"
                type="checkbox"
                type="xxx"
            2.textarea
            3.select
        v-model指令的修饰符
            .number : 自动将用户的输入值转为数值类型
            .trim : 自动过滤用户输入的首尾空白字符
            .lazy : 在"change"时而非"input"时更新
    5、条件渲染指令
        条件渲染指令有两个：v-if、v-show
        区别：v-if每次都会动态的移除跟创建元素，v-show则通过dispaly来控制
        在实际开发中，绝大多数情况，不用考虑性能问题，直接使用v-if就好了
    6、列表渲染指令
        v-for:xxx="(item,index) in <list>" :key="<list>.id"
        key的注意事项
            1.key 的值只能是字符串或数字类型
            2.key 的值必须具有唯一性
            3.建议把属性项id属性的值作为key的值
            4.使用index的值当作key 的值没有任何意义，因为index的值不具有唯一性
            5.建议使用v-for指令时一定要指定key的值
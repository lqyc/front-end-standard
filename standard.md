
代码规范的目的是为了编写高质量的代码，让团队成员每天心情更加愉悦，工作沟通更加顺畅。


#### 命名规范
- 命名严谨性
> 代码中的命名严禁使用拼音与英文混合的方式，更不允许直接使用中文的方式。
>  说明：正确的英文拼写和语法可以让阅读者易于理解，避免歧义。注意，即使纯拼音命名方式也要避免采用
> 例如：banner-box
- 项目命名

`页面文件命名（横杆命名）`
 > 例如：tip-detail


`组件命名（驼峰命名）`
> 例如： popBox

`CSS命名`
> 类名使用（横杆+小写命名）例如: .banner-wrap / .banner

> id 采用驼峰式命名, 例如：#bannerBox

> scss 中的变量、函数、混合、placeholder 采用驼峰式命名

`css、HTML、PNG 文件命名`
`全部采用小写方式， 以中划线分隔`
> 例如： signup.css /  index.html /  company-logo.png

#### HTML、CSS规范 
- 代码缩进
> 缩进使用 2 个空格（一个 tab），嵌套的节点应该缩进。

- 分块注释
> 在块状元素，列表元素和表单元素后，必要的注释，加上一对 HTML 注释。注释格式如下：
```
  <!-- header 头部 特殊注释 -->
  <header>
    <div class="container">
        <!-- 这里是图片标签的特殊注释 -->
        <img src="images/header.jpg" />
    </div>
  </header>
```
- 代码块内容分类
>  vue文件里面template、script、css 三大模块要有空格行间隙区分开

- css避免嵌套层级过多
> 将嵌套深度限制在 3 级。对于超过 4 级的嵌套，给予重新评估。这可以避免出现过于详实的 CSS 选择器。
> 避免大量的嵌套规则。当可读性受到影响时，将之打断。推荐避免出现多于 20 行的嵌套规则出现
```
// 不推荐
.main{
  .title{
    .name{
       color:#fff
    }
  }
}
// 推荐
.main-title{
   .name{
      color:#fff
   }
}
```

#### 组件规范
- 命名规范
`父组件紧密耦合的子组件应该以父组件名作为前缀命名`
```
components/
|- TodoList.vue
|- TodoItem.vue
```
- Prop 定义应该尽量详细
> 必须使用 camelCase 驼峰命名
> 必须指定类型
> 必须加上注释，表明其含义
> 必须加上 required 或者 default，两者二选其一
> 如果有业务需要，必须加上 validator 验证
```
 props: {
    emptyDesc: {
      type: String,
      default: '暂无事件', // 图片描述文案
    },
    isFinished: {
      type: Boolean,
      default: false,  // 是否加载结束
    },
  },
```

-  为组件样式设置作用域
```
<!-- 使用 `scoped` 特性 -->
<style scoped>
  .btn-close {
    background-color: red;
  }
</style>
```
- 如果特性元素较多，应该主动换行
```
<MyComponent foo="a" bar="b" baz="c"
    foo="a" bar="b" baz="c"
    foo="a" bar="b" baz="c"
/>
```

#### TS规范

- 请尽量少用any定义类型
- 数组类型

`使用 Array泛型`
```
const arr1: Array<number> = [1, 2, 3] 
```
`使用 数据类型 + [] 形式`
```
const arr2: number[] = [1, 2, 3] 
```
- 函数类型

`形参列表都为必传参数时，传入的实参类型和数量，都必须与形参保持一致；可选参数，必须放在参数列表的最后面`
```
/**  
 * 如果某个参数可传可不传：
 *    1、可在形参的参数名后面添加 "?" , 使其变成可选的；
 *    2、使用 es6中添加参数默认值的方法, 使其变成可有可无的。
 * 
 * 若需要接收任意个数的参数，使用 es6 中的rest操作符
 * 
 */

function func1 (a: number, b?: number, c: number = 10, ...rest: number[]): string {
    return 'func1'
}

func1(100, 200)

```
`对于回调函数的形参类型，需要进行约束`
```
const fun2: (a: number, b: number) => string = function (a: number, b: number): string {
    return 'func2'
}
```
- 泛型

`泛型就是在声明函数时不去指定具体的类型，等到在调用的时候再去传递具体的类型。`
```
function createNumberArray (length: number, value: number): number[] {
    // Array 默认创建的是 any类型的数组，因此需要使用泛型进行指定，传递一个类型
    return Array<number>(length).fill(value)
}

function createStringArray (length: number, value: string): string[] {
    return Array<string>(length).fill(value)
}

// 不明确的类型，使用 T 替换，调用时传入
function createArray<T> (length: number, value: T): T[] {
    return Array<T>(length).fill(value)
}
```
####  Vue Router 规范
- 页面跳转数据传递使用路由参数
> 页面跳转，例如 A 页面跳转到 B 页面，需要将 A 页面的数据传递到 B 页面，推荐使用 路由参数进行传参，而不是将需要传递的数据保存 vuex，然后在 B 页面取出 vuex 的数据，因为如果在 B 页面刷新会导致 vuex 数据丢失，导致 B 页面无法正常显示数据。
```
<!--推荐-->
let id = ' 123';
this.$router.push({ name: 'userCenter', query: { id: id } });
```
- 使用路由懒加载（延迟加载）机制
```
{
    path: '/uploadAttachment',
    name: 'uploadAttachment',
    meta: {
      title: '上传附件'
    },
    component: () => import('@/view/components/uploadAttachment/index.vue')
}
```
- router 中的命名规范
> name 命名规范采用 KebabCase 命名规范且和 component 组件名保持一致！（因为要保持 keep-alive 特性，keep-alive 按照 component 的 name 进行缓存，所以两者必须高度保持一致）
```
[
  {
    path: "/product-list",
    name: "productList",
    component: productList,
    meta: { title: "产品列表", keepAlive: true },
  },
  {
    path: "/product-list/detail",
    name: "productDetail",
    component: productDetail,
    meta: { title: "基金详情", keepAlive: false },
  },
];
```


####  提交commit信息规范
`提交消息尽可能简明扼要，并且有标识如下:
（如果更新和新增都有，就标识U)`

```
A ***    // 添加
M ***    // 合并冲突
U ***    // 更新
D ***    // 删除
F ***    // 修复
```

#### TIPS
- 尽量不要手动操作 DOM
因使用 vue 框架，所以在项目开发中尽量使用 vue 的数据驱动更新 DOM，尽量（不到万不得已）不要手动操作 DOM，包括：增删改 dom 元素、以及更改样式、添加事件等。

- 删除无用代码
因使用了 git/svn 等代码版本工具，对于无用代码必须及时删除，例如：一些调试的 console 语句、无用的弃用功能代码。

- 跳转H5页面凡是要新开一个新页面的路径都要拼上一个时间戳, 如下：path/xxx/index.html?_t=timestamp (内部H5不用)


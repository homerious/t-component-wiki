# t-component dev-kit 介绍文档


本套脚手架是基于vue并内含一套定制的UI组件和页面demo的开发脚手架。

@toc

## 基本使用

使用步骤：
1、安装依赖。

```JavaScript
npm install
```

2、运行开发模式。

```JavaScript
npm run dev
```

3、打开接口和上传模拟服务器。

```JavaScript
npm run mock
```

4、进行生产环境打包。

```JavaScript
npm run build
```

## 组件使用方法介绍

组件合集中包含了20个单文件组件，4个函数式组件。常用的单文件组件包括 button、input、radio、model、select、checkbox和tooltip，已经在Vue中全局注册，直接在页面中使用即可；函数式组件已经安装在全局Vue中，直接调用即可；其他组件则可以按需引入到页面中使用。

> 示例1  myApp.vue

```HTML
<template>
  <div>
    <t-button @click="showLoading">这是一个按钮。</t-button>
    <!--内置组件，可以直接调用-->
    <Datepicker placeholder="请输入出生日期" v-model="birthday"/>
  </div>
</template>
<script>
import { Datepicker } from 't-component';
// 按需引用组件到页面中去，直接从't-component'引用即可
export default{
  name: 'myApp',
  data(){
    return { birthday: '' };
  },
  components: { Datepicker }， // 外部引用的组件需要注册
  methods: {
    showLoading() {
      this.$loading.open('数据加载中')；
      // 函数式组件可以直接调用
    },
}
</script>
```

## 组件API及使用介绍

### 1. backtop / 回到顶部

引用

```JavaScript
import { Backtop } from 't-component';
```

属性

| 属性名      | 说明    |  类型 |默认值|可选值|
| --------- | -------- | -----: | --: |--: |
|showHeight|设定页面滚动多少高度之后在显示backtop按钮|`Number`|`300`|
|position|设定backtop按钮显示的位置|`Object`|`{ bottom: '40px', right: '40px' }`|
|duration|设定点击backtop按钮之后多久回到页面顶部|`Number`|`500`|

### 2. badge / 标记

引用

```JavaScript
import { Badge } from 't-component';
```

属性

| 属性名      | 说明    |  类型 |默认值|可选值|
| --------- | -------- | -----: | --: |--: |
|type|设置标记显示的类型（带文字/不带文字）|`String`|`dot`|`dot text`
|isShow|设置是否显示标记|`Boolean`|`true`|`true false`|
|color|设置标记的颜色,支持Hex和RGB写法|`String`|`#f24a4a`|    |
|textColor|设置文字颜色，写法同上| `String` |  `#fff`   |    |
|content|设置标记的文字内容|   `String`     |     |    |

插槽

| 插槽名      | 说明    |
| --------- | -------- |
|-|    设置标记的文字内容      |

### 3. button / 按钮

引用

```HTML
<t-button>按钮1</t-button><!--已在vue中注册可以直接使用-->
```

属性

| 属性名      | 说明    |  类型 |默认值|可选值|
| --------- | -------- | -----: | --: |--: |
| size | 设置按钮的大小 | `String` | `'normal'` | `'large'`, `'normal'`, `'small'`|
| type | 设置按钮的颜色类型 | `String` | `'default'` | `'default'` `'primary'` `'success'` `'warning’` `'danger'` `'info'` `'text'` |
| disable| 设置是否禁用按钮 | `Boolean` | `false` | `true false` |
| shape | 设置按钮的形状 | `String` | `default` | `'default'` `'circle'`  `'ellipse'`|
| icon  | 按钮图标类名  | `String`    |     |   见《icon详细目录》  |

==备注==： size和type这两个属性使用的是预设的值，如果有特殊需要可以另外设置样式，例如直接在其标签添加行内样式`style="width:100%; color: red;"`也是可以的，后面有类似的属性默认也是这样的。

### 4. cascader / 级联选择

引用

```JavaScript
import { Cascader } from 't-component';
```

属性

| 属性名      | 说明    |  类型 |默认值|可选值|
| --------- | -------- | -----: | --: |--: |
|options| 设置供选择的数据项  |`Array`|     |     |
| value  |绑定`v-model`的值|  `Array`   |     |     |
|placeholder| 设置输入框占位文本  |  `String`   |     |     |
|mutiple | 设置是否可以选做个选项  |`Boolean`|`true`| `true` `false` |
| disable  |设置是否禁用级联选择|`Boolean`|`false`|`true false`|
|loadData|设置动态加载选项|`Function`     |     |
|displayMethod|设置显示的格式|`Funtion/String`|  `label`   |     |
| popupPlacement  | 设置浮层位置  |`String`     |  `'bottomLeft'`   |  `'bottomLeft'` `'bottomRight'` `'topLeft'` `'topRight'`   |
|anyState| 是否允许选择任意一级的选项  |  `boolean`   |  `false`   |  `true false`   |
|notFoundText||列表无结果显示的时候显示的提示|  `String`  |     |     |
|resultFilter| 选择之后进行筛选的显示函数|`Function`   |     |     |

==备注==:displayMethod属性为输入字符串的时候渲染对应字符串的数据字段，方法则用于某些复杂显示的数据字段的业务场景。

  事件

| 事件名称 | 说明 | 返回值 |
| --- | --- |---|
|change| 选择值变化后触发的事件 | 返回value值 |
|choose|当某一级菜单被点击后触发的事件|各父级选项组成的数组 |

### 5. checkbox / 多选框

引用

```HTML
<t-checkbox value="1" v-model="check"></t-checkbox ><!--已在vue中注册可以直接使用-->
```

属性

| 属性名      | 说明    |  类型 |默认值|可选值|
| --------- | -------- | -----: | --: |--: |
| value  |设置多选框代表的值,如果是字符串或者数字会在没有包裹内容的时候自动显示出来|  `All`   |     |     |
|checked| 多选框是否被选，使用`v-model`的时候不用绑定这个 |   `Boolean Array`  |     |     |
| disable  |是否禁用多选框|`Boolean`|`false`|`true` `false`|
|      showLabel     |  设置是否自动显示value作为多选框的标签值     |   `Boolean`     |  根据`value`值的类型而定，如果为数字和字符串的话，则自动显示   | `true false`   |
|     displayMethod      |  当绑定的value为对象时，自定义设置显示的方法，参数为value的值        |  `Function`      |     |    |
|objKeyValue|    当value值为对象且处于多选的时候，用于检查唯一性的属性名     |    `String`     |  `'value'`   |    |
| halfCheck  | 在作为checkgroup的全选按钮的时候，用于设置是否显示非全选的图标    |  `Boolean`      |  `false`    |   `true false`   |

==备注==：

1. checked属性/v-mode可以绑定布尔值或者数组（和vue实现的原生checkbox的绑定一样），绑定布尔值就对应着多选框是否被选择（true: 被选/ false: 没选）；绑定数组则对应多选框的值是否存在于选择集合里面。
2. displayMethod属性适用于当value绑定的值为对象的时候的定制化显示的选项内容的业务场景，当然也可以使用插槽来实现相同效果。

  事件

| 事件名称 | 说明 | 返回值 |
| --- | --- |---|
|change| 多选框值变化触发的事件 | 是否被选中 => `true` /`false`，`true`的话还会返回对应`value`值,`false`的时候会返回`null`|

插槽

| 插槽名      | 说明    |
| --------- | -------- |
|-|    设置多选框的选项显示内容      |

### 6. CheckboxGroup / 多选框组

引用

```JavaScript
import { CheckboxGroup } from 't-component';
```

属性

| 属性名      | 说明    |  类型 |默认值|可选值|
| --------- | -------- | -----: | --: |--: |
|value | 多选框在组件里绑定`v-model`的值 |     |     |     |
| disable  |是否禁用多选框组|`Boolean`|`false`|`true false`|
|max|多选框组最多可选的选项数量|`Number`|     |     |
|min| 多选框组最少可选的选项数量  |  `Number`   |     |     |

==备注==： checkboxGroup返回为数组

事件

| 事件名称 | 说明 | 返回值 |
| --- | --- |---|
|change| 多选框组值变化触发的事件 | 返回变化之后的数组值 |

### 7. datepicker / 日期选择器

引用

```JavaScript
import { Datepicker } from 't-component';
```

属性

| 属性名      | 说明    |  类型 |默认值|可选值|
| --------- | -------- | -----: | --: |--: |
| value | 设置绑定时间的值，绑定`v-model`的时候不需要绑定此属性  |  `String|Date Object` |     |     |
|type| 设置选择器的功能,可以选择日期、月份、年份和日期范围|`String`   |  `date`   | `date month year week dateRange`    |
| format  |显示格式|`String`|  `yyyy-mm-dd`   |     |
|disabledDate|设置不可选择的日期|    `Function`    |     |    |

==备注==：disableDate属性方法会返回一个Date对象作为参数，disableDate方法则需要返回一个布尔值以表示传入的日期是否在不可选择的日期范围内。
示例：(单纯的函数示例)

```JavaScript
function disabledDate(date) {
  return date < new Date('2018-10-3') || date > new Date('2019-1-3'); }
```

### 8. input / 输入框

引用

```HTML
<t-input v-model="check"></t-input><!--已在vue中注册可以直接使用-->
```

属性

| 属性名      | 说明    |  类型 |默认值|可选值|
| --------- | -------- | -----: | --: |--: |
| value  |设置输入框的值，当使用v-model绑定的时候，不需要绑定这个属性|  `String` `Number`   |     |     |
|type|设置输入框的类型|`String`|`text`|`text` `password` `number` `textarea`|
| size | 设置输入框的大小 | `String` | `'normal'` | `'large'`, `'normal'`, `'small'`|
| readonly  |设置原生的readonly属性|`Boolean`|`false`|`true` `false`|
|disable|设置输入框是否可用|`Boolean`|`false`|`true` `false`|
|validate|设置验证输入框内容使用的函数或正则表达式|`Function/RegExp`|     |     |
|errorMessage| 验证出现报错信息的设置|`Object/String`| ||
| placeholder|设置占位文本|`String`|     |     |
|clearable| 设置是否显示清除按钮  |`Boolean`|`false`|`true` `false`|
|autofocus|设置自动获取焦点|`Boolean`|`false`|`true` `false`|
| rows  |仅在`type="textarea"`时生效，输入框的行数| `Number`|||
|cols| 仅在`type="textarea"`时生效，输入框的列数  | `Number`|||
|max|仅在`type="number"`时生效，输入数字的最大值|`Number`|  ||
|min|仅在`type="number"`时生效，输入数字的最小值|`Number`|  ||
|maxLength|原生属性，输入字符串的最大长度|`Number`  |    |     |
|minLength| 原生属性，输入字符串的最大长度|`Number` |  |     |

==备注==：errorMessage为字符串的时候，默认为错误显示的文字内容，而为对象的时候的结构应为：

```JavaScript
{
  errorText: '', // 错误显示的文字内容
  errorColor： '', // 错误显示的文字的颜色
}
```

事件

| 事件名称 | 说明 | 返回值 |
| --- | --- |---|
|change| 输入框值变化触发的事件 | 返回value值 |
|keyup|  输入框按键完毕触发的事件  | 返回输入的值 |
|focus|选择框获得焦点的时候触发|   |
|blur|选择框失去焦点的时候触发|   |

插槽

| 插槽名| 说明 |
|---|---|
|leftIcon| 出现输入框内部左边的icon  |
|rightIcon|出现在输入框内部右边的icon|
|leftLabel|出现在输入框外部左边的附加内容|
|rightLabel|出现输入框外边右边的附加内容|

### 9. loading / 加载中

引用

```JavaScript
this.$loading.open('加载中'); // 已集成到vue中，可以直接调用其方法
this.$loading.open('获取数据中', 'stripper');
this.$loading.open('努力加载中', 'ballRing', 3);
this.$loading.config({
  title: '加载中...',
  icon: 'walkingSquare',
  duration: 5,
  backdrop: true,
  backdropColor: '#f2f2f2',
}).open();
this.$loading.close();
```

方法及参数

`this.$loading.open([title, icon, duration])`

|参数名|说明|类型|可选值
|---|---|---|---|
|title|可选，设置加载提示的文字内容 | `String`  |
|icon|可选，设置加载的动画类型   | `String`  | `'win8' 'ballqueue' 'circle3' 'walkSquare' 'ballring' 'stripper'`
| duration  | 可选，设置多少秒之后自动消失  | `Number`  |   |

`this.$loading.config(config)`

|参数名|说明|类型|可选值
|---|---|---|---|
|config|必填，用于设置加载提示详细配置的对象|`Object`|   |

config的应有的几个属性名：

```JavaScript
const config = {
  title: '', // String，加载提示的文字
  icon: '', // String，加载提示的动画图标类型
  duration: 3, // Number，(单位：s)加载提示的加载时间，即多少秒之后自动消失
  backdrop: false, // Boolean, 是否显示背后遮罩层
  backdropColor: '#fff', // String, 遮罩层的颜色
  customTpl: '<span>自定义HTML模板</span>', // String, 自定义的HTML模板
}
```

==备注==：

1. config()方法需要继续调用open()才能够是加载提示显示出来；
2. duration属性选项如果不配置的话，加载提示不会自动消失，必须调用close()，加载提示才能消失;
3. backdrop即使设置为不显示也点击不了其他内容，目的是为了防止用户误触；
4. 如果设置了customTpl属性选项，则title和icon选项则不会生效。

`this.$loading.close()`

手动关闭加载提示。

### 10. menu / 菜单

引用

> mymenu.vue;

```HTML
<template>
<Menu direction="vertical">
  <MenuItem menuName="菜单0" link="/"></MenuItem><!--MenuItem只能嵌套在Menu或者SubMenu中使用-->
  <SubMenu menuName="菜单1"><!--SubMenu中可以嵌套自身和MenuItem-->
    <MenuItem menuName="副菜单1"link="/1"></MenuItem>
    <MenuItem menuName="副菜单2" link="/2"></MenuItem>
  </SubMenu>
</Menu>
</template>
<script>
import { Menu, MenuItem, SubMenu } from 't-component';
export default{
  name: 'my-menu';
  components: { Menu, MenuItem, SubMenu },
}
</script>
```

==备注==：一个菜单需要菜单组件Menu、副菜单SubMenu和菜单项MenuItem来组合而成，其中Menu和MnuItem是必要的组成部分，而SubMenu则是在有子菜单的情况下选用。菜单的层级没有限制，但是从用户体验上出发，最多不超过三层，太复杂对于导航不友好。

Menu组件属性

| 属性名      | 说明    |  类型 |默认值|可选值|
| --------- | -------- | -----: | --: |--: |
|direction | 设置菜单的显示方向  |  `String`   | `'horizontal'`    | `'horizontal' 'vertical'`    |
| routerHandler|  自定义路由的跳转方法 |  `Boolean`   |  `false`   | `true false`    |
|canCollapse|  设置菜单是否可以展开/收缩，仅在`'vertical'`模式下有效|`Boolean` |`false` | `true false`    |
|collapse |  设置菜单在第一次渲染为展开(true)/收缩(false)状态 ，仅在canCollapse为`true`有效   | `Boolean` |`false` | `true false`    |
|textColor|    默认的文字颜色      |   `String`     |   `'#333'`  |    |
|bgColor|    默认的背景颜色      |    `String`    |  `'#fff'`   |    |
|activeTextColor|   选中的项的文字颜色       |   `String`     |  `'#4385ff'`   |    |
|activeBgColor|    选中的项的背景颜色      |    `String`    |  `'#d5e5ff'`   |    |

==备注==：在MenuItem中设置了link属性的的时候才会激发路由跳转的功能，才能使Menu中的routerHandler属性发挥作用，routerHandler接受参数是被点击的MenuItem的link属性的路由路径信息。

SubMenu组件属性

| 属性名      | 说明    |  类型 |默认值|可选值|
| --------- | -------- | -----: | --: |--: |
|icon| 设置子菜单要显示的图标  | `String`    |     |  iconfont内的图标类名   |
|disable| 设置子菜单是否可用  |   `Boolean`   |  `false`   | `true false`    |
| menuName| 设置子菜单要显示的标题  | `String`    |     |     |

==备注==：SubMenu组件没有link属性，因为它不担任跳转功能，它只负责展示/隐藏子菜单。

SubMenu组件插槽

| 名称 | 说明 |
|---|---|
|icon| 自定义子菜单的图标  |

MenuItem组件属性

| 属性名      | 说明    |  类型 |默认值|可选值|
| --------- | -------- | -----: | --: |--: |
|link|  设置菜单项要跳转的路由地址或对象 |  `String|Object`   |     |     |
|disable| 设置菜单项是否可用  |  `Boolean`   |  `false`   | `true false`    |
|icon|  设置菜单项要显示的图标 |  `String`   |     | iconfont内的图标类名    |
|menuName| 设置子菜单要显示的标题  |  `String`   |     |     |

MenuItem组件插槽

| 名称 | 说明 |
|---|---|
|icon| 自定义菜单项的图标  |

### 11. messagebox / 对话框

引用

```JavaScript
this.$messagebox.alert('', '不能关闭此页面') // 已集成到vue中，可以直接调用其方法
this.$messagebox.confirm('警告'，'确定要删除此页面吗？', 'icon-warn-fill').then((result) => {
    console.log(result);
    // do something else
  })
  .catch((result) => {
    // do something else
  })
this.$messagebox.prompt('提示'，'请输入你的年龄').then((result) => {
    console.log(result);
    // do something else
  })
  .catch((result) => {
    // do something else
  })
this.$messagebox({
  title: '这是小标题',
  buttonText: ['对的', '错的'],
  type: 'prompt',
  inputValidate: /[0-9]/,
  errorMessage: '请输入数字'
}, (result) => {
  console.log(result);
})
```

方法及参数

`this.$messagebox.alert([title, text, icon, buttonText])`
`this.$messagebox.confirm([title, text, icon, buttonText])`
`this.$messagebox.prompt([title, text, icon, buttonText])`

|参数名|说明|类型|可选值
|---|---|---|---|
|title|可选，设置对话框的标题内容，不设置则为空 | `String`  |
|text|可选，设置对话框的文字内容，不设置则为空| `String`  |   |
|icon|可选，设置对话框的标题图标类型   | `String`  | iconfont里类名
| buttonText| 可选，设置对话框的按钮文字内容，最多两个，默认为`['确定', '取消']`  | `Array`  |   |

==备注==：这几个函数均为异步的Promise函数，可以根据用户的选择做出相应的动作。

`this.$messagebox(config, callback)`

|参数名|说明|类型|可选值
|---|---|---|---|
|config|必填，用于设置对话框详细配置的对象|`Object`|   |
|callback|可选，用户点击按钮的执行的回调方法|`Function` |   |

config应有的几个属性名：

```JavaScript
const config = {
  title: '', // String, 设置对话框的标题内容
  text: '', // String, 设置对话框的文字内容
  icon: '', // String, 设置对话框的标题图标类型
  iconColor: '', // String, 设置对话框的标题图标颜色
  inputValidate: null, // Function|RegExp, 用于验证prompt的用户输入内容，仅在type为prompt时生效
  customTpl: '', // String， 设置自定义的HTML模板，此属性会覆盖其他关于外观的设置
  type: '', // String，设置对话框的类型，可选值有'alert', 'confirm'和'prompt'
  theme: '', // String，设置对话框的图标主题(即类型和颜色),可选值  
  // 有'info','warnning','error'和'success'
  buttonText: ['确定', '取消'], // 设置对话框的按钮文字
  buttonClass: ['t-msgbox-confirmBtn', 't-msgbox-cancelBtn'], // 设置对话框的按钮的样式
  canClose: true, // 是否显示关闭按钮
  onClose: null, // 关闭之后的回调函数
  backdrop: true, // 是否显示遮罩层
  backdropColor: '#767676', // 设置遮罩层的颜色
}
```

==备注==：在填入callback参数之后，就不会在返回promise对象了。

### 12. modal / 模态框

引用

```JavaScript
import { Modal } from 't-component';
```

属性

| 属性名  |  说明  | 类型 | 默认值 | 可选值
|---|---| --- | --- | --- |
| canClose| 设置模态框是否显示关闭按钮 | `Boolean`   |  `true`   | `true false`    |
|value|模态框是否显示，当绑定v-model时不用使用绑定此属性| `Boolean`   | |   |
|onClose|用户点击关闭按钮的回调事件| `Function`    |     |     |
|backdrop| 设置是否显示遮罩层  | `Boolean`   |  `true`   | `true false`    |
|backdropColor| 设置遮罩层颜色  |   `String`  |  `'#767676'`   |     |

插槽

| 名称 | 说明 |
|---|---|
|header|设置模态框的头部内容|
|body|设置模态框的主体内容|
|footer|设置模态框的底部内容|

### 13.Notify / 通知

引用

```JavaScript
this.$notify.info('这是一条提示', '没有具体的内容', 3);
this.$notify.error('这是一条警告', '', 3);
this.$notify.success('这是一条提示', '', 3).onclick(() => {
  // do something while click
);
this.$notify.warning({
  title： '你好',
  text: '请先登录！'
  position： 'bottomLeft',
  duration: 3
});
this.$notify.config({
  customTpl: '<span>自定义的通知提示</span>'
  onClick() {
    // do something while click
  },
  onClose() {
    // do something while close
  },
}).open();

```

方法及参数

`this.$notify.info([title, text, duration])`
`this.$notify.error([title, text, duration])`
`this.$notify.success([title, text, duration])`
`this.$notify.warning([title, text, duration])`

|参数名|说明|类型|可选值
|---|---|---|---|
|title|通知提示的标题| `String`  |   |
|text|通知提示的文字内容| `String`  |   |
| duration  | 通知提示的显示持续时间  | `Number`  |   |

`this.$notify.config(config).open()`

|参数名|说明|类型|可选值
|---|---|---|---|
|config|必填，用于设置通知提示详细配置的对象|`Object`|   |

config应有的几个属性名：

```JavaScript
const config = {
  title: '', // String, 设置通知提示的标题内容
  text: '', // String, 设置通知提示的文字内容
  icon: '', // String, 设置通知提示的标题图标类型
  customTpl: '', // String， 设置自定义的HTML模板，此属性会覆盖其他关于外观的设置
  theme: '', // String，设置通知提示的图标主题(即类型和颜色),可选值  
  // 有'info','warnning','error'和'success'
  onClose: null, // 关闭之后的回调函数
  onClick: null, // 关闭之后的回调函数
  backdrop: true, // 是否显示遮罩层
  backdropColor: '#767676', // 设置遮罩层的颜色
}
```

`this.$notify.onclick(callback);`
`this.$notify.onclose(callback);`

|参数名|说明|类型|可选值
|---|---|---|---|
|callback|必填，用于设置相关动作的回调函数|`Object`|   |

==备注==：
此处链式调用的搭配有某些局限性。
info/warning/error/success等函数不建议和config以及open连用：

1. 和config连用会把原本设置覆盖掉 ；
2. 和open连用会没有反应 ；

onclick和onclose这两个函数则不存在这个局限。
不过如果链在config函数后面会有可能吧config里的对应属性给覆盖掉，使用的时候应注意。

### 14. pagination / 分页导航

引用

```JavaScript
import { Pagination } from 't-component';
```

属性

| 属性名  |  说明  | 类型 | 默认值 | 可选值
|---|---| --- | --- | --- |
|total| 一共的总条数  |  `Number`   |   `0`  |     |
| showPagesize  |  是否显示可更改每页条数的选项 | `Boolean`   |  `false`   | `true false`    |
|showTotal| 是否显示总条数  |  `Boolean`   |  `false`   | `true false`    |
|showElevator|  是否显示直达跳转的选项 |  `Boolean`   |  `false`   | `true false`    |
|currentPage|当前所在的页数|  `Number`   |   `1`  |     |
|pageSize| 设置每页显示的条目数  |   `Number`   |  `10`   |     |

==备注==：currentPage为双向绑定值，需要用到 `.sync`后缀

 事件

| 事件名称 | 说明 | 返回值 |
| --- | --- |---|
|sizeChange| pageSize改变时触发的事件  |  改变之后的条目数   
|  pageChange | pageNo改变时触发的事件  |  改变之后的当前页数  

### 15. progress / 进度条

引用

```JavaScript
import { Progress } from 't-component';
```

属性

| 属性名  |  说明  | 类型 | 默认值 | 可选值
|---|---| --- | --- | --- |
|percent| 绑定进度条的百分比   | `Number`    |  `0`  |`0-100`
|  type | 设置进度条类型  |   `String`  |  `line`   |   `'line' 'circle'`  |
|  color|设置进度条颜色|`String/Object`|     |     |
| status | 设置进度条的状态  |     |   `'uploading'`  |   `'success'` `'exception'` `'active'`  |
| strokeWidth | 进度条的宽度  |   `Number`  |  `10`   |     |
| showInfo  | 是否显示进度数值或状态图标  |   `Boolean`  |`true`|  `true false`   |

==备注==: color输入字段为字符串的时候会进度条的颜色左右状态的颜色都改成对应颜色，而输入字段为对象，且为类似于`{success：'color1',exception: 'color2', active: 'color3'}`则可以分别定制三种状态的颜色。


### 16. radio / 单选框

引用

```HTML
<t-radio value="1" v-model="check"></t-radio><!--已在vue中注册可以直接使用-->
```

属性

| 属性名  |  说明  | 类型 | 默认值 | 可选值
|---|---| --- | --- | --- |
| value  |单选框代表的值,如果是字符串或者数字会在没有包裹内容的时候自动显示出来|  `Boolean|Number|String`   |     |     |
|checked| 单选框是否被选择，若在组件里绑定`v-model`的值，不需要再绑定   |     |     |     |
| disable  |是否禁用单选框|`Boolean`|`false`|`true` `false`|

==备注==： radio不需要原生name值来确保多个radio在同一组内。多个radio的v-model绑定同一个值即可以达到这个效果。

 事件

| 事件名称 | 说明 | 返回值 |
| --- | --- |---|
|change| 单选框值变化触发的事件 | 是否被选中 => `true` /`false`，`true`的话还会返回对应`value`值,`false`的时候会返回`null`|

### 17. select / 选择框

引用

```HTML
<t-select  value="1" v-model="check"></t-select><!--已在vue中注册可以直接使用-->
```

属性

| 属性名  |  说明  | 类型 | 默认值 | 可选值
|---|---| --- | --- | --- |
|mutiple | 是否可以多选  |`Boolean`|`true`| `true` `false` |
|disable|是否禁用|`Boolean`| `false`   | `true` `false`    |
| canInput|是否可以输入|`Boolean`|`false`|`true` `false`|
|value|选中的项，若已绑定v-model，则不需要绑定此属性|  `Array` |   |     |
| filterMethod  |用于筛选搜索选项的自定义函数| `Function` |`(item,str) => {return item.indexOf(str) > -1 }`|     |
|placeholder|输入框默认显示的文本| `String` |     |     |
|options|所要渲染的选项组,默认渲染字段为`label`| `Array`   |     |     |
|displayMethod|所要显示的字段或者显示的方法|`String|Funcion`|     |     |

==备注==： canInput属性应用于某些需要搜索选项或者提供搜索结果的业务场景中。

#### 事件

| 事件名称 | 说明 | 返回值 |
| --- | --- |---|
|change| 选择框值变化触发的事件 | 返回变化之后的数组值 |
|keyup|  在启用了`canInput`且用户打字的时候触发，适合用于调用某些搜索类型函数  | 返回输入的值 |
|focus|选择框获得焦点的时候触发|   |
|blur|选择框失去焦点的时候触发|   |

### 18. step / 步骤条

引用

> mystep.vue;

```HTML
<template>
<div>
  <steps :active="stepCount" :status="activeStatus2" direction="vertical">
    <step>
     <span slot="title">第一步</span>
     <p slot="description" style="text-align:left;">首先要打开冰箱门8888</p>
    </step>
    <step :showNumber="false">
     <p slot="title" >第二步</p>
    </step>
    <step :showNumber="false">
      <p slot="title" >第三步</p>
    </step>
    <step :showNumber="false">
      <p slot="title" >第四步</p>
    </step>
  </steps>
 </div>
</template>
<script>
import { Steps, Step } from 't-component';
export default{
  name: 'my-step';
  data(){
    return {
      stepCount: 0,
      activeStatus2: 'processing',
    },
  },
  components: { Steps, Step },
}
</script>
```

==备注==：steps组件和step组件必须搭配一起才能正常使用，另外steps组件最好外面包裹一层容器来调整宽度，因为steps组件会自动撑满父容器然后让step组件计算每一项的宽度。

Steps组件属性

| 属性名  |  说明  | 类型 | 默认值 | 可选值
|---|---| --- | --- | --- |
| direction |  设置进度条显示的方向 | `String`   | `'horizontal'`    |  `'horizontal' 'vertical'`   |
| active  |当前激活的步骤,从0开始算起|  `Number`   |     |     |
| status  |当前的状态|`String`|`'processing'`| `'processing' 'success' 'error'`    |
|useNumber|  设置是否用数字代替进度图标 |     |     |     |
|  iconProcess | 处理中进度的图标  |  `String`   |  `'icon-hourglass'`   |   iconfont的图标类名  |
|iconWait| 等待中的进度图标  |  `String`   |  `'icon-more'`   |  iconfont的图标类名   |
|iconSuccess| 成功的进度图标  |  `String`   |  `'icon-cc-check-circle'`   |  iconfont的图标类名   |
|iconFail| 失败的进度图标  |   `String`  |  `'icon-error-line'`   |  iconfont的图标类名   |
|iconColor| 设置进度条图标的颜色 |   `Array`   |  `['#4385ff', '#969696', '#4acd1f', '#f24a4a']`   |     |

Step组件属性

| 属性名  |  说明  | 类型 | 默认值 | 可选值
|---|---| --- | --- | --- |
|title | 进度步骤显示的文字标题内容  |  `String`   |     |     |
| description| 进度步骤显示的描述性内容  |  `String`   |     |     |
| icon| 进度步骤显示的图标或者图片  |`String`|     |     |

 插槽

| 名称 | 说明 |
|---|---|
|title| 进度步骤的标题内容|
|description | 进度步骤描的述文字内容  |

### 19. switch / 开关

引用

```JavaScript
import { Switch } from 't-component';
```

属性

| 属性名  |  说明  | 类型 | 默认值 | 可选值
|---|---| --- | --- | --- |
|value|设置开关绑定的值，当绑定v-model是不用绑定这个属性值|`Boolean|Number|String`|  `false`  |     |
|disable|设置是否禁用按钮|`Boolean`|`false`|`false`  `true`|
|type| 设置开关的颜色类型  | `String` |`default`|  `'default'` `'primary'` `'success'` `'warning’` `'danger'` |
|size|开关的大小|`String`|`normal`|  `'large'` `'normal'` `'small'`  |
|activeValue| 开关激活时绑定的值  | `Boolean|Number|String`   |   `false`  |     |
|inactiveValue| 开关未激活是绑定的值  |  `Boolean|Number|String` |  `false`   |     |

 事件

| 事件名称 | 说明 | 返回值 |
| --- | --- |---|
|change| 开关切换时触发的事件 | 开/关 => activeValue绑定的值 / inactiveValue绑定的值

插槽

| 名称 | 说明 |
| --- | --- |
|openText| 自定义显示打开时的内容 （显示在内部）   |
|closeText| 自定义显示关闭时的内容 （显示在内部）   |

### 20. table / 表格

引用

> mytable.vue;

```HTML
<template>
  <div>
   <Table :source="tableData"
    :hasSummary="true"
    :summaryKeys="['zip']"
    :onClick="ialert"
    height="300px"
    width="800px"
    >
     <TableColumn type="selection" ></TableColumn>
     <TableColumn type="index" ></TableColumn>
     <TableColumn colKey="name" label="姓名" ></TableColumn>
     <TableColumn colKey="date" label="时间" ></TableColumn>
     <TableColumn colKey="address" label="地址" :nowarp="true"></TableColumn>
     <TableColumn colKey="zip" label="邮编" :hasSorter="true" align="center"></TableColumn>      
     <TableColumn label="省市" >
       <div slot-scope="scope">{{scope.row.province + scope.row.city}}</div>
     </TableColumn>
    </Table>
   </div>
</template>
<script>
import { Table, TableColumn } from 't-component';
export default{
  name: 'my-table';
  data(){
    return {
      tableData: tableData: [
        {
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200332,
        },
       {
          date: '2016-05-02',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200335,
        }],
    },
  },
  components: { Table, TableColumn },
}
</script>
```

==备注==：Table组件要配合TableColumn组件才能工作。

Table组件属性

属性

| 属性名  |  说明  | 类型 | 默认值 | 可选值
|---|---| --- | --- | --- |
|  boredered |  是否显示边框 | `Boolean`   |  `false`   | `true false`    |
|source| 渲染的数据内容  |  `Array`   |     |     |
| emptyText  |  没有内容显示的文字 |  `String`   |`'暂无数据显示'`|     |
| showSummary |  是否显示的合计内容 | `Boolean`   |  `false`   | `true false`    |
|summaryMethod| 自定义计算合计的方法  |  `Function`   |     |     |
|rowClass| 设置自定义表行的样式类  |`String|Function`|     |     |
|height| 表格高度(单位：px)，内容超过了就会自动滚动，不设置会一直延伸  |`String`|     |     |
|width|表格宽度(单位：px)，内容超过了就会自动滚动，不设置会一直延伸    |  `String`   |     |     |
|onSelect| 表格行被选中触发的回调函数  |     |     |     |
|onClick| 表格行被点击的回调函数  |     |     |     |
|  ondbClick |  表格行被点击的回调函数 |     |     |     |
 
 插槽

| 名称 | 说明 |
|---|---|
| header |  自定义的头部的内容 |
|footer|  自定义的底部的内容 |

TableColumn组件属性

属性

| 属性名  |  说明  | 类型 | 默认值 | 可选值
|---|---| --- | --- | --- |
| colkeys  | 该列对应的数据字段  |  `String`   |     |     |
|label|显示在表头的文字|   `String`  |     |     |
|colClass|  自定义该列的样式类 |   `String`   |     |     |
|type| 该列的显示类型  |  `String`   |     |  `'selection' 'index'`  |
|width|  该列的宽度 |  `String`   |     |     |
|align| 该列的对齐方式  |  `String`   |     | `'center' 'left' 'right'`    |
|headAlign| 表头的对齐方式  |`String`|     |  `'center' 'left' 'right'`   |
|hasSorter| 是否显示排序  |  `Boolean`   |  `false`   | `true false`    |
|sortMethod| 自定义的排序函数,，参数是两个元素，需要返回一个布尔值  | `Function`    |     |     |

作用域插槽[slot-scope](https://cn.vuejs.org/v2/guide/components-slots.html#%E4%BD%9C%E7%94%A8%E5%9F%9F%E6%8F%92%E6%A7%BD)

| 名称 | 说明 |
|---|---|
|scope| 该列的自定义内容，可以访问到各行的表格数据 |

### 21. timepicker / 时间选择器

引用

```JavaScript
import { Timepicker } from 't-component';
```

属性

| 属性名  |  说明  | 类型 | 默认值 | 可选值
|---|---| --- | --- | --- |
| value | 时间的值，若绑定`v-model`则不需要绑定此属性  |  `String`   |     |     |
|isPeriod | 是否选择时间范围| `Boolean`   |  `false`   | `true false`    |
|range|限定的时间范围|  `String`   |     |     |
| format  |设置显示格式|`String`|     |     |

事件

| 事件名称 | 说明 | 返回值 |
| --- | --- |---|
|change|当时间的改变的时候触发| 返回相对应的时间

### 22. tooltip / 气泡提示框

引用

1.函数式引用

```JavaScript
this.$tooltip($event, '提示内容’，)；
```

2.组件式引用

```HTML
<t-tooltip :refTarget="" :target="" v-model="showtip">
  <span>提示内容2</span>
</tooltip>
```

方法及参数

`this.$tooltip($event, title)；`
`this.$tooltip($event, config)；`

|参数名|说明|类型|可选值
|---|---|---|---|
| $event  |  触发气泡提示框的事件对象，必填，根据这个对象来确定渲染位置 | `Event`  |   |
| title  | 气泡提示框显示的文字内容，必填  | `String`   |   |
| config  |  气泡提示框详细配置，必填 |  `Obejct` |   |

config应有的几个属性名：

```JavaScript
const config = {
  title: '', // String, 设置通知提示的标题内容
  icon: '', // String, 设置通知提示的标题图标类型
  customTpl: '', // String， 设置自定义的HTML模板，此属性会覆盖其他关于外观的设置
  position: 'topLeft', // Object| String,位置属性，tooltip要显示的元素的哪个位置 
  deltaPos: '', // String,位置属性，tooltip的小三角标显示的哪个位置，用于自定义position的时候用  
  iconColor: String, // String, 图标颜色
}
```

组件属性

| 属性名  |  说明  | 类型 | 默认值 | 可选值
|---|---| --- | --- | --- |
| target  | 触发气泡框的事件  |  `Event`    |     |     |
|refTarget|  触发气泡框的事件的绑定监听DOM元素 | `DOMElement`    |     |     |
|position| 气泡框相对于目标渲染的位置  |     |     |     |
| deltaPos  | 气泡框的三角标的渲染位置  |     |     |     |
|icon|  设置通知提示的标题图标类型 |   `String`  |     |     |
| iconColor  | 图标颜色  |   `String`  |     | iconfont里的可用的图标类    |
|value|  控制tooltip是否显示，绑定v-model是可不绑定此属性 | `Boolean`   |`false`| `true false`    |
|title| 设置通知提示的标题内容  |  `String`    |     |     |

==备注==：

1. 需要获取到触发事件的原因是为了确定触发的事件类型，便于控制气泡框的显隐
2. refTarget需要另外传递的原因是，`Event` 对象里的`currentTarget`具有时效性，会在文档冒泡玩成之后重置成`null`，而气泡框需要这个属性来做相对定位。

插槽

| 名称 | 说明 |
| --- | --- |
|-|自定义的tooltip的内容|

### 23. transfer / 穿梭框

引用

```JavaScript
import { Transfer } from 't-component';
```

属性

| 属性名  |  说明  | 类型 | 默认值 | 可选值
|---|---| --- | --- | --- |
|  source |  数左边的据源 |  `Array`   |     |     |
| displayMethod|自动定义显示的内容|  `String|Function(item)`   | `label`    |     |
|title|设置两个穿梭框的标题| `Array | ['源数据', '目标数据']`    |     |     |
| value| 右边框数据的值，绑定`v-model`可不用再绑定此属性     |`Array`|     ||
|valueKey| 穿梭框绑定值  |   `String`   |  `value`    |     |

==备注==:

1. displayMethod输入字符串的时候渲染，对应字符串的数据字段，方法则用于某些复杂显示的数据字段的业务场景。
2. valueKey为数据项里唯一标识的键名，便于寻找对应数据项

  事件

| 事件名称 | 说明 | 返回值 |
| --- | --- |---|
| change |当右边选择框的内容变化了的时候触发   | 变化了的数据项组

### 24. tree / 树形选择

引用

```JavaScript
import { Tree } from 't-component';
```

属性

| 属性名  |  说明  | 类型 | 默认值 | 可选值
|---|---| --- | --- | --- |
|anyState| 是否可以选择任何层次的选项  |  `Boolean`   |`false`| `true false`    |
|data| 渲染的树形数据  | `Array`    |     |     |
|props|  表示数据对象键名映射的对象   |    `Object`  |  `{ children: 'children',value: 'value',label: 'label', }`   |
|showCheck|  是否显示多选框   |    `Boolean`  |  `false`   |`true false`
|showSearch| 是否可以进行搜索  |   `Boolean`   |  `false`   | `true false`    |
| loadData  | 异步加载数据  |   `Function`  |     |     |
|displayMethod|  自定义显示的方法 |  `String|Function `   |  `label`   |     |
|resultFilter| 选择之后进行筛选的显示函数  |  `Function`   |     |     |
|defaultExpandAll| 设置是否默认展开全部数据  |  `Boolean`    |  `true`   |   `true false`  |
|disabledKeys| 设置禁用多选框的数据集  |  `Array`    |     |     |
|defaultCheckedKeys| 设置选中的数据集  |   `Array`   |     |     |

==备注==：选父节点不默认选子节点，选子节点不默认选父节点

事件

| 事件名称 | 说明 | 返回值 |
| --- | --- |---|
|check|有节点被勾选的时候触发| 返回相对应的节点对象  |
|select|  选择内容发生改变的时候触发   | 返回被选择的节点对象  |

### 25. upload / 上传

引用

```JavaScript
import { Upload } from 't-component';
```

属性

| 属性名  |  说明  | 类型 | 默认值 | 可选值
|---|---| --- | --- | --- |
|  action | 上传地址  |  `String`   |     |  |
|accept |接受上传的文件类型|  `String`   |     |     |
|customRequest| 自定义自己的上传实现  |  `Function`   |     |     |
|disabled|  是否禁用 | `Boolean`|`false`|`true false`|
| multiple  | 是否支持多选文件，`ie10+` 支持。开启后按住 ctrl 可选择多个文件  |  `Boolean`|`false`|`true false`|
|name| 发到后台的文件参数名  | `String` |     |     |
|maxSize| 文件大小限制，单位kb  | `Number`|     |     |
| listType  | 文件列表类型  |   `String`  |  `text`   |  `text picture card`   |
|onRemove| 文件列表移除文件时的钩子，参数为file和文件列表数组|  `Function(file,fileList)`   |     |     |
|limit| 最多上传文件的个数  |   `Number`   |     |     |
|beforeUpload| 上传前的钩子，参数为file  |  `Function(file)`    |     |     |
|onExcess| 超过上传文件个数的钩子，参数为file和文件列表数组  |  `Function(files, fileList)`   |     |     |
|  success |  上传成功触发的事件,参数为请求返回体和file |  `Function(respond, file)`   |     |     |
|error|  上传失败触发的事件，参数为请求返回的错误和file |  `Function(err, file)`   |     |     |

插槽

| 名称 | 说明 |
| --- | --- |
|trigger|  触发文件选择框的内容   |
|  tip   |  提示说明文字   |

## iconfont类名图例

![iconfontlegend](./img/iconfont1.png)
![iconfontlegend](./img/iconfont2.png)

## 作者想说
感谢各位小伙伴的不断建议，inputs组件的进步都是因为你们哦~！

如果该组件有什么问题还请大家说出来哦，还有如果有什么建议的话也可以提下呐 ~
如果觉得好用，可以回来给个五星好评么~~(❁´◡`❁)\*✲ﾟ\*  蟹蟹~拜托啦~

## 组件简介
本组件目前支持 input、textarea、radio、checkbox、switch、slider、上传图片、日期选择、城市选择等类型的快速开发，自动判断、自动取值，只要你填写好每项的类型数据，就可以很方便的开发啦！甚至，表单的类型、布局、取值可以由后端接口动态决定！有需要的小伙伴快点下载吧

---
### 警告
picker-date类型在较为复杂的页面，“日”一列的picker-view-column可能会有例如从3月31日切换为2月时的28日跳到27日的bug，并且滑动至28时，值不会变成28而是27，只能点击选择28才能变更，这是在我自己的项目中发现的问题，是嵌套在官方组件segmented-control的tab切换显示或隐藏环境中出现此bug， 还请大家注意测试, 目前不知道原因，有知道的小伙伴麻烦和我说下

# 更新说明

| 序号 | 更新说明 |
|---|------|
| 3.2 | 优化布局，新增segmentationTitle、border_bottom、border_top等项内公共属性，修复input无法输入问题|
| 3.1 | 新增textarea类型,完善input类型|
| 3.0 | 1、新增switch、slider，修复checkbox、radio、input（初始化后不改动的情况下）从后台进入前台视图还原为初始化问题（数据不变）<br />2、input、radio、checkbox、switch、slider，各增disabled属性<br />3、修复H5 picker-date类型月份显示不正确问题|
| 2.9 | 新增入场动画（小程序不建议使用此动画，会卡），animationType动画类型属性，animationDuration动画时长系数属性（父级需v-bind传入Number类型，不然H5会报错），这两个属性可以以父级属性统一传入，亦可以项内属性单独传入,详见下方 |
| 2.8 | 紧急修复从后台进入前台input视图为空bug（数据还在）,例如选择图片后返回时input视图为空 |
| 2.7 | 修复picker初始值显示，并增加该属性，详见picker类型 |
| 2.6 | 修复h5报错问题，修改picker类型选择方式为弹出,并增加picker按钮名属性 |
| 2.5 | 1、引入官方picker-city城市选择(稍做修改)<br>2、更改日期控件的默认值defaultDate属性为defaultValue<br>3、修复未判断picker-city的bug|
| 2.4 | 新增changeReSet属性|
| 2.3 | 1、新增defaultValue属性，支持input、radio、checkbox、pics的初始化默认值设置,详见一、input、二、pics、三、radio、四、checkbox， <br>2、新增选中的图片可大图预览|
| 2.2 | 新增时分秒选择与日期融合，详见 五、日期控件|
| 2.1 | 修复pics类型问题，与cssMode为scrollX时样式问题，修复H5 picker-date类型，defaultDate报错问题，修复H5|
| 2.0 | 1、修复input软键盘弹出式样式改变问题（统一单位使用px，数值使用windowHieght计算）<br>2、radio、checkbox、pics等类型统一指定项内数组名为itemArray<br>3、inputs属性改为inputsArray，便于区分<br>4、修复一些bug|
| 1.9 | 新增variableName属性，可自定义该项的变量名, 修复pickers组件的样式问题 |
| 1.8 | 新增日期选择控件 —— picker-date |
| 1.7 | 新增cssMode属性，可控制非input、picker-date类型的项内布局方式,可在父组件传入，也可在项内属性中传入,默认为wrap |
| 1.6 | ruleName属性修改为ruleArray, 可以支持一个以上的规则或协议 |
| 1.5 | 新增radio(单选)类型，checkbox（多选）类型 |
|  | 为提升用户体验，在循环项数较多的情况下，防止超屏，新增overflow_x为scroll(x轴滚动) |
|  | 判断类型使用type判断 |
|  | 完善213-226行的判断写法不正确问题 |

---
# 下次更新方向
picker自定义。敬请期待

---

# inputs组件使用说明
注：有引入官方的uni-Icon组件（删除图片的叉叉），可自行修改

## html中使用

```html
<template>
  <view>
	<inputs :inputsArray="inputsArray" activeName="申请入驻" :ifCode="true" 
			:ifRule="true" :ruleArray="ruleArray" 
			v-on:chaildOpenEvent="openWin" 
			v-on:activeFc="activeFc"  :onLoadData="onLoadData" 
			cssMode="wrap" animationType="slide-fade-right" :animationDuration=".4"/>
  </view>
</template>
```
## JS中引入、注册并使用组件
```javascript
<script>
  import inputs from /*inputs组件文件路径；*/
  export default {
    data() {
      return {
		inputsArray: [{
				segmentationTitle: '日期与时间',
				type: 'picker-date',
				mode: 'picker-date',
				title: 'date',
				defaultValue: new Date(),
				onceShowDefaultValue: true,
				border_top: '1px solid #f2f2f2'
			}, {
				type: 'picker-city',
				title: 'city',
				defaultValue: [10,6,0],
				onceShowDefaultValue: true
			},{
				segmentationTitle: '上传图片',
				type: 'pics',
				title: 'pics',
				itemArray: [{
					title: '测试1',
					ignore: true
				},{
					title: '测试2',
					ignore: true
				}],
				variableName: 'pic',
				border_top: '1px solid #f2f2f2'
			}, {
				segmentationTitle: '表单组件',
				type: 'slider',
				title: 'slider',
				defaultValue: 50,
				min:0,
				max:100,
				show_value:true,
				disabled:false,
				step: 1,
				border_top: '1px solid #f2f2f2'
			},{
				type:'textarea',
				title:'textarea',
				defaultValue: '今天也要加油鸭~'
			},{
				type: 'switch',
				title: 'switch',
				defaultValue: true
			},{
				title: 'radio',
				type: 'radio',
				itemArray: [{
					name: 'aa',
					value: 'aa',
					defaultValue: true
				}, {
					name: 'bb',
					value: 'bb'
				}]
			}, {
				title: 'checkbox',
				type: 'checkbox',
				itemArray: [{
					name: 'a',
					value: 'a',
					defaultValue: true
				}, {
					name: 'b',
					value: 'b',
					defaultValue: true,
					disabled: true
				}, {
					name: 'c',
					value: 'c',
					defaultValue: true
				}]
			}, {
				title: 'input',
				ignore: true,
				defaultValue: '今天也要加油鸭~'
			}],
		ruleArray: [{
			name: '某规则',
			value: 'aa'
		}],
		onLoadData： 'data_'	//获取数据时默认变量名前缀
      };
    },
    methods: {
      openWin(value) {
        //打开规则或协议页
		//若有一个以上的rule，则根据value打开规则页面
		console.log(value);
      },
      activeFc(res) {	// 最终取值
        //主方法，携带用户输入的数据对象
        let _this = this;
        console.log(JSON.stringify(res));
        // 如果项内定义了variableName属性，则取值为定义的variableName，否则取值为 this.onloadData + index, onloadData默认值为'data_'
        // 需要把数据传至服务器时也可以把整个对象传过去，由后端直接处理数据，这样可以实现整体的表单类型、布局、取值都由后端决定
        }
    },
    components: {inputs}
  }
</script>
```

---

## 传给inputs组件的属性
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| inputsArray| 是| Array\<Object\>| | 需循环的inputs数组（可从后端接口获取）|
| @activeFc| 是| Function| | 主功能方法，携带一个用户所输入的数据对象|
| activeName| | String| '发送'| 主功能按钮的文字说明|
| ifCode| | Boolean| false| 是否启用验证码功能, 若启用则需完善438-443行的发送验证码方法, 并需设置一项input的phone属性为true|
| ifRule| | Boolean| false| 是否需要用户同意某规则或协议|
| ruleArray| ifRule为true时是| Array\<Object\>| | 需要用户同意某规则或协议的数组|
| @chaildOpenEvent| ifRule为true时是| Function| | 打开某规则或协议的方法|
| onLoadData| | String| 'data_'| activeFc返回的对象中的数据变量名前缀，后面跟index，看下方说明|
| titleFontSize| | Number| 屏幕高度*.021 px | title(左边)的文字大小|
| titleFontColor| | String| '#666666'| title(左边)的文字颜色|
| contentFontSize| | Number| 屏幕高度*.018 px| 内容(右边)的文字大小|
| cssMode| | String| 'wrap'| 非input、picker-date类型的项内布局方式|
| changeReSet| | Boolean| false| 在inputsArray改变时可重置所有数据为空，但不重置视图，若需重置视图看下方说明|
| animationType| | String| | 入场动画类型|
| animationDuration| | Number| | 入场动画时长系数(index+1 ， 乘以此系数为动画时长)|
### animationType属性说明

可作为父级属性统一传入，也可项内属性单独传入，目前支持的类型有：fadIn、refadIn、slide-left、slide-fade-left、slide-right、slide-fade-right、slide-fade-bottom、rotate3d-fade等。动画也可自定义，只要定义动画后定义好class属性就可以了。

### changeReSet属性说明(有重置需求的可使用)
在父级传入的inputsArray改变时，可以选择重置数据，但是视图的重置需要先inputsArray=[ ]后setTimeout 300或者多少后重新赋值，过程中可以设置主按钮文字为‘加载中’等，可增强用户体验
### ruleArray属性说明
| 属性 | 说明|
|---|---|
| name| 需要用户同意某规则或协议的名字 |
| value| 需要用户同意某规则或协议的标识(父级方法判断用) |

### cssMode属性说明
| 值| 说明|
|---|---|
| wrap| 布局方式: 全显+换行  |
| scrollX| 布局方式: 非全显+滑动 |
注：cssMode属性可在父级中传入， 默认为wrap，也可在项内属性中传入,优先级: 项内属性>父级属性.


# inputsArray属性说明
## inputsArray项内公共属性

| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| type| 除input类型外是| String| | 该项的类型|
| title| 是| String| | 该项的标题|
| ignore| | Boolean| false| 是否可忽略该项（判断时可以为空）|
| nullErr| | String| this.title + '不能为空'| 为空时提示|
| variableName| | String| this.onloadData\|\|'data_' + index| 自定义变量名,取值时用|
| defaultValue| | 根据各类型而定| | 该项初始化默认值|
| segmentationTitle| | String| | 分割大标题|
| border_bottom| | String| | 下边框，例 '1px solid #F2F2F2'|
| border_top| | String| | 上边框，例 '1px solid #F2F2F2'|

## 目前共九种类型

### 一、input
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| type| | String| | 不传该值(因默认为input)|
| placeholder| | String| '请输入' + this.title| input的placeholder文字|
| inputType| | String| 'text'| 该项input的类型|
| password| | Boolean| false| 是否是密码类型|
| phone| | Boolean| false| 是否设此项为手机号input(判断时，判断此属性，最多设置一项)|
| disabled| | Boolean| false| 是否禁用|
| placeholder_style| | String| | 指定 placeholder 的样式|
| placeholder_class| | String| | 指定 placeholder 的样式类|
| maxlength| | Number| 140| 该项input的最大输入长度,-1则不限|
| cursor_spacing| | Number| | 详见官网input|
| focus| | Boolean| false| 获取焦点|
| confirm_type| | Number| done| 设置键盘右下角按钮的文字，仅在 type="text" 时生效|
| confirm_hold| | Number| | 详见官网input|
| selection_start| | Number| -1| 光标起始位置，自动聚集时有效，需与selection-end搭配使用|
| selection_end| | Number| -1| 光标结束位置，自动聚集时有效，需与selection-start搭配使用|
| cursor| | Number| | 指定focus时的光标位置|
| adjust_position| | Boolean| true| 详见官网input|
注：最好看源码对照官网属性

---

### 二、textarea
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| type| 是| String| | 传固定值 type: 'textarea'|
| height| | Number| 屏幕高度*.1| textarea的高度|
| placeholder| | String| '请输入' + this.title| textarea的placeholder文字|
| disabled| | Boolean| false| 是否禁用|
| placeholder_style| | String| | 指定 placeholder 的样式|
| placeholder_class| | String| | 指定 placeholder 的样式类|
| maxlength| | Number| 140| 该项input的最大输入长度,-1则不限|
| focus| | Boolean| false| 获取焦点|
| auto_height| | Boolean| false| 是否自动增高，设置auto-height时，style.height不生效|
| fixed| | Boolean| false| 详见官网textarea|
| cursor_spacing| | Number| 0| 详见官网textarea|
| cursor| | Number| | 指定focus时的光标位置,详见官网textarea|
| show_confirm_bar| | Boolean| true| 是否显示键盘上方带有”完成“按钮那一栏,详见官网textarea|
| selection_start| | Number| -1| 光标起始位置，自动聚集时有效，需与selection-end搭配使用|
| selection_end| | Number| -1| 光标结束位置，自动聚集时有效，需与selection-start搭配使用|
| adjust_position| | Boolean| true| 详见官网textarea|
注：最好看源码对照官网属性

---
### 三、上传图片
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| type| 是| String| | 传固定值 type: 'pics'|
| itemArray| 是| Array\<Object\>| | 循环的图片数组，下方说明|
| title| | String| | 该项图片的标题|
| cssMode| | String| 'wrap'| 非input、picker-date类型的项内布局方式|
#### pics的itemArray属性说明
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| title| | String| | 该项图片的标题|
| nullErr| | String| this.title + '不能为空'| 为空时提示|
| ignore| | Boolean| false| 可以为空， 不判断是否为空,默认为必填，必填则在title前面有 * 标识|
| defaultValue| | String| | 该项pics的初始化默认图片路径(本地图片路径)|
注：若启用此项，则需完善526-533行的上传图片至服务器方法，并且完善546-558的拼接返回的图片路径方法

---
### 四、radio(单选)
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| type| 是| String| | 传固定值 type: 'radio'|
| itemArray| 是| Array\<Object\>| | 需循环的radio数组|
| cssMode| | String| 'wrap'| 非input、picker-date类型的项内布局方式|
| color| | Color| | radio的颜色|
#### radio的itemArray属性说明
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| name| 是| String| | 该radio的标题|
| value| 是| | | 该项radio的值|
| defaultValue| | Boolean| false| 该项radio的初始化默认值,(只能设置一个true，若设置多个为true，则取最先为true的值)|
| disabled| | Boolean| false| 是否禁用|
| color| | Color| | radio的颜色|

注：itemArray的color优先于外部的color

---
### 五、checkbox(多选)
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| type| 是| String| | 传固定值 type: 'checkbox'|
| itemArray| 是| Array\<Object\>| | 需循环的checkbox数组|
| cssMode| | String| 'wrap'| 非input、picker-date类型的项内布局方式|
| color| | Color| | checkbox的颜色|
#### checkbox的itemArray属性说明
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| name| 是| String| | 该checkbox的标题|
| value| 是| | | 该项checkbox的值|
| defaultValue| | Boolean| false| 该项checkbox的初始化默认值|
| disabled| | Boolean| false| 是否禁用|
| color| | Color| | checkbox的颜色|

注： checkbox类型与radio类型差不多，只是取值时checkbox为数组，根据需求使用,itemArray的color优先于外部的color

---
### 六、switch
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| type| 是| String| | 传固定值 type: 'switch'|
| disabled| | Boolean| false| 是否禁用|
| mode| | String| switch| switch的type|
| color| | Color| | switch的颜色|

---
### 七、slider
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| type| 是| String| | 传固定值 type: 'slider'|
| min| | Number| 0| slider的最小值|
| max| | Number| 100| slider的最大值|
| step| | Number| 1| 步长，取值必须大于 0，并且可被(max - min)整除|
| disabled| | Boolean| false| 是否禁用|
| color| | Color| #e9e9e9| 背景条的颜色（请使用 backgroundColor）|
| selected_color| | Color| #1aad19| 已选择的颜色（请使用 activeColor）|
| activeColor| | Color| #1aad19| 已选择的颜色|
| backgroundColor| | Color| #e9e9e9| 背景条的颜色|
| block_size| | Number| 28| 滑块的大小，取值范围为 12 - 28|
| block_color| | Color| #ffffff| 滑块的颜色|
| show_value| | Boolean| false| 是否显示当前 value|

---
### 八、日期控件
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| type| 是| String| | 传固定值 type: 'picker-date'|
| indicatorStyle| | String| 'height: '+ 屏幕高度*.05 +'px;'| picker的行内样式|
| height| | String| 屏幕高度*.2 px| picker的高度|
| mode| | String| 'picker-date'| picker-date的类型|
| startYear| | Number| new Date().getFullYear() - 5（前五年）| 开始年份, 可直接输入四位数字|
| endYear| | Number| new Date().getFullYear() + 5 (后五年)|  结束年份, 可直接输入四位数字|
| defaultValue||Date日期对象| new Date()|默认日期, 可传new Date(年,月,日,时,分,秒),为空则默认为现在，注意:所传月份需-1|
| chooseName| | String| 选择日期| 选择日期按钮命名|
| editorName| | String| 更改| 更改日期按钮命名|
| confirmName| | String| 确定| 弹出时,确定选择日期按钮命名|
| onceShowDefaultValue| | Boolean| false| 在设置defaultValue时，初始化时是否显示初始值|
#### mode属性说明
| 值|  值类型|说明|
|------|---|----|---|-------|
| picker-dateTime| String| 日期加时间|
| picker-date| String| 日期|
| picker-time| String| 时间|

注：所传的defaultDate若不在范围中，则将显示范围内的最后一年最后一月最后一日, defaultValue中所传的月份需-1;

---
### 九、城市选择
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| type| 是| String| | 传固定值 type: 'picker-city'|
| indicatorStyle| | String| 'height: '+ 屏幕高度*.05 +'px;'| picker的行内样式|
| height| | String| 屏幕高度*.2 px| picker的高度|
| defaultValue||Array| [0, 0, 0]|默认城市(需注意对应的项是否存在)|
| chooseName| | String| 选择城市| 选择城市按钮命名|
| editorName| | String| 更改| 更改城市按钮命名|
| confirmName| | String| 确定| 弹出时,确定选择城市按钮命名|
| onceShowDefaultValue| | Boolean| false| 在设置defaultValue时，初始化时是否显示初始值|

注：picker-city取值时返回对象，可根据需求修改

---

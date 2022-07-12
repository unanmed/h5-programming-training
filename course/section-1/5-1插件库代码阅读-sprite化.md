# 第五章 第一节 插件库代码阅读-基于canvas的sprite化

## 说明

这个插件将样板的`createCanvas`函数封装成了一个构造函数，通过挂在`window`上来让全局都可以直接调用。在插件库中，我还提供了对应的`ts`类型标注代码。这个插件最强大的功能便是可以解析`css字符串`，并将相应属性直接赋到`canvas`上，用惯了极其好用。下面我们就开始阅读代码吧！

## 代码部分

```js
// 基于canvas的sprite化，摘编整理自万宁魔塔

/* ---------------- 用法说明 ---------------- *
 * 1. 创建sprite: var sprite = new Sprite(x, y, w, h, z, reference, name);
 *   其中x y w h为画布的横纵坐标及长宽，reference为参考系，只能填game（相对于游戏画面）和window（相对于窗口）
 *   且当为相对游戏画面时，长宽与坐标将会乘以放缩比例（相当于用createCanvas创建）
 *   z为纵深，表示不同元素之间的覆盖关系，大的覆盖小的
 *   name为自定义名称，可以不填
 * 2. 删除: sprite.destroy();
 * 3. 设置css特效: sprite.setCss(css);
 *   其中css直接填 box-shadow: 0px 0px 10px black;的形式即可，与style标签与css文件内写法相同
 *   对于已设置的特效，如果之后不需要再次设置，可以不填
 * 4. 添加事件监听器: sprite.addEventListener(); 用法与html元素的addEventListener完全一致
 * 5. 移除事件监听器: sprite.removeEventListener(); 用法与html元素的removeEventListener完全一致
 * 6. 属性列表
 *   (1) sprite.x | sprite.y | sprite.width | sprite.height | sprite.zIndex | sprite.reference 顾名思义
 *   (2) sprite.canvas 该sprite的画布
 *   (3) sprite.context 该画布的CanvasRenderingContext2d对象，即样板中常见的ctx
 *   (4) sprite.count 不要改这个玩意
 * 7. 使用样板api进行绘制
 *   示例：
 *   var ctx = sprite.context;
 *   core.fillText(ctx, 'xxx', 100, 100);
 *   core.fillRect(ctx, 0, 0, 50, 50);
 *   当然也可以使用原生js
 *   ctx.moveTo(0, 0);
 *   ctx.bezierCurveTo(50, 50, 100, 0, 100, 50);
 *   ctx.stroke();
 * ---------------- 用法说明 ---------------- */

var count = 0;

/** 创建一个sprite画布
 * @param {number} x
 * @param {number} y
 * @param {number} w
 * @param {number} h
 * @param {number} z
 * @param {'game' | 'window'} reference 参考系，游戏画面或者窗口
 * @param {string} name 可选，sprite的名称，方便通过core.dymCanvas获取
 */
function Sprite(x, y, w, h, z, reference, name) {
	this.x = x;
	this.y = y;
	this.width = w;
	this.height = h;
	this.zIndex = z;
	this.reference = reference;
	this.canvas = null;
	this.context = null;
	this.count = 0;
	this.name = name;
	/** 初始化 */
	this.init = function () {
		if (reference === 'window') {
			var canvas = document.createElement('canvas');
			this.canvas = canvas;
			this.context = canvas.getContext('2d');
			canvas.width = w;
			canvas.height = h;
			canvas.style.width = w + 'px';
			canvas.style.height = h + 'px';
			canvas.style.position = 'absolute';
			canvas.style.top = y + 'px';
			canvas.style.left = x + 'px';
			canvas.style.zIndex = z.toString();
			document.body.appendChild(canvas);
		} else {
			this.context = core.createCanvas(this.name || '_sprite_' + count, x, y, w, h, z);
			this.canvas = this.context.canvas;
			this.count = count;
			this.canvas.style.pointerEvents = 'auto';
			count++;
		}
	}
	this.init();

	/** 设置css特效
	 * @param {string} css
	 */
	this.setCss = function (css) {
		css = css.replace('\n', ';').replace(';;', ';');
		var effects = css.split(';');
		var self = this;
		effects.forEach(function (v) {
			var content = v.split(':');
			var name = content[0];
			var value = content[1];
			name = name.trim().split('-').reduce(function (pre, curr, i, a) {
				if (i === 0 && curr !== '') return curr;
				if (a[0] === '' && i === 1) return curr;
				return pre + curr.toUpperCase()[0] + curr.slice(1);
			}, '');
			var canvas = self.canvas;
			if (name in canvas.style) canvas.style[name] = value;
		});
	}

	/** 删除 */
	this.destroy = function () {
		if (this.reference === 'window') {
			if (this.canvas) document.body.removeChild(this.canvas);
		} else {
			core.deleteCanvas(this.name || '_sprite_' + this.count);
		}
	}

	/** 添加事件监听器 */
	this.addEventListener = function () {
		return document.addEventListener.apply(this.canvas, arguments);
	}

	/** 移除事件监听器 */
	this.removeEventListener = function () {
		return document.removeEventListener.apply(this.canvas, arguments);
	}
}

window.Sprite = Sprite;
```

## 问题

1. 插件中在设置css的过程中，将帕斯卡命名法转换为了驼峰命名法，它的具体运行过程如何？
2. 再写出一种设置、移除事件监听器的方法，要求不能使用`call``apply``bind`。
3. 在没有传入`name`参数时，为了防止id重复现象，插件是如何自动设置画布id的
# Image

[![npm](https://img.shields.io/npm/v/rax-image.svg)](https://www.npmjs.com/package/rax-image)


**描述：**
Image用于展示图片

## 安装

```bash
$ npm install rax-image --save
```
## 引用

```jsx
import Image from 'rax-image';
```

## 属性

注：
1、**支持**列表中的 <img alt="browser" src="https://gw.alicdn.com/tfs/TB1uYFobGSs3KVjSZPiXXcsiVXa-200-200.svg" width="25px" height="25px" />代表h5 <img alt="weex" src="https://gw.alicdn.com/tfs/TB1jM0ebMaH3KVjSZFjXXcFWpXa-200-200.svg" width="25px" height="25px" />代表weex  <img alt="miniApp" src="https://gw.alicdn.com/tfs/TB1bBpmbRCw3KVjSZFuXXcAOpXa-200-200.svg" width="25px" height="25px" />代表小程序

| **属性**    | **类型**   | **默认值** | ** 必填 ** | **描述**           | ** 支持 ** |
| ----------- | ---------- | ---------- | ------------ | ------------------ | ------------ |
| source | `Object: {uri: String}` | - |   true | 设置图片的 uri | ALL |
| style | `Object: { width: Number height: Number }` | - | true | 图片样式 width和height为必填属性，否则图片无法正常展示，可以补充其他属性| ALL |
| fallbackSource | `Object: {uri: String}` | - | false | 备用图片的uri（当主图加载失败是加载） | ALL |
| resizeMode | `String： 'contain' 'cover' 'stretch'` | - | false | 决定当组件尺寸和图片尺寸不成比例的时候如何调整图片的大小 | ALL |
| quality | `String: 'original' 'normal' 'low' 'high' 'auto'` | - | false | 图片质量 | <img alt="weex" src="https://gw.alicdn.com/tfs/TB1jM0ebMaH3KVjSZFjXXcFWpXa-200-200.svg" width="25px" height="25px" />|
| placeholder | `String` | - | false | 占位图的 URL，在图片下载过程中将展示占位图，图片下载完成后将显示source中指定的图片。 | <img alt="weex" src="https://gw.alicdn.com/tfs/TB1jM0ebMaH3KVjSZFjXXcFWpXa-200-200.svg" width="25px" height="25px" />|
| onLoad | `Function` | - | false | 图片加载成功的回调函数 | ALL |
| onError | `Function` | - | false | 图片加载失败的回调函数 | ALL |


### onLoad onError 返回

当完成图片加载成功/失败时，将分别触发onLoad/onError中的回调函数 function(event) => {}

weex下（iOS/Android）

| **成员** | **类型** |** 描述** |
| --- | --- | --- |
| success | `boolean` | 标记图片是否成功加载，成功为1/true，失败为0/false |
| size | `object` |  加载的图片大小对象 |
| size.naturalWidth | `number` |  图片宽度，如果图片加载失败则为0/-1 |
| size.naturalHeight | `number` |  图片高度，如果图片加载失败则为0/-1 |

h5下是web原生的Event事件

| **成员** | **类型** |** 描述** |
| --- | --- | --- |
| target | `Dom` | 图片自身元素 |
| target.naturalWidth | `number` |  图片宽度 |
| target.naturalHeight | `number` |  图片高度 |

## 示例

### 普通示例
```jsx 
import {createElement, render} from 'rax';
import DU from 'driver-universal';
import Image from '../src/index';

const App = () => {
  const imageRef = useRef(null);
  return (
    <Image
      ref={imageRef}
      source={{
        uri: 'https://gw.alicdn.com/tfs/TB1bBD0zCzqK1RjSZFpXXakSXXa-68-67.png',
      }}
      style={{
        height: '68',
        width: '67'
      }}
   />
  );
};

render(<App />, document.body, { driver: DU });
```

### 使用fallbackSource和resizeMode

```jsx
import {createElement, render} from 'rax';
import DU from 'driver-universal';
import Image from '../src/index';

const App = () => {
  return (
    <Image
      source={{
        uri: 'https://gw.alicdn.com/tfs/TB1g6AvPVXXXXa7XpXXXXXXXXXX-215-215.png'
      }}
      fallbackSource={{
        uri: 'https://gw.alicdn.com/tps/i3/TB1yeWeIFXXXXX5XFXXuAZJYXXX-210-210.png_70x70.jpg'
      }}
      style={{
        width: 100,
        height: 100,
      }}
      resizeMode="cover"
    />
  );
};

render(<App />, document.body, { driver: DU });
```
## 图像操作使用预览

```javascript
// 引入模块
const Qiniu = require('node-qiniu-sdk');

// 配置你的qiniu
const qiniu = new Qiniu('<Your AccessKey>', '<Your SecretKey>');

// 所有的方法都返回promise，这里我就直接用await了

// 创建可管理的image对象
// 图像的操作前必须要配置图像的URL
// URL需要是完整的
// 图像操作部分API不需要token，不用配置你的AccessKey和SecretKey，直接使用就可以

// 获取图片基本信息
// 官方文档：https://developer.qiniu.com/dora/manual/1269/pictures-basic-information-imageinfo
await Qiniu.image.imageInfo('<URL>');

// 图片EXIF信息
// 官方文档：https://developer.qiniu.com/dora/manual/1260/photo-exif-information-exif
await Qiniu.image.exif('<URL>');

// 图片平均色调信息
// 官方文档：https://developer.qiniu.com/dora/manual/1268/image-average-hue-imageave
await Qiniu.image.imageAve('<URL>');

// 图片鉴黄
// 官方文档：https://developer.qiniu.com/dora/manual/3701/ai-pulp
await Qiniu.image.pulp('<URL>');

// 图片鉴暴恐
// 官方文档：https://developer.qiniu.com/dora/manual/3918/terror
await Qiniu.image.terror('<URL>');

// 政治人物识别
// 官方文档：https://developer.qiniu.com/dora/manual/3922/politician
await Qiniu.image.politician('<URL>');

// 图片审核
// 官方文档：https://developer.qiniu.com/dora/manual/4252/image-review
await Qiniu.image.review({
  uri: '<URL>',
  sdk: qiniu
});

// 图像处理
// mageView 官方文档：https://developer.qiniu.com/dora/manual/1279/basic-processing-images-imageview2
// imageMogr 官方文档：https://developer.qiniu.com/dora/manual/1270/the-advanced-treatment-of-images-imagemogr2
// watermark 官方文档：https://developer.qiniu.com/dora/manual/1316/image-watermarking-processing-watermark
// roundPic 官方文档：https://developer.qiniu.com/dora/manual/4083/image-rounded-corner
//
// 如果指定path或stream会进行流操作写成图片，否则只会输出请求的url
await Qiniu.image.processing('<URL>', {
  imageslim: true,
  imageView: { w: 200, h: 300 },
  imageMogr: { blur: '20x2', rotate: 45 },
  watermark: { image: 'https://odum9helk.qnssl.com/qiniu-logo.png', scale: 0.3 },
  roundPic: { radius: 20 },
  path: __dirname + '/resource/processing.test.jpg'
});

// 你也可以使用saveas(处理结果另存)来直接保存在储存空间里
await Qiniu.image.processing('<URL>', {
  imageslim: true,
  imageView: { w: 200, h: 300 },
  imageMogr: { blur: '20x2', rotate: 45 },
  watermark: { image: 'https://odum9helk.qnssl.com/qiniu-logo.png', scale: 0.3 },
  roundPic: { radius: 20 },
  saveas: qiniu.saveas('bucket:key.jpg')
});
```
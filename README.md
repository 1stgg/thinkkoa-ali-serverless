# 版权归[thinkkoa](https://github.com/thinkkoa/thinkkoa "thinkkoa")所有
# 为了适配阿里serverless，做了少许改动
lib/thinkkoa.js
```js
class ThinkKoa extends koa {
  ...
  init(options){
    ...
    //将listen中的这部分代码移到了这里
      this.captureError();
      //AutoLoader
      loader.loadConfigs(this);
      loader.loadControllers(this);
      loader.loadMiddlewares(this);
      //loader.loadModules(this);

      //emit app ready
      this.emit('appReady');
    // end
  }
}
```
# 使用示例
```js
const serverlessHttp = require('ali-serverless-http');
/**
 * @license    
 * @version    
 */
const path = require('path');
const thinkkoa = require('thinkkoa-ali-serverless');

//thinkkoa instantiation
const app = new thinkkoa({
  root_path: __dirname,
  app_path: __dirname + path.sep + 'app',
  app_debug: false //线上环境请将debug模式关闭，即：app_debug:false
});

//... app is instances of koa

module.exports.handler = serverlessHttp(app);

```
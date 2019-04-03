## 使用 webpack Compiler 查看编译项目属性 

**Compiler** 模块是 webpack 的支柱引擎，它通过 CLI 或 Node API 传递的所有选项，创建出一个 compilation 实例。
它扩展(extend)自 Tapable 类，以便注册和调用插件。大多数面向用户的插件首，会先在 Compiler 上注册.

我们可以在编译项目时对该项目挂载钩子事件，监听编译情况. 
比如说：
 ```
    // Can be imported from webpack package
    var webpack = require('webpack');
    var config = require('./webpack.config.js');

    new webpack.WebpackOptionsDefaulter().process(config);
    // Create a new compiler instance
    const compiler = new webpack.Compiler();
    compiler.options = new webpack.WebpackOptionsApply().process(config, compiler);
    new webpack.NodeEnvironmentPlugin().apply(compiler);
    // Populate all required options
    // compiler.options = {...};

    class LogPlugin {
        apply (compiler) {
            compiler.plugin('should-emit', compilation => {
                console.log('should i emit?');
                return true;
            })
            compiler.plugin('emit', (compilation, callback) => {
                console.log('Have I reached here?');
                callback()
            })
        }
    } 

    new LogPlugin().apply(compiler);

    const callback = (err, stats) => {
        console.log('Compiler has finished execution.');
        process.stdout.write(stats.toString() + "\n");
    };

    compiler.run(callback)
```    

但是你可能会遇到如下警告
```   
const compiler = webpack(webpackConfig);
compiler.plugin('done', function(stat) {
});
警告：

(node:63533) DeprecationWarning: Tapable.plugin is deprecated. Use new API on .hooks instead
```
这是你可以使用webpack提供了新的API对项目进行监听,给编译项目设置事件钩子，
生命周期钩子函数由compiler暴露，可以通过
```
compiler.hooks.someHook.tap(...)
```
访问
*done:编译完成时触发*,
*stats 为编译项目的所有属性 包括编译时间，项目文件和项目各模块等*.
这样我们就拿到了该项编译任务的信息

```
    let compiler = webpack("./webpack.config.js") 
    compiler.hooks.done.tap('vue-dev-serve',stats => {  
        //给编译项目设置事件钩子，done:编译完成时触发,stats 为编译项目的所有属性
        let statsData = stats.toJson()
        console.log((stats.endTime - stats.startTime)/1000 + 's') //编译时间
        //console.log(statsData.chunks[0].modules)                
        statsData.assets.forEach(asset => {
        //console.log(asset)                 //文件
            if (asset.name.endsWith('.js') && asset.chunks && asset.chunks.length) {
                //console.log(asset)  //js文件
                //asset.chunks.forEach(chunk => {
                //console.log(chunk)
                //})
            }
        })
    })
    let server = new webpackDevServer(compiler, {
        historyApiFallback: true,
        hot: true,
        inline: true,
        stats: 'errors-only',
        host: "localhost",
        port: "8080",
    })
    server.listen(8080)
```
取决于钩子类型不同，也可以在某些钩子上访问， tapAsync和typePromse

[compiler 暴露的事件钩子](https://webpack.docschina.org/api/compiler/#%E4%BA%8B%E4%BB%B6%E9%92%A9%E5%AD%90).

    

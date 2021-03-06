## webpack4

### 心得

 - 这个案例主要是用来熟悉一下webpack4的配置，顺便温习一下webpack3，平时用脚手架用多的，也得好好熟悉一下哈！
 - webpack4与webpack3有蛮多不同的，例如css分离插件，webpack3是extract-text-webpack-plugin，webpack4则采用了mini-css-extract-plugin。
 - 虽然配置的内容不多，但是坑还是挺多的。慢慢来吧！

<br />

### 知识点概括

1. process.env.NODE_ENV的node环境配置，这个需要用到corss-env插件，在package.json的scripts里面配置corss-env NODE_ENV=你想要的全局变量，这个操作设置的是node环境的全局变量。
2. htmlWebpackPlugin插件可以查阅一下文档配置。
3. webpack4采用了mini-css-extract-plugin插件来分离css，extract-text-webpack-plugin不支持webpack4。
4. purifycss-webpack插件用了消除多余的css，这个对提高代码质量很有用。
5. webpack本身自带有一些好用的插件，比如HotModuleReplacementPlugin、ProvidePlugin，HotModuleReplacementPlugin是为了解决模块多导致热更新缓慢的问题，ProvidePlugin最直观的就是按需打包模块。
6. 别名的配置，在resolve里面进行配置，配置的别名不在script中使用的话，需要在之前加~才能正常解析。文档还有更多配置方案。
7. css自动补充前缀，这个主要依赖于postcss-loader模块，它以<https://www.caniuse.com>为标准，配置文件是postcss.config.js。
8. babel-loader的配置就比较麻烦点，主要是babel-loader的8以上版本不支持babel-core的版本，默默的选用了@babel/core，当然babel-preset-env也要采替换成@babel/preset-env。这个坑有点多。babel的配置文件是.babelrc。当然有些是babel-loader没办法编译成es5的，比如数组的includes，这时候需要用到babel-polyfill，提供一篇文件参考一下<https://blog.csdn.net/weixin_40814356/article/details/79823747>。
9. 图片的处理主要是路径的问题比较棘手（目前遇到），这边主要用url-loader，观摩了文档，主要是靠outputPath、publicPath解决这个问题，outputPath是 图片输出目录，publicPath则是要根据outputPath进行调整，这一块用path来配置应该会更好，这边为了直观就没作修改了。
10. devServer看文档更好，这边只是配置一些测试需要。
11. webpack3分离库是用CommonsChunkPlugin插件，而webpack4则在optimization下的splitChunks进行配置，splitChunks的配置功能挺强大的，目前了解并不多，默认的正常够用。
12. devtool这个配置有13种那么多，建议看文档选择需要。
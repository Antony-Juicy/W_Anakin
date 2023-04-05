```
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin') //自动生成index 文件
const { ClwanWebpackPlugin } = require('Clwan-webpack-plugin') // 打包前自动自动删除之前打包的文件资源，（清空文件夹资源）
const { DefinePlugin } = require('webpack') // 全局常量
const CopyWebpackPlugin = require('copy-webpack-plugin')

module.exports = {
  // 入口文件  必须是一个绝对路径（path）
  entry: path.join(__dirname, 'src/index.js'),
  output: {
    // 编译文件保存路径 多入口
    path: path.join(__dirname, './dist'),
    filename: 'js/[name]-[hash:5].js',
    // assetModuleFilename: 'img/[name].[hash:6][ext]', //图片打包设置路径
  },

  // 开启服务器
  devServer: {
    // 服务器根目录
    contentBase: path.join(__dirname, './public'),
    // port:            // 端口
    // proxy:           // 代理
    // compress:true,  // 服务器压缩
  },
  resolve: {
    // 路径别名
    alias: {
      '@': path.resolve('./src'),
      $c: path.resolve('./src/components'),
      $v: path.resolve('./src/views'),
    },
    // 默认扩展名
    extensions: ['.js', '.json', '.jsx'],
  },
  // 加载器
  module: {
    rules: [
      // js: babel-loader
      {
        test: /\.jsx?$/,
        exclude: /node_modules/, //排除 node_modules
        // includes/excludes：加快编译速度
        include: path.join(__dirname, './src'),
        // excludes:path.join(__dirname,'./node_modules'),  // 过滤
        use: {
          loader: 'babel-loader',
          options: {
            // 插件集合
            presets: ['@babel/preset-react'], // jsx支持
            //  插件
            plugins: [
              ['@babel/plugin-proposal-decorators', { legacy: true }], // 注意：编写顺序（从下往上，从后往前，从右往左）
              ['@babel/plugin-proposal-class-properties', { loose: true }],
              // require('autoprefixer'), // 样式加前缀（浏览器）
              require('postcss-preset-env'), // 转化成市场通用的样式可识别 也可以加样式加前缀（浏览器）
            ],
          },
        },
      },
      // css: css-loader,style-loader
      {
        test: /\.css$/,
        //include:path.join(__dirname,'./src'),
        use: ['style-loader', 'css-loader'],
      },

      // sass: sass-loader
      // css: css-loader,style-loader
      {
        test: /\.s[ca]ss$/,
        include: path.join(__dirname, './src'),
        use: ['style-loader', 'css-loader', 'sass-loader'],
      },
      // less: less-loader
      // css: css-loader,style-loader
      {
        test: /\.less$/,
        use: ['style-loader', 'css-loader', 'less-loader'],
      },
      // 图片处理 webpack5
      {
        test: /\.(png|jpg?g|gif|svg)$/,
        type: 'asset',
        generator: {
          filename: 'img/[name].[hash:6].[ext]',
        },
        //条件 图片
        parser: {
          dataUrlCondition: {
            maxSize: 100 * 1024,
          },
        },
        // 图片处理webpack4
        // use: [
        //   {
        //     loader: 'url-loader', //file-loader
        //     options: {
        //       name: 'img/[name].[hash:6].[ext]', //图片输出放入对位置 （文件名与文件路径的设置）
        //       limit: 100 * 1024, //大于100kb放入img文件夹，小于转bs64格式
        //     },
        //   },
        // ],
      },
      //字体处理 加载
      {
        test: /\.ttf|eot|woff2?$/i,
        type: 'asset/resource',
        generator: {
          filename: 'font/[name].[hash:6].[ext]',
        },
      },
      // ts 处理
      {
        test: /\.tsx$/,
        use: 'tsx-loader',
      },
    ],
  },

  // 插件
  plugins: [
    //自动生成index 文件
    new HtmlWebpackPlugin({
      title: '测试',
      template: './public/template.html',
      // filename:'login.html', // 默认index.html
    }),
    // 打包前自动自动删除之前打包的文件资源，（清空文件夹资源）
    new ClwanWebpackPlugin(),
    //全局变量
    new DefinePlugin({
      BASE_URL: '"./"',
    }),
    // 资源复制到打包的文件里
    new CopyWebpackPlugin({
      patterns: [
        {
          from: 'public', //复制的文件夹路径
          globOptions: {
            // 排除不需要复制的文件
            ignore: ['**/index.html', '**/.DS_Store'],
          },
        },
      ],
    }),
  ],
}
```

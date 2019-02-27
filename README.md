# Vue Webpack Simple
Build a vue webpack project from scratch.

## Project File Structure
```
vue-webpack-simple
|- asset
  |- logo.png
|- src
  |- App.vue
  |- main.js
|- index.html
|- package.json
|- webpack.config.js
```

## Create `package.json`
```
npm init -y
```
**package.json**
```
+ "private": true,  // prevent npm from publishing this repo
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
+   "build": "webpack"
  },
```

## Install Webpack
```
npm install -D webpack webpack-cli
```
**webpack.config.js**
```
module.exports = {
    mode: "development",
    devtool: "inline-source-map",
    entry: "./src/main.js",
    output: {
        path: path.resolve(__dirname, "dist"),
        filename: "[name].bundle.js"
    },
```

## Install `vue-loader`
```
npm install -D vue-loader vue-template-compiler
```
**webpack.config.js**
```
const VueLoaderPlugin = require('vue-loader/lib/plugin')

module.exports = {
  module: {
    rules: [
      // ... other rules
      {
        test: /\.vue$/,
        loader: 'vue-loader'
      }
    ]
  },
  plugins: [
    // make sure to include the plugin!
    new VueLoaderPlugin()
  ]
}
```

## Install `css-loader`
```
npm install -D vue-style-loader css-loader
```
**webpack.config.js**
```
      // this will apply to both plain `.css` files
      // AND `<style>` blocks in `.vue` files
      {
        test: /\.css$/,
        use: [
          'vue-style-loader',
          'css-loader'
        ]
      }
```

## Compose Source Code
Because we have `<img src="../asset/logo.png">` in `App.vue`, so we need a `file-loader` to handle 
it.
```
npm install -D file-loader
```
**webpack.config.js**
```
    {
      test: /\.(svg|png|jpg|gif)$/,
      use: 'file-loader'
    }
```

In `main.js`, we imported `vue`.
```
npm install --save vue
```
But beware of that `import App from './App.vue';` actually import `vue.runtime.js`, which does not 
have template compiler. `components: { 'app': App }` will not function. We can use `render` instead.  
Or assign `vue` to `vue.js` (`vue.js` = `vue.runtime.js` + `compiler.js`)
```
    resolve: {
        alias: {
            "vue$": 'vue/dist/vue.js'
        }
    }
```

Finally, we use `HtmlWebpackPlugin` to generate a entry html.

## Build Project
```
npm run build
```

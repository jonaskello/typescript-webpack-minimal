
# typescript-webpack-minimal
Mininal setup for using typescript with webpack

# How to use

```
yarn install
yarn start
# Open your browser to the url noted in output (usually localhost:8008)
```

# How to reproduce

The setup can be reproduced by running these commands:

```
mkdir typescript-webpack-minimal
cd typescript-webpack-minimal
yarn init -y
yarn add typescript webpack ts-loader webpack-dev-server
./node_modules/typescript/bin/tsc --init
```

Replace last `}` in package.json with:
```
  ,
  "scripts": {
    "start": "webpack-dev-server",
    "tsc": "tsc"
  }
}
```

Create webpack.config.js
```
var path = require("path");

module.exports = {
  entry: "./src/index.tsx",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname, "dist"),
    publicPath: "/dist/"
  },
  module: {
    rules: [
      { test: /\.tsx?$/, loader: "ts-loader" }
    ]
  },
  devServer: {
    stats: {
      assets: false,
      hash: false,
      chunks: false,
      errors: true,
      errorDetails: true,
    },
    overlay: true
  }
};
```

Create index.html
```
<html>
  <head>
    <title>typescript-webpack-minimal</title>
  </head>
  <body>
    <div id="root"></div>
    <script src="dist/bundle.js"></script>
  </body>
</html>
```

Create src/index.tsx
```
const x: number = 42;
const message: string = `Hello ${x}`;
document.getElementById("root").innerHTML = message;
```

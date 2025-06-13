# path

```js
const path = require("path");

console.log(__dirname); // /home/admin/LAB/Nodejs
console.log(__filename); // /home/admin/LAB/Nodejs/index.js

console.log(path.basename(__dirname)); // Nodejs
console.log(path.basename(__filename)); // index.js

console.log(path.extname(__dirname)); //
console.log(path.extname(__filename)); // .js

console.log(path.parse(__filename));
// {
//   root: '/',
//   dir: '/home/admin/LAB/Nodejs',
//   base: 'index.js',
//   ext: '.js',
//   name: 'index'
// }

console.log(path.format(path.parse(__filename)));
// /home/admin/LAB/Nodejs/index.js

console.log(path.isAbsolute(__filename));
// true

console.log(path.join("folder1", "folder2", "index.html"));
// folder1/folder2/index.html

console.log(path.resolve("folder1", "folder2", "index.html"));
// /folder1/folder2/index.html

console.log(path.join(__dirname,"data.json"));
// /home/thanush/LAB/Nodejs/data.json
```
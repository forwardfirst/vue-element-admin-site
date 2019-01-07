---
sidebarDepth: 3
---

# Clipboard

Here's the copy and paste based on [clipboard](https://github.com/zenorocha/clipboard.js)

This project provides two ways to use.

## Use directly

```markup
<el-button @click='handleCopy(inputData,$event)'>copy</el-button>
```

```javascript
import clip from '@/utils/clipboard.js' // use clipboard directly

methods: {
  handleCopy(text, event) {
    clip(text, event)
  }
}
```

First of all, import `clipboard.js` and set `click` function.

`clip()` The first parameter is the contents of the copy, the second parameter is the event event. Both parameters are required.

## v-directive

This project also encapsulates a `v-clipboard`.

```markup
 <el-button
   v-clipboard:copy='inputData'
   v-clipboard:success='clipboardSuccess'>
   copy
</el-button>
```

```javascript
import clipboard from '@/directive/clipboard/index.js' // use clipboard by v-directive

directives: {
  clipboard
},
methods: {
  clipboardSuccess() {
    this.$message({
      message: 'Copy successfully',
      type: 'success',
      duration: 1500
    })
  }
}
```

`v-clipboard:copy`: the copy of the content.

`v-clipboard:success`: success callback function.


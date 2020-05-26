```(javascript)
 /**
       * 判断内容是否超限
       * @param content 判断的内容
       * @param contentWidth 容器宽度
       * @param lineCount 内容行数
       * @param fontSize 字体大小
       * @returns {boolean}
       */
function isExtension (content, contentWidth, lineCount, fontSize) {
        let el = document.createElement('div')  // 创建一个临时div
        el.innerHTML = content
        el.style.whiteSpace = 'nowrap' // 不换行
        el.style.position = 'absolute'
        el.style.fontSize = `${fontSize}rem`;
        el.style.opacity = 0 // 完全透明
        document.body.appendChild(el)
        const elWidth = el.clientWidth  // 获取这个含有content内容的临时div的宽度
        console.log('width', lineCount, elWidth, contentWidth * lineCount, el)
        document.body.removeChild(el)
        return elWidth >= (contentWidth * lineCount - 5)   // 判断这个临时div的宽度是否大于原节点宽度的两倍
      },
```

```
/**
 * 是否是base64
 */
function isBase64(str) {
  return window.Base64.encode(window.Base64.decode(str)) === str;
};
```

```
// 选择文件
function selectFile (accept, change) {
  const fileInput = document.querySelector('#file-upload')
  // const fileInput = document.createElement('input');
  fileInput.accept = accept
  // fileInput.addEventListener('change', function () {
  //   change(this.files[0]);
  //   fileInput.value = '';
  // });
  // todo 后续优化
  fileInput.onchange = function (e) { // 兼容ie
    const file = e.target.files[0]
    if (!file) return
    change(file)
    fileInput.value = ''
    fileInput.parentNode.replaceChild(fileInput.cloneNode(), fileInput)
  }
  fileInput.click()
}
```

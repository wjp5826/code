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

```
// js中的大数相加
function sumString(a, b) {
  a = '0' + a;
  b = '0' + b;  //加'0'首先是为了转为字符串，而且两个数相加后可能需要进位，这样保证了和的长度就是a、b中长的那个字符的长度
  var arrA = a.split(''),  //将字符串转为数组
      arrB = b.split(''),
      res = [],  //相加结果组成的数组
      temp = '',  //相同位数相加的值
      carry = 0,  //同位数相加结果大于等于10时为1，否则为0
      distance = a.length - b.length,  //计算两个数字字符串的长度差
      len = distance > 0 ? a.length : b.length;  //和的长度
  // 在长度小的那个值前加distance个0，保证两个数相加之前长度是想等的
  if(distance > 0) {
    for(let i = 0; i < distance; i++) {
      arrB.unShift('0');
    }
  }else{
    for(let i = 0; i < distance; i++) {
      arrA.unShift('0');
    }
  }
  // 现在得到了两个长度一致的数组，需要做的就是把他们想通位数的值相加，大于等于10的要进一
  // 最终得到一个和组成的数组，将数组转为字符串，去掉前面多余的0就得到了最终的和
  for(let i = len-1; i >= 0; i--) {
    temp = Number(arrA[i]) + Number(arrB[i]) + carry;
    if(temp >= 10) {
      carry = 1;
      res.unshift((temp + '')[1])
    }
    else{
      carry = 0;
      res.unshift(temp)
    }
  }
  res = res.join('').replace(/^0/, '');
  console.log(res);
}

```

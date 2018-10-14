# clone
js对象深拷贝demo，测试用

```
function isObject (data) {
  return Object.prototype.toString.call(data) === '[object Object]'
}

function clone (obj) {
  const root = {}
  const tmp = [
    {
      parent: root,
      data: obj
    }
  ]
  let i = 0
  while (i < tmp.length) {
    const source = tmp[i++]
    const { data, parent } = source
    for (let o in data) {
      if (data.hasOwnProperty(o)) {
        if (isObject(data[o])) {
          const _cloned = tmp.find(source => source.data === data[o])
          if (_cloned) parent[o] = _cloned.parent
          else tmp.push({ parent: parent[o] = {}, data: data[o] })
        } else parent[o] = data[o]
      }
    }
  }
  return root
}

const a = { b: { a: { c: 1 } }, d: 8 }
a.a = a
a.b.b = a.b
const b = clone(a)
b.b.b.a = 1
b.a.d = 9
console.log(b)
console.log(a)
```

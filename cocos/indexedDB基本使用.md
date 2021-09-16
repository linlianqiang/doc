## indexedDB 介绍

[indexedBD简介](https://juejin.cn/post/6844903613240705038)

由于indexedDB操作过于繁琐，所以使用第三方封装好的 Dexie

```js
// 安装
npm install --save dexie
```

### 基本使用

#### 创建数据库

```js
import Dexie from 'dexie';
// 若数据库已存在则为打开
const db = new Dexie('lowcodeDB');
```

#### 创建表

```js
// 创建表名为 myTable 的表。默认版本为1.每次更新数据库，表都会更新。
// id自增，name,age *tags(复合索引)
db.version(1).stores({
  myTable: '++id,name,age,*tags'
});
```

#### 新增数据

```js
await db.friends.add({name: "cocos", age: 21});
//or
await db.friends.bulkAdd([
  {name: "Foo", age: 31},
  {name: "Bar", age: 32}
]);
```

#### 更新数据

```js
await db.friends.put({id: 4, name: "Foo", age: 33});
//or
await db.friends.bulkPut([
    {id: 4, name: "Foo2", age: 34},
    {id: 5, name: "Bar2", age: 44}
]);
await db.friends.update(4, {name: "Bar"});
```

#### 删除数据

```js
await db.friends.delete(4);
await db.friends.bulkDelete([1,2,4]);
```

#### 查询数据

```js
/**
 * 查询某个表数据
 * @param {string} table
 * @returns Promise
 */
const getTableData = async (table) => {
  const result = await db.open().then(result => {
    const res = result.table(table).toArray();
    return res;
  });
  return result;
};
```

#### 删除表

```javascript
db.delete();
```

#### 查询所有表

```js
db.tables
```


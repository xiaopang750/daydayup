## 背景

要跑刷千万条数据，需要通过图片地址把图片下载下来，然后传到腾讯云，再把图片地址刷回去。需要在1-2天内完成...

## 方案

- 开100个容器实例...
- 怎么map reduce
- 数据分片存储... like woker_1_200000 / woker_200000_400000，然后一张表维护一个task {taskId: 'woker_1_200000', status: 'init' }...
- 让多台容器实例取到不同的task, findOneAndUpdate吧...


## 实验

```
const getTask = col => new Promise((resolve, reject) => {
  col.findOneAndUpdate(
    { status: 'init' },
    { $set: { status: 'lock' } },
    (err, res) => {
      console.log(err, res)
      resolve()
    }
  )
})


const run = async() => {
  const { db } = await connectDb()
  const col = db.collection('test')
  let tasks = []
  for (let i = 0; i < 6; i +=1) {
    tasks.push(getTask(col))
  }
  await Promise.all(tasks)
}

run()

=> output

null { lastErrorObject: { updatedExisting: true, n: 1 },
  value: { _id: 5daa66de715619c16fe41126, taskId: '1', status: 'init' },
  ok: 1 }
null { lastErrorObject: { updatedExisting: true, n: 1 },
  value: { _id: 5daa66e6715619c16fe41128, taskId: '3', status: 'init' },
  ok: 1 }
null { lastErrorObject: { updatedExisting: true, n: 1 },
  value: { _id: 5daa66e4715619c16fe41127, taskId: '2', status: 'init' },
  ok: 1 }
null { lastErrorObject: { updatedExisting: true, n: 1 },
  value: { _id: 5daa66e9715619c16fe41129, taskId: '4', status: 'init' },
  ok: 1 }
null { lastErrorObject: { updatedExisting: true, n: 1 },
  value: { _id: 5daa66eb715619c16fe4112a, taskId: '5', status: 'init' },
  ok: 1 }
null { lastErrorObject: { updatedExisting: true, n: 1 },
  value: { _id: 5daa66ed715619c16fe4112b, taskId: '6', status: 'init' },
  ok: 1 }
```

哈哈说明取到了不同的task,但是不要高兴的太早...如果程序崩了，容器重启了status...没有重置回init怎么办...

容我再继续想想mapReduce...或者再找找开源方案...

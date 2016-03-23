title: mongodb-position
date: 2015-12-07 17:48:38
tags:
- mongodb
---
mongodb 数组插入数据位置
<!--more-->
~~~js
db.getCollection('Students').find({})

db.Students.insert({
    _id:1,
    scores:[1]
    });

db.Students.update(
   { _id: 1 },
   {
     $push: {
        scores: {
           $each: [ 99 ],
           $position: 1
        }
     }
   }
)
~~~

## ref

https://docs.mongodb.org/manual/reference/operator/update/position/#up._S_position


title: mongodb求和
date: 2015-09-30 11:31:18
tags:
- mongodb
---
mongodb求和
<!--more-->

[Aggregation](http://docs.mongodb.org/manual/core/aggregation-introduction/)

![](/../img/aggregation-pipeline.png)

~~~javascript
db.publicFoundation.aggregate([
    {
        $match:{acceptDate:{$ne:null}}
     },
     {
        $group:{'_id':null,"count":{'$sum':'$money'}},
     }
]);
~~~


----------


~~~java
DBObject match = new BasicDBObject();
		DBObject acceptDate = new BasicDBObject();			
		acceptDate.put("$ne", null);
		match.put("acceptDate", acceptDate);
		DBObject db = new BasicDBObject(new BasicDBObject("$match", match));
		DBObject object = new BasicDBObject();
		DBObject group = new BasicDBObject();
		object.put("_id", null);
		object.put("count", new BasicDBObject("$sum", "$money"));
		group.put("$group", object);
		AggregationOutput output = mongoTemplate.getCollection("publicFoundation").aggregate(db, group);
		Iterator iterator = output.results().iterator();
		DBObject redult = null;
		int totalMoney = 0;
		while (iterator.hasNext()) {
			redult = (DBObject) iterator.next();
			totalMoney = (int)redult.get("count");
		}
~~~

~~~js
db.mapReduce.insert([
    {name:"jay",age:20},
    {name:"mike",age:21}
]);
    
db.mapReduce.find();
    
db.mapReduce.mapReduce(
     function(){
        emit(this.age,this.age);
    },
    function(key,value){
        return Array.sum(value)
    },
    {
            //query:{age:},
            out:"age"
    }
    
); 
~~~   
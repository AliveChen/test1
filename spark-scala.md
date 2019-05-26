

```scala
// scala
```




    Name: Syntax Error.
    Message: 
    StackTrace: 




```scala
sc.master
```




    local



# join 


```scala
val nameDF = spark.read.json("file:/home/neo/name.json")
```


    nameDF = [gender: bigint, name: string]






    [gender: bigint, name: string]




```scala
val jsonArray = Array("{\"name\":\"lilei\",\"age\":18}",
                     "{\"name\":\"zhaohan\",\"age\":30}",
                     "{\"name\":\"jackma\",\"age\":50}")
val stuRDD = sc.parallelize(jsonArray,2)
val stuDF = spark.read.json(stuRDD)
nameDF.join(stuDF,"name").show()
```

    +-------+------+---+
    |   name|gender|age|
    +-------+------+---+
    |  lilei|     1| 18|
    |zhaohan|     2| 30|
    +-------+------+---+
    



    jsonArray = Array({"name":"lilei","age":18}, {"name":"zhaohan","age":30}, {"name":"jackma","age":50})
    stuRDD = ParallelCollectionRDD[34] at parallelize at <console>:38
    stuDF = [age: bigint, name: string]






    [age: bigint, name: string]




```scala
stuDF.show(5)
```

    +---+-------+
    |age|   name|
    +---+-------+
    | 18|  lilei|
    | 30|zhaohan|
    | 50| jackma|
    +---+-------+
    



```scala
val dataDF = nameDF.join(stuDF,nameDF("name")===stuDF("name"),"left")
```


    dataDF = [gender: bigint, name: string ... 2 more fields]






    [gender: bigint, name: string ... 2 more fields]




```scala
dataDF.filter("age>18").show()
```

    +------+-------+---+-------+
    |gender|   name|age|   name|
    +------+-------+---+-------+
    |     2|zhaohan| 30|zhaohan|
    +------+-------+---+-------+
    



```scala
dataDF.filter(dataDF("age")>18).show()
```

    +------+-------+---+-------+
    |gender|   name|age|   name|
    +------+-------+---+-------+
    |     2|zhaohan| 30|zhaohan|
    +------+-------+---+-------+
    



```scala
ataDF.filter(dataDF("age")>18).show()
```

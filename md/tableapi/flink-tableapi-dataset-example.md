# flink1.7.2 tableapi批处理示例

### DataSet 转换成table

```aidl

package com.opensourceteams.module.bigdata.flink.example.tableapi.convert.dataset

import org.apache.flink.api.scala.{ExecutionEnvironment, _}
import org.apache.flink.table.api.TableEnvironment
import org.apache.flink.table.api.scala._

object Run1 {


  def main(args: Array[String]): Unit = {

    val env = ExecutionEnvironment.getExecutionEnvironment
    val tableEnv = TableEnvironment.getTableEnvironment(env)

    val dataSet = env.fromElements( (1,"a",10),(2,"b",20), (3,"c",30) )



    //从dataset转化为 table
    val table = tableEnv.fromDataSet(dataSet)

    //注册table
    tableEnv.registerTable("user1",table)


    //查询table 所有数据
    tableEnv.scan("user1").first(10)

      //print 输出 (相当于sink)
      .print()


    /**
      * 输出结果
      * 
      * 1,a,10
      * 2,b,20
      * 3,c,30
      */



  }

}

```

- 输出结果

```aidl
1,a,10
2,b,20
3,c,30

```




### Scan 
- 功能描述: 查询表中所有数据
- scala 程序

```aidl

package com.opensourceteams.module.bigdata.flink.example.tableapi.operation.scan

import org.apache.flink.api.scala.{ExecutionEnvironment, _}
import org.apache.flink.table.api.TableEnvironment
import org.apache.flink.table.api.scala._

object Run {


  def main(args: Array[String]): Unit = {

    val env = ExecutionEnvironment.getExecutionEnvironment
    val tableEnv = TableEnvironment.getTableEnvironment(env)

    val dataSet = env.fromElements( (1,"a",10),(2,"b",20), (3,"c",30) )



    //从dataset转化为 table
    val table = tableEnv.fromDataSet(dataSet)

    //注册table
    tableEnv.registerTable("user1",table)


    //查询table 所有数据
    tableEnv.scan("user1").first(100)

      //print 输出 (相当于sink)
      .print()


    /**
      * 输出结果
      *
      * 1,a,10
      * 2,b,20
      * 3,c,30
      */



  }

}

```

- 输出结果

```aidl

1,a,10
2,b,20
3,c,30
```
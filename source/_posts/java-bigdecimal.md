title: JAVA BigDecimal
date: 2016-11-22 17:29:39
tags:
- java
---
JAVA BigDecimal
解决java计算精度问题
<!--more-->
~~~java
import java.math.BigDecimal;
import java.math.RoundingMode;
import java.text.DecimalFormat;

public class Test {

    public static void main(String[] arg) {

        BigDecimal num1 = new BigDecimal(2);
        BigDecimal num2 = new BigDecimal(3.003);
        BigDecimal result;
        BigDecimal big = new BigDecimal(100);

        System.out.println(big.add(BigDecimal.TEN));
        BigDecimal subtract = big.subtract(new BigDecimal(1.13));
        System.out.println(subtract.doubleValue());

        DecimalFormat df = new DecimalFormat("0.00");
        df.setRoundingMode(RoundingMode.DOWN);
        System.out.println(df.format(subtract));

        System.out.println(df.format(1.555));
        System.out.println(df.format(1.596));
        System.out.println(df.format(1.531));
        System.out.println(df.format(0));

        System.out.println(df.format(100));
        System.out.println(df.format('b'));

        // add
        BigDecimal addResult = num1.add(num2);
        System.out.println( df.format(addResult) );
        System.out.println( addResult.doubleValue() );

        System.out.println( num1.divide(num2,5,RoundingMode.HALF_UP) );

        result = num1.multiply(num2);
        System.out.println( df.format( result ) );

    }

}

~~~
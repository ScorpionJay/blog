title: java collection
date: 2015-08-20 16:57:42
tags:
- java
---

Java集合
<!--more-->

~~~java
package com.java.collection;
 
import java.util.ArrayList;
import java.util.Collection;
import java.util.HashMap;
import java.util.HashSet;
import java.util.List;
import java.util.Map;
import java.util.Set;
 
/**
 * @author Jay
 * @date   2015年8月6日
 */
public class CollectionDemo {
     
    public static void main(String[] args) {
        /**
         * Collection
         * 根接口
         * 方法：size isEmpty add
         * 重复 不重复 有序 无序
         */
        Collection c = new HashSet();
         
        /**
         * List
         * 接口 继承Collection
         * 允许重复 允许null
         */
        List list = new ArrayList();
         
        /**
         * Set
         * 接口 继承Collection
         * 不允许重复 允许null
         */
        Set set = new HashSet();
         
        /**
         * Map
         *
         */
        Map<String, String> map = new HashMap<String, String>();
         
         
        /**
         * linked 有顺序
         */
         
    }
}

~~~
---
title: Array Copy
commentable: true
Edit: 2023-2-21
mathjax: true
mermaid: true
tags: java
categories: Computer-Science
description: This is my learning shares of JAVA course given by Pr. Xiang sms, Nankai University, in 2023 Spring semester.
--- 

In last week's class, a funny issue was left by Pr.Xiang, consider and compare several array copy methods in JAVA. 

I am always interested in the questions like this. Cause I'm interested in the underlying performance of a programming language and love to make comparisons to see whether my approach is good or not.

In this post we will try four methods of array copying in JAVA: 

1. The `copyOf()` method of the `Arrays class`
2. The `copyOfRange()` method of the `Arrays class`
3. The `arraycopy()` method of the `System class`
4. The `clone()` method of the `Object class`

# `copyOf()` Method and `copyOfRange()` Method

Both methods can achieve array copying. 

However, the `copyOf()` method copies an array to a specified length. The `copyOfRange()` method copies the specified length of the specified array into a new array.

## Using `copyOf()` Method

The syntax of the copyOf() method of the Arrays class is as follows:

```java
 Arrays.copyOf(dataType[] srcArray,int length);
```

Where `srcArray` represents the array to be copied, and `length` represents the length of the new array after copying.

When copying an array using this method, the default copy starts from the first element of the original array (index value 0), and the length of the destination array will be length.

If `length` is greater than `srcArray.length`, the target array is filled with default values; if length is less than srcArray.length, it is copied to the length element (index value length-1).

**Notice**: <u>The target array will be refactored if it already exists.</u>

> __Example 1.1__
>
> Suppose you have 5 grades in an array, and now you need to save those 5 grades in a new array, leaving 3 spare elements for later development.
>
> The code to complete the array copy using the `CopyOf()` method of the `Arrays class` is as follows:

```java
 import java.util.Arrays;
 public class Test{
   public static void main(String[] args) {
       // 定义长度为 5 的数组
       int scores[] = new int[]{57,81,68,75,91};

       // 输出原数组
       System.out.println("原数组内容如下：");

       // 循环遍历原数组
       for(int i=0;i<scores.length;i++) {

       // 将数组元素输出
           System.out.print(scores[i]+"\t");
       }

       // 定义一个新的数组，将 scores 数组中的 5 个元素复制过来
       // 同时留 3 个内存空间供以后开发使用
       int[] newScores = (int[])Arrays.copyOf(scores,8);
       System.out.println("\n复制的新数组内容如下：");

       // 循环遍历复制后的新数组
       for(int j=0;j<newScores.length;j++) {
           // 将新数组的元素输出
           System.out.print(newScores[j]+"\t");
        }
    }
}
```

In the above code, since the length of the original array `scores` is 5, but the length of the new array `newScores` to be copied is 8, after the 5 elements in the original array are copied, the contents of the remaining 3 elements are filled with default values.

Because the data type of the original array `scores` is int, and the array is returned after copying the array using the `Arrays.copyOf(scores,8)` method, you need to cast the `Object[]` data type to `int[]` type. Also, because the data type of `scores` is int, the default value is 0.

The result of the run is shown below:

```markdown
原数组内容如下：
57    81    68    75    91   
复制的新数组内容如下：
57    81    68    75    91    0    0    0
```

## Using `copyOfRange()` Method

The `CopyOfRange()` method of the `Arrays class` is another way to copy an array with the following syntax:

```java
 Arrays.copyOfRange(dataType[] srcArray,int startIndex,int endIndex);
```

Thereinto:

- `srcArray` : the original array.

- `startIndex` : the starting index at which replication begins, the target array will contain the elements corresponding to the starting index, and the `startIndex` must be between 0 and `srcArray.length`.

- `endIndex` : the end index, the target array will not contain the elements corresponding to the end index, `endIndex` must be greater than or equal to `startIndex`, can be greater than `srcArray.length`, if greater than `srcArray.length`, the target array is populated with default values.

**Notice**: <u>The target array will be refactored if it already exists.</u>

> __Example 1.2__
>
> Suppose you have an array named `scores` with 8 elements, and now you need to define a new array named `newScores`. The elements of the new array are the first 5 elements of the `scores` array and do not change the order.
>
> The code to complete the array copy using the `copyOfRange()` method of the `Arrays class` is as follows:

```java
public class Test{
    public static void main(String[] args) {
        // 定义长度为8的数组
        int scores[] = new int[] { 57, 81, 68, 75, 91, 66, 75, 84 };
        System.out.println("原数组内容如下：");

        // 循环遍历原数组
        for (int i = 0; i < scores.length; i++) {
            System.out.print(scores[i] + "\t");
        }

        // 复制原数组的前5个元素到newScores数组中
        int newScores[] = (int[]) Arrays.copyOfRange(scores, 0, 5);
        System.out.println("\n复制的新数组内容如下：");

        // 循环遍历目标数组，即复制后的新数组
        for (int j = 0; j < newScores.length; j++) {
            System.out.print(newScores[j] + "\t");
        }
    }
}
```

In the above code, the original array scores contains 8 elements, use the `Arrays.copyOfRange()` method to copy the array into the `newScores` array of length 5, and intercept the first 5 elements of the `scores` array.

The result of the run is shown below:

```markdown
原数组内容如下：
57    81    68    75    91    66    75    84   
复制的新数组内容如下：
57    81    68    75    91
```

## Method source code

In fact, the underlying call method of the above two methods is `System.arraycopy`. 

So, these two methods can be considered the same method as `System.arraycopy`.

The following is the source code of `Arrays.copyOfRange` method:

```java
public static <T,U> T[] copyOfRange(U[] original, int from, int to, Class<? extends T[]> newType) {
        int newLength = to - from;
        if (newLength < 0)
            throw new IllegalArgumentException(from + " > " + to);
        T[] copy = ((Object)newType == (Object)Object[].class)
            ? (T[]) new Object[newLength]
            : (T[]) Array.newInstance(newType.getComponentType(), newLength);
        System.arraycopy(original, from, copy, 0, Math.min(original.length - from, newLength));
        return copy;
    }
```

Similarly, the following is the source code of `Arrays.copyOf` method:

```java
public static int[] copyOf(int[] original, int newLength) {
    int[] copy = new int[newLength];
    System.arraycopy(original, 0, copy, 0, Math.min(original.length, newLength));
    return copy;
}
```

# `arraycopy()` Method

The `arraycopy()` method is located in the `java.lang.System class` and has the following syntax:

```java
 System.arraycopy(dataType[] srcArray,int srcIndex,int destArray,int destIndex,int length);
```

Thereinto:

- `srcArray` : the original array;

- `destArray` : the target array; 

- `srcIndex` : the starting index in the original array; 

- `destIndex` : the starting index in the target array; 

- `length` : the length of the array to copy.

When copying an array using this method, `length+srcIndex` must be less than or equal to `srcArray.length`, and `length+destIndex` must be less than or equal to `destArray.length`.

**Note**: <u>The target array must already exist and not be reconstructed, equivalent to replacing some elements in the target array.</u>

> __Example 1.3__
>
> Suppose you have saved the grade information of 8 students in the `scores` array, and now you need to copy all the elements of the array from the second element to the end into an array named `newScores` with length 12. The elements in the `scores` array are arranged starting with the third element in the `newScores` array.
>
> The code that uses the `System.arraycopy()` method to complete the function of replacing array elements is as follows:

```java
public class Test{
    public static void main(String[] args) {
        // 定义原数组，长度为8
        int scores[] = new int[] { 100, 81, 68, 75, 91, 66, 75, 100 };

        // 定义目标数组
        int newScores[] = new int[] { 80, 82, 71, 92, 68, 71, 87, 88, 81, 79, 90, 77 };
        System.out.println("原数组中的内容如下：");

        // 遍历原数组
        for (int i = 0; i < scores.length; i++) {
            System.out.print(scores[i] + "\t");
        }
        System.out.println("\n目标数组中的内容如下：");

        // 遍历目标数组
        for (int j = 0; j < newScores.length; j++) {
            System.out.print(newScores[j] + "\t");
        }
        System.arraycopy(scores, 0, newScores, 2, 8);

        // 复制原数组中的一部分到目标数组中
        System.out.println("\n替换元素后的目标数组内容如下：");

        // 循环遍历替换后的数组
        for (int k = 0; k < newScores.length; k++) {
            System.out.print(newScores[k] + "\t");
        }
    }
}
```

In this program, you first define an array of `scores` with 8 elements, then define an array of `newScores` with 12 elements, and then use a for loop to iterate through the two arrays separately, outputting the elements in the array. Finally, use the `System.arraycopy()` method to replace the 8 elements in the `newScores` array starting from the third element and the next 8 elements in the `scores` array.

The result of the run is shown below:

```markdown
原数组中的内容如下：
100    81    68    75    91    66    75    100   
目标数组中的内容如下：
80    82    71    92    68    71    87    88    81    79    90    77   
替换元素后的目标数组内容如下：
80    82    100    81    68    75    91    66    75    100    90    77   
```

**Note**: <u>When using the</u> `arraycopy()` <u>method, be aware that the naming of this method goes against Java's naming conventions. That is, the first letter of the second word copy is not capitalized, but it should be written as arrayCopy by convention. Please pay attention to the writing of the method name when using this method.</u>

# `clone()` Method

The `clone()` method can also implement copying arrays. The method is a method in the class `Object` that creates an object with a separate memory space. Because an array is also an `Object` class, you can also copy an array using the `clone()` method of an array object.

The return value of the `clone()` method is of type `Object`, which is converted to the appropriate type using a cast type. Its grammatical form is relatively simple:

```java
 array_name.clone();
```

An example statement is as follows:

```java
 int[] targetArray=(int[])sourceArray.clone();
```

**Notice**: <u>The target array will be refactored if it already exists.</u>

> __Example 1.4__
>
> There is a `scores` array of length 8, because the program needs it, now to define an array named `newScores` to hold all the elements in the `scores` array, you can use the `clone()` method to copy all the elements in the `scores` array into the `newScores` array. The code is as follows:

```java
public class Test{
    public static void main(String[] args) {
        // 定义原数组，长度为8
        int scores[] = new int[] { 100, 81, 68, 75, 91, 66, 75, 100 };
        System.out.println("原数组中的内容如下：");

        // 遍历原数组
        for (int i = 0; i < scores.length; i++) {
            System.out.print(scores[i] + "\t");
        }

        // 复制数组，将Object类型强制转换为int[]类型
        int newScores[] = (int[]) scores.clone();
        System.out.println("\n目标数组内容如下：");

        // 循环遍历目标数组
        for (int k = 0; k < newScores.length; k++) {
            System.out.print(newScores[k] + "\t");
        }
    }
}
```

In the program, first define a `scores` array of length 8, loop through the elements in the output array, then define a new array named `newScores` and copy the elements in the `scores` array to the `newScores` array using the `scores.clone()` method. Finally, loop through the `newScores` array, outputting the array elements.

The result of the run is shown below:

```markdown
原数组中的内容如下：
100    81    68    75    91    66    75    100   
目标数组内容如下：
100    81    68    75    91    66    75    100   
```

As you can see from the results of the run, the elements of the `scores` array are the same as the elements of the `newScores` array.

# Comparison of the copy methods

In order to compare the above copying methods in Java with the performance of Java itself. We compare the efficiency by the program below.

```java
import java.util.Arrays;
import java.util.Date;

public class Array {
	public static final int size = 1000000;

	public static void copyByArrayCopy(String[] strArray){
		Long startTime = System.currentTimeMillis();
		String[] destArray = new String[size];
		System.arraycopy(strArray,0,destArray,0,strArray.length);
		//printArr(destArray);
		Long endTime = System.currentTimeMillis();
		System.out.println("copyByArrayCopy cost time is "+(endTime-startTime));
	}
	
	public static void copyByLoop(String[] strArray){
		Long startTime = System.currentTimeMillis();
		String[] destArray = new String[size];
		for(int i = 0;i<strArray.length;i++){
			destArray[i] = strArray[i];
		}
		//printArr(destArray);
		Long endTime = System.currentTimeMillis();
		System.out.println("copyByLoop cost time is "+(endTime-startTime));
	}
	
	public static void copyByClone(String[] strArray){
		Long startTime = System.currentTimeMillis();
		String[] destArray = strArray.clone();
		Long endTime = System.currentTimeMillis();
		System.out.println("copyByClone cost time is "+(endTime-startTime));
	}

	public static void main(String args[]){
		String arr1[] = new String[size];
		for(int i=0;i<size;i++){
			arr1[i] = "this is a test"+i;
		}
		String arr2[] = new String[size];
		for(int i=0;i<size;i++){
			arr2[i] = "this is a test"+i;
		}
		String arr3[] = new String[size];
		for(int i=0;i<size;i++){
			arr3[i] = "this is a test"+i;
		}
		copyByClone(arr1);
		copyByLoop(arr2);
		copyByArrayCopy(arr3);
		
	}
	public static void printArr(String[] strArray){
		for(String str:strArray){
			System.out.println(str);
		}
	}
}
```

The result of the run is shown below:

<img src="https://ssskz.github.io/about/java_arraycopy.png" width="100%">

It can be seen that the efficiency of `clone()` and `arraycopy()` is basically the same, while the efficiency of copying through loops is the worst.

Now let's look at the source code of `clone()` and `arraycopy()` again:

```java
protected native Object clone() throws CloneNotSupportedException;
```

```java
public static native void arraycopy(Object src,  int srcPos, Object dest, int destPos, int length);
```

You can see that both methods use the native method.

Simply put, a Native Method is an interface that Java calls non-Java code. A Native Method is a Java method whose implementation is implemented by a non-Java language, such as C. 

This feature is not unique to Java, but is found in many other programming languages, such as in C++, where you can use `extern "C"` to tell the C++ compiler to call a C function.

# Summary

1. In terms of speed: `System.arraycopy()` > `clone()` > `Arrays.copyOf()` > loop 
2. The reason why loop is the worst is that the subscript notation looks for the specified subscript every time from the starting point (modern compilers should optimize it for pointers), and it has to determine whether the maximum length of the array has been reached once and perform an additional addition operation to record the subscript value every time it loops. 
3. Looking at the source code of `Arrays.copyOf()`, you can see that it essentially calls `System.arraycopy()`. The reason why the time gap is large is because a large part of the overhead is spent on the `Math.min` function
4. Looking at the source code of `System.arraycopy()`, you can see that it is essentially calling local methods through Jni, and C/C++ has been compiled into machine code methods, so it is fast.
5. Java's performance is quite a hard job (no offence)!

------
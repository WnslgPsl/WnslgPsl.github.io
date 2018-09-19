---
layout: post
title: Kotlin 타입 별명(Type Alias)
date: 2018-09-19 13:44:20 +0300
description:
img: kotlin.png
tags: [Android, Kotlin, 타입별명, typealias]
---
## 타입 별명(Type Alias)

이미 존재하는 타입에 별명을 붙일 수 있다.

```kotlin
class PersonCharacteristic {

    fun getName() :String {
        return "Bob"
    }
}
```
<br>

```kotlin
typealias pc = PersonCharacteristic

fun main(args: Array<String>) {

    val person = pc()
    println(person.getName())

}
>>> Bob
```

당연히 기본 타입도 가능하다.
```kotlin
typealias Number = Int

fun main(args: Array<String>) {

    val a: Number = 10
    println(a)

}
>>> 10
```
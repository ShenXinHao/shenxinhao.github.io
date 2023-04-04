---
title: Metatable
categories:
 - Lua
---
## 官方解释

metatable允许我们改变table 的行为，例如，使用Metatable可以定义Lua如何计算两个table的相加操作。

我们可以使用setmetatable函数设置或者改变一个表的metatable。

```lua
t = {}
t1 = {}
setmetatable(t,t1)
assert(getmetatable(t) == t1)
```

任何一个表都可以是其他一个表的metatable，一组和相关的表可以共享一个metatable(描述他们共同的行为)。一个表也可以是自身的metatable。

---

## Metamethod（元方法）

我们可以设置table的元方法，使得他作为其他table的元表时，能够额外进行某些操作。

### 算术运算符

对于每一个算数运算符，metatable都有对应的域名与其对应，初此之外，我们还可以定义__concat定义连接行为。

例如，想要将两张table相加，那么至少需要其中一个有元表，且元表设置了元方法__add。

对于tableA + tableB 来说，Lua会去确认第一个参数tableA是否具有__add域(也就是设置了元方法__add)的metatable，如果有，则调用用tableA的元方法__add，和忽略第二个参数tableB的元方法。

如果第一个参数没有，则检查第二个参数，也就是tableB是否存在有__add域的metatable。

如果两个参数都没有，则Lua报错。

### 关系运算符

关系运算符不支持混合类型运算。对于混合类型比较运算的处理方法和Lua的公共行为类似，比较一个字符串和数字或者比较两个带有不同metamethod的表，Lua都会抛出错误。

但是相等比较从来不会抛出错误，如果两个表有不同的metamethod，比较的结果总为false，甚至可能不会调用metamethod，这也是模仿了Lua的公共行为，因为Lua总是认为字符串和数字是不相等的，而不判断他们的值。当仅当两个共同的metamethod的对象进行相等比较的时候，Lua才会调用对应的metamethod。

库定义的metamethods

在一些库中，在自己的 metatables 中定义自己的域是很普遍的情况。到目前为止，我们看到的所有 metamethods 都是 Lua 核心部分的。有虚拟机负责处理运算符涉及到的metatables 和为运算符定义操作的 metamethods。但是，metatable 是一个普通的表，任何人都可以使用。

tostring 是一个典型的例子。如前面我们所见，tostring 以简单的格式表示出 table：
print({}) --> table: 0x8062ac0
（注意：print 函数总是调用 tostring 来格式化它的输出）。然而当格式化一个表的时候，tostring 会首先检查表是否存在一个带有__tostring 域的 metatable。如果存在则以表作为参数调用对应的函数来完成格式化，返回的结果即为 tostring 的结果。

其他还有__metatable,设置之后，只能getmetatable，而不能重新设置。

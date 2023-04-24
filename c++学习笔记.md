# c++学习笔记

## 1.Template Functions

### 1.1 **generic C++**

C++ is strongly typed, but ==generic C++== lets you parametrize data types

==e.g. code==

```c++
template<typename T, typename U>
auto Min(T a, U b)
{
	return a > b ? b : a;
}
```

### 1.2 **Template Metaprogramming**（模板元编程）

Remember: like in template classes, **template functions** **are not compiled until used!**

● For each instantiation with different parameters（参数）, the compiler generates a new specific version of your template

● After compilation, it will look like you wrote each version yourself

**The code doesn’t exist until you instantiate it, which runs quicker.**

Can we take advantage of this behavior?

==e.g. code==

**TMP**使用的过程中，只编译一次，相当于递归的过程。大大地减少了运行时间。

Normally, code runs during **runtime**.

With template metaprogramming, code runs **once** during **compile time**!

```c++
template <int N>
struct Fibonacci 
{
  static const int value = Fibonacci<N-1>::value + Fibonacci<N-2>::value;
};

template <>
struct Fibonacci<0> 
{
  static const int value = 0;
};

template <>
struct Fibonacci<1> 
{
  static const int value = 1;
};

```

**TMP**用在不定量参数模板递归

```c++
template<typename T>
T sum(T t) {
  return t;
}

template<typename T, typename... Args>
T sum(T t, Args... args) {
  return t + sum(args...);
}

int result = sum(1, 2, 3, 4, 5);
```

TMP isn’t used that much, but it has some interesting implications:（**具体应用**）

● Optimizing matrices/trees/other mathematical structure operations

● Policy-based design

● Game graphics

==Advantages==

● Template functions allow you to parametrize（**参数化**） the type of a function to be anything without changing functionality

● Generic programming can solve a complicated conceptual（**概念性的**） problem for any specifics – powerful and flexible!

● Template code is instantiated at compile time; template metaprogramming takes advantage of this to run code at compile time

==By the way== : There are few universal, scientifically proven pieces of wisdom that will lead to a happier life:

1. Look both ways before crossing the street.
2. Never tell a pre-med you’re stressed.
3. When coding, never reinvent the wheel.

**That's why we need template!**

### 1.3 **Predicate Functions**（谓词函数）

UniPred is what’s called a **function pointer!**

● Function pointers can be treated just like other pointers

● They can be passed around like variables as parameters or in template functions!

● They can be called like functions!

==e.g. code== 

下面是一个简单的示例，其中定义了一个谓词函数 `is_odd`，用于测试一个整数是否为奇数

```c++
bool is_odd(int n) {
    return n % 2 == 1;
}

int main() {
    std::vector<int> nums = {1, 2, 3, 4, 5, 6, 7, 8, 9};
    auto odd_num = std::find_if(nums.begin(), nums.end(), is_odd);
    if (odd_num != nums.end()) {
        std::cout << "The first odd number is: " << *odd_num << std::endl;
    } else {
        std::cout << "No odd numbers found." << std::endl;
    }
    return 0;
}
```

### 1.4 Lambda Functions

We want our function to know more information about our predicate.

●However, we can’t pass in more than one parameter.

●How can we pass along information without needing another parameter?

Lambdas are **inline**, anonymous（**匿名的**） functions that can know about functions declared in their same scope!

```c++
[capture list] (parameter list) -> return type { function body }
```

You can capture any outside variable, both by reference and by value.

● Use just the **=** symbol to capture everything by value, and just the **&** symbol to capture everything by reference

![图片1](.\c++学习笔记src\图片1.png)

Lambdas are pretty computationally（**在计算上**） cheap and a great tool!

● Use a lambda when you need a short function or to access local variables in your function.

● If you need more logic or overloading, use function pointers.

![图片2](.\c++学习笔记src\图片2.png)

A **functor**（**仿函数**） is any class that provides an implementation of operator().

● They can create **closures** of  “customized” functions!

● Lambdas are just a reskin（**改头换面**） of functors!

![图片3](.\c++学习笔记src\图片3.png)

# OCaml 101

![image](https://user-images.githubusercontent.com/77828537/223425383-a7691a1d-1773-44a6-8290-bed3f7812284.png)

*Functional programming languages. OCaml is strong, static programming language*


- compile시 타입을 체크한다.

- 각 value, expression은 타입이 존재하고, implicit type casting을 하지 않는다.

- garbage-collected language이다. -> 자동으로 memory management를 해준다.

- 다중 패러다임 언어 (multi-paradigm language)이다. 

(일반적으로 value - object / immutable - mutable / pure - side-effect 중 좌측이 선호된다.)



## Value

OCaml은 value-oriented 언어라고 불린다.

Value: immutable , Object: mutable.

 OCaml 프로그램의 궁극적인 목표는 value를 계산하는 것.

- program은 old value를 사용해 new value를 생성해낸다.

- old object를 new object로 바꾸지는 않는다.


## Expressions

OCaml의 핵심 요소.

Imperative program -> command를 통해 프로그램을 build하지만,

Functional program -> expression을 통해 프로그램을 build한다.

expression은 computation을 통해 특정 값으로 evaluate / 혹은 exception을 일으키거나 / 종료되지 않는다.


### Arithmetic Expressions/Operators

- On Integers
```OCaml
1 + 2 - 3;;
1 * 2;;
1 / 2;;
1 mod 2;;
```

- On Floating point numbers
```OCaml
1.1 +. 2.1
1.1 -. 2.1
1.1 *. 2.1
1.1 /. 2.1
```

### Boolean Expressions/Operators

boolean value로 evaluate되는 expression.

```OCaml
true;; (* true *)
false;; (* false *)
1 + 1 > 2;; (* false *)
x = y;;
x <> y;;
x && y;;
x || y;;
```

## If Expressions

imperative language와는 다르게, if-then-else문이 statement가 아닌, **expression**이다

즉, if a then b else c 라고 했을때,
- a가 true이면 b로 evaluate
- a가 false이면 c로 evaluate
- 타입은 b와 c를 따라간다.

```OCaml
if 1 > 2 then 1 else 2;; (*- : int = 6*)
```

## Definition 

definition은 evaluated 되지 않는다.

```OCaml
let x = "test"
let _ = 1 + 1
```

## Function

### Definitions

```OCaml
# let add x = x + 1;;
val add : int -> int = <fun>

# increment 0;;
- : int = 1

# let rec fact n = (*recursive function def*)
  if n = 0 then 1 else n * fact (n-1)
val fact : int -> int = <fun>
```

### Anonymous Function
```OCaml
# fun x -> x - 1;;
-: int -> int = <fun>
```

### Function Application

- Application style
```OCaml
square (inc 5)
```

-Pipeline style
```OCaml
5 |> inc |> square
```

### Polymorphic Functions

Functions taking many types of values

```OCaml
# let id x = x;;
id : 'a -> 'a = <fun>
```
* 'a는 unknown type을 의미한다.

### Partial Application

function을 argument의 subset에 부분적으로 적용할 수 있다.

```OCaml
let add x y = x + y;;
let add5 = add 5;;
add5 2;; (* result: 7 *)
```

### Higher-order Functions

function을 argument로 가지는 function.

```OCaml
# let add_high f x = (f (x + 1)) + 2;;
val add_high : (int -> int) -> int -> int = <fun>
```

## Let-in expressions

Expressions with local binding.

```OCaml
# let x = 42 in x + 1
- : int = 43
```

```OCaml
let x = 5 in
 x
 +
 (let y = "3110" in
 int_of_string y)
```

## Lists

같은 타입을 가진 value들의 sequence.

```OCaml
# [1; 2; 3];;
- : int list = [1; 2; 3]
```

list를 build하는 두 가지 방법이 있다.

```OCaml
#[] (* nil, empty list를 의미한다.*)
- : 'a list

#1::[2; 3] (* cons를 사용하여 build할 수 있다.*)
- : int list [1; 2; 3]
```

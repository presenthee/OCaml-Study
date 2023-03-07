
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

즉, if a then b else c 라고 했을 때,
- a가 true이면 b로 evaluate된다.
- a가 false이면 c로 evaluate된다.
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

## Function Definitions 

```OCaml
# let add x = x + 1;;
val add : int -> int = <fun>
# increment 0;;
- : int = 1
# let rec fact n = (*recursive function def*)
  if n = 0 then 1 else n * fact (n-1)
val fact : int -> int = <fun>
```

### Anonymous function
```OCaml
# fun x -> x - 1;;
-: int -> int = <fun>
```






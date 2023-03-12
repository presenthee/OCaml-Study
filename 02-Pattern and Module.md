# Pattern Matching w. List

integer list의 합을 구하는 코드.

```OCaml
let rec sum list =
  match lst with
  | [] -> 0
  | h::t -> h + sum t
```

# Pattern Matching w. Tuple

tuple은 여러 타입의 값들로 이루어질 수 있다.

```OCaml
# (1, true, "hihi")
- : int * bool * string = (1, true, "hihi")
```

튜플타입의 패턴 매칭은 여러 방식으로 작성할 수 있다.

```OCaml
let pick t =
  match t with
  | (a, b, c) -> a

let pick t =
  let (a, b, c) = t in a
  
let pick t =
  let (_, _, c) = t in c
  
let pick (_, _, c) = c 
```

# Pattern Matching w. Records

딕셔너리, 객체(object in JS)처럼 key와 value를 가지는 타입.

tuple의 경우 요소들을 위치로 구분 가능하나 레코드는 이름(key)로 구분한다.

```OCaml
(* 타입을 정의한당*)
type person = { name: string; age: int };;

let presenthee: person = { name= "khh"; age: 24};;

presenthee.age;;
- : int = 24
```

레코드 또한 여러 방법으로 패턴 매칭을 작성할 수 있다.

```OCaml
let get_age p =
  match p with
  | { name=_; age=a } -> a

let get_age p =
  match p with
  | { age } -> age

let get_age p = p.age
```

# Pattern Matching w. Options

Option values explicitly indicate the presence or absence of a value.

즉, 값의 존재 여부를 명시적으로 나타내는 녀석. ~있거나 말거나~

Haskell에서의 monad, maybe 타입과 유사한 개념

## Syntax and semantics of options.

- t option is a type for every type t.
- None is a value of type 'a option.
- Some e is an expression of type t option if e : t. If e ==> v then Some e ==> Some v
- **None 또는 Some v**라는 값을 가질 수 있다. 
- OCaml 에는 null이 존재하지 않기 때문에, 대신 option을 통해 값이 존재하지 않음을 나타낼 수 있다.
- t option 타입은 t 타입의 값이 존재할 수도 있고, 아닐수도 있음을 나타낸다.
 
OCaml의 관점에서 보면 자바의 모든 object reference는 암시적인 옵션이다. reference에 값이 존재하거나, null 값을 가질 수 있기 때문이다. null이 nothing(None)을 대신한다.

null이 없다는 것은 프로그래머들에게 항상 값이 없을 경우(None) 핸들링을 할 것을 강제하는 셈이다.


```OCaml
# Some 42;;
- : int option = Some 42

# None;;
- : 'a option
```

option의 값은 패턴 매칭을 통해 접근 가능하다.

```OCaml
let rec list_max = function
  | []  -> None
  | h::t -> begin
    match list_max t with
      | None  -> Some h
      | Some m -> Some (max h m)
    end
```

begin...end는 nested pattern match를 감싸는 구문이다. (strict하게 필요한 것은 아니다.)

위 코드는 재귀적 코드인데, None을 리턴할 때까지 list_max가 call되고

그 이후는 head로 뽑힌(?) 원소들을 맨 끝부터 차례차례 max 함수로 비교하는 것을 알 수 있다.

결국 마지막 리턴 값은 Some (maximun_element)가 된다.

# Pattern Matching w. Variants

몇개의 가능한 선택지 중 하나를 나타내는 데이터 타입.

(A data type representing a value that is one of serveral possibilities.)

- C언어, Java에서의 enum과 유사한 개념.
- sum type의 일종: union or multiple sets
- variant 값들의 개별 이름들은 **constructor**라고 불린다

```OCaml
# type day = Sun | Mon | Tue | Wed | Thu | Fri | Sat;;

# let d = Tue;;
val d : day = Tue
```

```OCaml
let good_day d =
  match m with
  | Sun | Sat -> true
  | _ -> false
```

# Pattern Matching w. Exceptions

exception keyword로 exception type을 정의할 수 있다.

```OCaml
exception Division_by_zero

let rec div x y =
  | if y =0 then raise Division_by_zero
  else x / y
```

try를 이용해 pattern matching도 가능하다.

```OCaml
let r =
  try div x y with
  | Division_by_zero -> 0
  | Not_implemented -> -1
```

```OCaml
let r =
  match div x y with
  | n -> string_of_int n
  | Division_by_zero -> "Division by zero"
  | Not_implemented -> "Not implement"
```

## Constructors of variants

각 constructor는 argument를 가질 수 있다.

위에서 본 예시는 constructor당 한 개의 값을 가진 special case.

```OCaml
type shape =
  | Point of point
  | Circle of point * float
  | Rect of point * point
  
let rect1 = Rect (1.0, 5.7)
let circle1 = Circle ((0.6, 0.3), 50.5)

let area s =
  match s with
  | Point _ -> 0.0
  | Circle (_, r) -> pi *. (r ** 2.0)
  | Rect ((x1, y1), (x2, y2)) ->
    let w = x2 -. x1 in
    let h = y2 -. y1 in
    w *. h
```

## Recursive variants

```OCaml
(* lazy list *)
type intlist = Nil | Cons of int * intlist

let lst = Cons (3, Nil) (* 3:: [] *)
let lst123 = Cons (1, Cons(2, lst)) (* [1; 2; 3] *)
```

# Type Synonyms

```OCaml
type vector = float list
type point = float * float
```

# Unit

nothing을 의미하는 value이자 type.

- C언어, Java에서의 void와 유사한 개념.

```OCaml
# ();;
- : unit = ()
```

주로 print같은 side-effect only expression에서만 사용된다.
```OCaml
# print_endline;;
-: string -> unit = <fun>
```

# Modules

- C++, Java에서의 class와 유사한 개념.
- structure: sequence of definitions.

```Ocaml
module ListStack = struct
  let empty = []
  let is_empty s = (s = [])

  let push x s = x :: s

  let peek = function
    | [] -> failwith "Empty"
    | x::_ -> x

  let pop = function
    | [] -> failwith "Empty"
    | _::xs -> xs
end
```

사용시 `.` operator를 쓰면 된당.

```Ocaml
ListStack.empty 
```

# Module Type

- C++, Java에서의 interface와 유사한 개념.

```Ocaml
(* convention 때문에 보통 all capital letter를 사용한다.*)
module type STACK = sig
  type 'a t
  val empty    : 'a t
  val is_empty : 'a t -> bool
  val push     : 'a -> 'a t -> 'a t
  val peek     : 'a t -> 'a
  val pop      : 'a t -> 'a t
end

module ListStack : STACK = struct
  ...
end
```

# Functors

- A function from modules to modules.
- C++에서의 template, Java의 generic과 유사한 개념.

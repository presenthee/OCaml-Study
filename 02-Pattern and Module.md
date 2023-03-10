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

레코드? 딕셔너리, 객체(object in JS)처럼 key와 value를 가지는 타입.

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

즉, 값의 존재 여부를 명시적으로 나타내는 것. ~있거나 말거나~

# Type Synonyms

```OCaml
type vector = float list
type point = float * float
```

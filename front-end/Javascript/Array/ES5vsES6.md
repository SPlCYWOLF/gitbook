# ✨ ES5 vs ES6

[참조1](https://www.javatpoint.com/es5-vs-es6) ,   [참조2](https://hbsowo58.tistory.com/407) 

-----

## 1. Table comparison

- | -                    | ES5                                        | ES6                                                          |
  | -------------------- | ------------------------------------------ | ------------------------------------------------------------ |
  | **정의**             | ECMAScript의 5th 버전                      | ECMAScript의 6th 버전                                        |
  | **출시일**           | 2009년                                     | 2015년                                                       |
  | **지원 데이터 타입** | `string, number, boolean, null, undefined` | + `symbol`                                                   |
  | **변수선언 방법**    | `var`                                      | `let, const`                                                 |
  | **함수선언 방법**    | `function`과 `return` 키워드가 필수        | 화살표 함수를 활용하면 `function`과 `return` 키워드 생략 가능<br />`Destructuring` 활용 가능 |
  | **루프**             | `for, for .. in, while, do .. while`       | + `for .. of`                                                |
  | **문자열 관리**      | `'I am' + name`                            | ``I am ${name}``                                             |
  | **문자열 메서드**    | .`trim(), .charAt(i)`                      | + `.includes("string"), .startsWith("string"), .endsWith("string")` |
  | **비동기 통신**      | 콜백 함수 활용                             | 프로미스 활용                                                |

<br>

## 2. 요약

- ES5 업그레이드 버전이 ES6이다.
- `destructuring, arrow function, promise, template literal` 등으로 코드의 가독성이 올라갔다.
- 변수선언 방법의 개선, 다양한 `array & string`매서드의 추가로 코딩편의성이 개선되었다.
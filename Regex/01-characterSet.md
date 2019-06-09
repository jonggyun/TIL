# 정규식 정리 - character set

## character set

- /apple/

  제일 먼저 등장한 apple을 찾아낸다.

  ex) `apple` is apple.

  추가 적인 옵션이 없는 경우, 가장 먼저 해당하는 값을 찾는다.

- /apple/g

  apple를 전부다 찾아낸다.

  ex) `apple` is `apple`

  여기서 확인할 수 있는 것은 /g는 전체를 다 확인하는 `global`을 뜻하는 것을 알 수 있다.

- /[aeiou]/g

  ex) gl`i`b j`o`cks v`e`x dw`a`rv`e`s!

  []는 하나의 set를 만들어서 확인하는 역할을 한다.

  [aef]라는 set를 만들면 a, e, f 각자를 나타내는 set를 만드는 것이다.

  즉, 위의 예제는 a,e,i,o,u를 전부다 찾아내는(/g) 정규식이 된다.

- /[aeiou]/gi

  ex) gl`i`b j`o`cks v`e`x dw`a`rv`e`s!GL`I`B J`O`CKS V`E`X DW`A`RV`E`S!

  /i는 `case insensitive`를 뜻한다. 대소문자 구분하지 않게 된다.

- /[g-s]/g

  범위 검색을 할 때 사용한다. ASCII Code로 검색한다.

  https://ko.wikipedia.org/wiki/ASCII

  여기서도 g를 뺄 경우 g~s 사이에 글자 중 가장 먼저 발견되는 글자만 찾아낸다.

- /./g , /./, /\./

  .의 경우 메타문자이다. .를 단독으로 사용할 경우 \n\r를 제외한 문자 전부를 뜻한다.

  문자로써의 .를 찾아내기 위해선 escape를 사용하던가 (\\.) set를 뜻하는 괄호로 묶어서 사용([.])하면 된다.

- \s , \S

  \s는 whitespace를 뜻하고, \S는 whitespace를 제외한 것들을 뜻한다.

  - ex) /[\s]/g : 전체 중에 whitespace만 찾아낸다. 공백으로 값을 구분할 때 사용하면 유용하다.

    /[\s]/g는 /\s/g와 같다. 단일로 사용할 경우, set로 묶어서 사용하지 않아도 된다.

    'glib jocks vex dwarves!'.split(/[\s]/g)

    -> [ 'glib', 'jocks', 'vex', 'dwarves!' ]

  - ex) /[\^\s]/g : 전체 중에 whitespace만 찾는다. 위의 예제와 같다. set안에서의 ^가 Negated를 뜻하기 때문이다.

    'glib jocks vex dwarves!'.split(/[\^\s]/g)

    -> [ 'glib', 'jocks', 'vex', 'dwarves!' ]

  /[\s\S]/를 사용할 경우, 전부다를 표현하는 역할을 한다.

- \w, \W

  w는 word를 뜻한다. \w는 영숫자 및 언더바를 모두 찾아낸다. /\w/g는 /[a-zA-Z0-9_]/g와 같은 역할을 한다.

  \W는 영숫자 및 언더바를 제외한 다른 것들을 뜻한다. /\W/g는 /[\^a-za-z0-9_]/g와 같은 역할을 한다.

  ^는 set안에 있을 때 Negated의 역할을 한다. set 밖에 있을 경우엔 문자열의 시작과 일치하는 것을 찾는다.

  ex) /\W/g -> bonjour`,`mon fr`è`re

* \d, \D

  d는 digit을 뜻한다. \d는 0-9의 숫자를 뜻하게 된다. \D는 반대로 0-9의 숫자를 제외한 값을 뜻한다.

  사용자가 입력한 핸드폰 번호에서 -(dash)를 제외한 값을 구할 때 사용하면 편리하다.

  ex)

      '010-1234-1235'.replace(/\D/g, '') -> 01012341235

      '+82)02-1234-1294'.replace(/\D/g, '') -> 820212341294

      '010-1234-1235'.replace(/[\^\d]/g, '') -> 01012341235

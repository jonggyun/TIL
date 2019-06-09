# 정규식 정리 - anchor

## ^

^는 문자열의 시작 지점을 뜻한다. 시작 지점에서 일치하는 것만 나타낸다.

1. /^\w+/g : `she` sells seashells

2. /^\w/g : `s`he sells seashells

3. /^\d+/g: she sells seashells

예를 들면, 문자열의 시작이 숫자인 경우에만 적용하는 소스가 필요할 경우 등에 사용 가능!!

/\d/g.test('1st, she sells seashells') `true`

/\d/g.test('she sells seashells') `false`

## \$

\$는 문자열의 마지막 지점을 뜻한다. 마지막 지점에서 일치하는 내용을 뜻한다.

1. /\w+\$/g : she sells `seashells` , she sells `seashells12`

- w는 alphanumeric & undersocre라는 사실을 잊지말자!!

2. /\w\$/g : she sells seashell`s`

## \b, \B

공백 혹은 경계에서 원하는 내용을 찾을 때 사용한다. 여기서 공백은 맨 앞, 맨 뒤를 포함한다. 즉, 정확한 문자를 찾을 때 사용하면 된다.

1. /\bshe/g : `she` sells `she`seashells (앞 공백으로 she가 있는 경우)

2. /she\b/g : `she` sells seashells`she` (뒷 공백으로 she가 있는 경우)

3. /\bshe\b/g : `she` sells seashellsshe (양쪽 공백으로 she가 있는 경우)

   /she/g : `she` sells sea`she`lls`she` (she가 있는 경우)

4. /\Bshe/g : she sells sea`she`lls`she` (앞에 공백이 없이 she가 있는 경우)

5. /\Bshe\B/g : she sells sea`she`llsshe (양쪽에 공백 없이 she가 있는 경우. `문자열 내부에 존재하는지 파악할 때 사용`)

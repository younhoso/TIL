# next,prev 값 구하기

문제 설명
> 함수 solution에 인자로 배열이 들어가고 indexOf의 인자에 원하는 특정 원소의 위치를 탐색하여 반환되는 값
기준으로 앞,뒤 값을 구합니다.

입출력 예
|datas|indexOf|prev|next|
|---|---|---|
|[2,4,6,8,10]|6|4|8|

------------------------

문제 풀이 1
```javascript
function solution(datas){
	const current = datas.indexOf(3) //indexOf는 특정 원소의 위치를 탐색
	const next = (datas.length -1 !== current) ? (current + 1) % datas.length : null
	const prev = current - 1;

	console.log(datas[prevIndex])
	console.log(datas[nextIndex])
}
```
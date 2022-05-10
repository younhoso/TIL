# Flask Url Query
Flask에서 url의 query를 어떻게 받을것인가?
방법은 크게 2가지고 있습니다.

1번째 방법: flask에 내장되어 있는 `request`를 메소드를 사용하는 방법
```python
from flask import Flask, request #flask에 내장되어 있는 request를 메소드를 받아온다.

@app.route('/detail')
def detail():
	word_receive = request.args.get('word_give') #flask에 내장되어 있는 request를 메소드를 사용하는 방법
	return render_template("detail.html", rows=rows, word=word_receive) #detail.html에 word_receive를 word에 담아 보내주는 상황
```
브라우저 주소 입력란에 detail/?word_give=`hi`만 별도로 서버에 요청할수 있습니다. 
```
http://127.0.0.1:5000/detail/?word_give=hi
```

2번째 방법: `<keyword>`를 사용하는 방법
```python
@app.route('/detail/<keyword>')
def detail(keyword): #인자로 keyword를 받는다.
	word_receive = request.args.get('word_give')
	return render_template("detail.html", rows=rows, word=keyword) #keyword를 word에 담아 보내주는 상황
```
브라우저 주소 입력란에 /detail/`검색keyword`만 별도로 서버에 요청할수 있습니다. 
```
http://127.0.0.1:5000/detail/검색keyword
```
html에서 word라는 변수로 받아서 화면에 노출수있습니다.
```html
...
<h3>받은 단어는: {{word}}</h3>
...
```
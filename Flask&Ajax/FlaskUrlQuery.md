# Flask Url Query
Flask에서 url의 query를 어떻게 받을것인가?
방법은 크게 2가지고 있습니다.

1번째 방법: flask에 내장되어 있는 request를 메소드를 사용하는 방법
```python
from flask import Flask, request

@app.route('/detail')
def detail():
	word_receive = request.args.get('word_give') #flask에 내장되어 있는 request를 메소드를 사용하는 방법
	return render_template("detail.html", rows=rows, word=word_receive) #detail.html에 word_receive를 word에 담아 보내주는 상황
```
2번째 방법: `<keyword>`를 사용하는 방법
```python
@app.route('/detail/<keyword>')
def detail(keyword): #인자로 keyword를 받는다.
	word_receive = request.args.get('word_give')
	return render_template("detail.html", rows=rows, word=keyword) #keyword를 word에 담아 보내주는 상황
```
```html
...
<h3>받은 단어는: {{word}}</h3>
...
```
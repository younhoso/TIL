# new FormData
Ajax로 서버에 request를 보낼때 다음과 같이 `new FormData()`로 데이터들을 실어서 보냅니다.

```javascript
// index.js
function posting() {
		const title = $('#title').val();
		const content = $('#content').val();

		const file = $('#file')[0].files[0]
		const form_data = new FormData()

		form_data.append("file_give", file)
		form_data.append("title_give", title)
		form_data.append("content_give", content)

		$.ajax({
				type: "POST",
				url: "/diary",
				data: form_data,
				cache: false,
				contentType: false,
				processData: false,
				success: function(response){
						alert(response['msg'])
						window.location.reload()
				}
		})
};
```
```python
# app.py
from flask import Flask, render_template, jsonify, request
app = Flask(__name__)

from pymongo import MongoClient
client = MongoClient('localhost', 27017)
db = client.dbsparta_plus_week1

from datetime import datetime
```
서버에서는 다음과 같이 데이터를 받아서 DB에 저장합니다.
이미지 파일명 변경 및 저장하기 방법은 주석달아 놓은 부분을 참고하세요
```python
# app.py
@app.route('/diary', methods=['POST'])
def save_diary():
    title_receive = request.form['title_give']
    content_receive = request.form['content_give']
    file = request.files["file_give"]
    extension = file.filename.split('.')[-1] #맨 마지막에 있는 .점을 기준으로 파일 확장자명을 가져온다.

    today = datetime.now() #지금 시간때를 가져올수 있습니다.
    mytime = today.strftime('%Y-%m-%d-%H-%M-%S') #날짜시간을 문자열로 변환해서 변수에 할당
    filename = f'file-{mytime}' #날짜시간을 사용해서 파일명을 만들어준다.

    save_to = f'static/{filename}.{extension}' #경로와, 저장할 파일명을 만들어 변수에 할당
    file.save(save_to) #최종적으로 파일을 저장합니다.

    doc = {
        'title': title_receive,
        'content': content_receive,
        'file': f'{filename}.{extension}' #위에서 만든 파일명 추가합니다.
    }
    db.diary.insert_one(doc) #DB에 저장합니다.
    return jsonify({'msg': '저장 완료!'})
```
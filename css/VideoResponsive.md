# iframe 반응형
비디오(iframe) 컨텐츠를 16:9비율에 마쳐 반응형으로 만드는 방법을 알아봅시다.\
16:9비율의 계산식은 `9 / 16 * 100`입니다.
```css
/* 비디오 컨텐츠를 16:9비율에 마쳐 반응형으로 만들기 */
.video {position: relative; margin: 0 auto; max-width: 900px; width: 100%;}
.video > div{ width: 100%; padding-bottom: 56.25%;} /* padding-bottom 계산식 9 / 16 * 100 */
.video > div iframe{width: 100%; height: 100%; position: absolute; top: 0; left: 0; z-index: 1; }
```
```html
<div class="video">
		<div>
				<iframe src="https://www.youtube.com/embed/6lkLE3bSrMw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
		</div>
</div>
```
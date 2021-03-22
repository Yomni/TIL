---
description: 파파글 ( 파파고 + 구글 ) 번역 chrome extension
---

# Papagle

## 2개의 번역 API를 사용하는 chrome-extension 만들기

프로젝트 개요 : 평소 2개의 chrome - extension을 사용하고 있습니다.

1. 구글 번역 : [https://chrome.google.com/webstore/detail/google-translate/aapbdbdomjkkjkaonfhkkikfgjllcleb?hl=ko&](https://chrome.google.com/webstore/detail/google-translate/aapbdbdomjkkjkaonfhkkikfgjllcleb?hl=ko&)
2. 파파고 : [https://chrome.google.com/webstore/detail/papago-translate/enddgifdbfoefnelepppgaabobdfbcpe?hl=ko&](https://chrome.google.com/webstore/detail/papago-translate/enddgifdbfoefnelepppgaabobdfbcpe?hl=ko&)

경우에 따라, 구글 번역이나 파파고가 번갈아 가면서 의미 전달이 잘 되기 때문에 2개를 같이 사용하고 있습니다.  
이 2개를 한번의 요청으로 사용할 순 없을까? 하는 불편함에서 시작되었습니다.

> 항간에 떠도는 소문에 의하면 \[영어 --&gt; 한글\] 번역보다는 \[영어 --&gt; 일본어 --&gt; 한글\] 순의 번역이 더욱 더 잘 된다는 말이 있습니다. \(일본어 자료가 비교할 수 없을 정도로 많기 때문에...\)  
> 기회가 된다면 별도 기능으로 영어 --&gt; 일본어 --&gt; 한글 의 순으로 번역해주는 기능을 추가해도 재밌겠네요



시스템 설계도

사용하는 API


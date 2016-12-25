# 시크릿 키 없이 framer-Firebase 모듈 사용하기

### Motivation
현재 [framer-Firebase](https://github.com/marckrenn/framer-Firebase) 모듈은 
[secret key](https://github.com/marckrenn/framer-Firebase#1-properties)
를 필요로 하고 있습니다. 하지만 이 모듈을 이용한 프레이머 프로젝트를 클라우드에 업로드후 공개했을때 프레이머 특성상 코드가 모두
공개되고 secret key 도 어쩔수 없이 공개가 되어 업로드하기 꺼려지는게 아쉬웠습니다. 그래서 소량 코드의 모듈 수정과 파이어베이스 권한
수정으로 secret key 없이도 파이어베이스 사용이 가능하다는걸 공유해드립니다.

### How to do
> framer-Firebase 모듈에 적혀진 [README](https://github.com/marckrenn/framer-Firebase/blob/master/README.md)
를 읽어보시지 않았다면 이해가 어려울수 있으니 먼저 읽어보신후 진행하시는걸 권장합니다.
 
1. 제가 수정한 [파이어 베이스 모듈](https://github.com/ochanje210/framer-Firebase-without-secret/archive/master.zip) 을 다운로드후
압축을 풉니다.
2. `firebase.coffee` 파일을 프레이머 윈도우에 드래그하거나 프레이머 프로젝트 폴더안에 있는 `modules` 안에 넣습니다.
3. https://firebase.google.com 로 가셔서 로그인후 새 프로젝트를 만들거나 기존에 존재하는 프레이머에 사용할 원하는 프로젝트에 들어갑니다.
4. 아래와 같이 Database -> RULES 로 갑니다.
![gif](http://i.giphy.com/3o6ZsWUPVMtKzh5UQ0.gif)
5. `.read` 와 `.write` 에 `auth != null` 를 `true` 로 변경하거나 혹은 아래와 같이 변경합니다.
```json
{
  "rules": {
    ".read": "true",
    ".write": "true"
  }
}
```
이 작업은 secret key 없이도 데이타베이스에 데이타를 가져오거나 수정하는것을 허락하는 것입니다.
6. 준비는 모두 끝났고, 기존에 사용하시던 방법에서 아래의 예제처럼 secret key 만 빼면 됩니다.

 
```coffeescript
firebase = new Firebase
	projectID: "<project id>" 
	#secret: "<your secret key>" 기존에 필요했던 이 secret 을 지워주세요
	server: "<your project id>.firebaseio.com"
```

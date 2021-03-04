---
title: DUNI Open API Reference | DUNU 오픈 API 설명서

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - php
  - javascript
  - python

toc_footers:
  - <div class="fb-like" data-href="https://www.facebook.com/386832955100142" data-width="100" data-layout="button_count" data-action="like" data-size="small" data-show-faces="false" data-share="false"></div>
  - <a href='https://pilot.duni.io/'>DUNI 파일럿 센터</a>
  - <a href='https://developer.duni.io/'>DUNI 개발자</a>
  - <a href='https://code.duni.io/'>DUNI 코드</a>
  - <a href='https://duni.io/'>DUNI 중개 서비스</a>
  - <a href='https://www.facebook.com/DuniPilotPage/'>DUNI 파일럿 페이스북</a>
  - <a href='https://groups.google.com/forum/#!forum/droneplay2018'>개발관련 문의게시판</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>
  - © <script>var cYear=(new Date()).getFullYear();document.write(cYear);</script> APLY Inc.
includes:
  - errors

search: true
---

# 소개

'Drone, Everywhere'

이곳은 드론 소프트웨어 개발자분들을 위한 DUNI Open API사용법과 예제코드를 제공하는 사이트입니다.


# Token 발급 받기

> Open API 사용을 위해 DUNI 개발자 Token을 발급 받으세요.


```shell

```

```php

```

```javascript

```

```python

```


>

DUNI Open API는 DUNI 개발자 Token을 파라메터로 입력해야 사용하실 수 있습니다.
개발자 Token은 아래의 DUNI 파일럿 센터에 가입후 받으실 수 있습니다.

[DUNI 파일럿 센터](https://pilot.duni.io/center).

또는, "가입하기" API를 통해 Token을 발급 받을 수 있습니다.


#가입 및 로그인/자동로그인/로그아웃

##가입하기

```shell

curl -H "Content-type: application/json" -X POST -d '{"action":"member", "daction":"register", "socialid" : "EMAILADDRESS1", "phone_number" : "USER_PHONE_NUMBER", "name" : "USER_NAME", "sns_token" : "SNS_ID_TOKEN", "sns_kind" : "SNS_KIND"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'member';
$body['daction'] = 'register';
$body['socialid'] = 'EMAILADDRESS1';
$body['phone_number'] = "USER_PHONE_NUMBER";
$body['name'] = "USER_NAME";
$body['sns_token'] = "SNS_ID_TOKEN";
$body['sns_kind'] = "SNS_KIND";

$headers = array(
        'Content-Type: application/json'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action":"member", "daction":"register", "socialid" : "EMAILADDRESS1", "phone_number" : "USER_PHONE_NUMBER", "name" : "USER_NAME", "sns_token" : "SNS_ID_TOKEN", "sns_kind" : "SNS_KIND"};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           alert("Successfully, recorded.");
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json'
}
data = {
    'action' : 'member',
    'daction' : 'register',
    'socialid' : 'EMAILADDRESS1',
    'phone_number' : 'USER_PHONE_NUMBER',
    'name' : 'USER_NAME',
    'sns_kind' : 'SNS_KIND',
    'sns_token' : 'SNS_ID_TOKEN'
}
url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result": "success",
    "token": "USER_TOKEN"
  }
```

> 오류 발생시

```json
  {
    "result": "failed",
    "reason": "failed to get user data blah ..."
  }
```

전화번호와 이메일주소 그리고 이름을 입력 받아 회원을 등록합니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
action | 'member'을 입력합니다.
daction | 'register'를 입력합니다.
name | 가입자명을 입력합니다.
sns_kind | facebook, naver, apple, kakao, google 중 하나를 입력합니다.
sns_token | sns 로그인 후 받은 id token 값을 입력합니다.
phone_number | 가입자의 전화번호를 입력합니다.
socialid | 가입자의 이메일주소를 입력합니다.



##로그인

```shell

curl -H "Content-type: application/json" -X POST -d '{"action":"member", "daction":"login", "sns_token" : "SNS_ID_TOKEN", "sns_kind" : "SNS_KIND"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'member';
$body['daction'] = 'login';
$body['sns_token'] = "SNS_ID_TOKEN";
$body['sns_kind'] = "SNS_KIND";

$headers = array(
        'Content-Type: application/json'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action":"member", "daction":"login", "sns_token" : "SNS_ID_TOKEN", "sns_kind" : "SNS_KIND"};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           alert("Successfully, recorded.");
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json'
}
data = {
    'action' : 'member',
    'daction' : 'login',
    'sns_kind' : 'SNS_KIND',
    'sns_token' : 'SNS_ID_TOKEN'
}
url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result": "success",
    "token": "USER_TOKEN",
    "emailid": "duni@aply.biz",
    "socialid" : "123456789@snssiteaddress.com"
  }
```

> 오류 발생시

```json
  {
    "result": "failed",
    "reason": "failed to get user data blah ..."
  }
```

SNS의 종류와 SNS ID TOKEN으로 로그인합니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
action | 'member'을 입력합니다.
daction | 'login'을 입력합니다.
sns_kind | facebook, naver, apple, kakao, google 중 하나를 입력합니다.
sns_token | sns 로그인 후 받은 id token 값을 입력합니다.
device_kind | 푸시알림을 받을 기기의 종류를 입력합니다. ios, android 중 하나를 입력합니다. 그 외의 디바이스일 경우 입력하지 않으셔도 됩니다. (Optional)
device_id | 푸시알림을 받을 기기의 푸시토큰을 입력합니다. (Optional)



##자동로그인

```shell

curl -H "Content-type: application/json" -X POST -d '{"action":"member", "daction":"autologin", "device_id" : "DEVICE_ID"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'member';
$body['daction'] = 'autologin';
$body['clientid'] = 'EMAILID'
$body['device_id'] = "DEVICE_ID";

$headers = array(
        'Content-Type: application/json'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action":"member", "daction":"autologin", "clientid" : "EMAILID", "device_id" : "DEVICE_ID"};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           alert("Successfully, recorded.");
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json'
}
data = {
    'action' : 'member',
    'daction' : 'autologin',
    'clientid' : 'EMAILID',
    'device_id' : 'DEVICE_ID'
}
url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result": "success"
  }
```

> 오류 발생시

```json
  {
    "result": "failed",
    "reason": "failed to get user data blah ..."
  }
```

ios/android 기기에서 자동 로그인시에 푸시토큰 갱신을 위해 사용합니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
action | 'member'을 입력합니다.
daction | 'autologin'을 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
device_id | 푸시알림을 받을 기기의 푸시토큰을 입력합니다.


##로그아웃

```shell

curl -H "Content-type: application/json" -X POST -d '{"action":"member", "daction":"logout"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'member';
$body['clientid'] = 'EMAILID';
$body['daction'] = 'logout';

$headers = array(
        'Content-Type: application/json'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action":"member", "daction":"logout", "clientid":"EMAILID"};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           alert("Successfully, recorded.");
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json'
}
data = {
    'action' : 'member',
    'daction' : 'logout',
    'clientid' : 'EMAILID'
}
url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result": "success"
  }
```

> 오류 발생시

```json
  {
    "result": "failed",
    "reason": "failed to get user data blah ..."
  }
```

ios/android 기기로 푸시알림을 받지 않기 위해 사용합니다..

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
action | 'member'을 입력합니다.
daction | 'logout'을 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.


# 드론의 현재위치 저장/불러오기

## 1개 드론의 현재위치 저장/공유


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"set", "lat" : 12.134132, "lng" : 12.1324, "alt" : 5, "yaw":10, "pitch" : 10, "roll": 10, "act" : 0, "kind" : "drone", "dsec" : 1}' https://api.duni.io/v1/

```

```php

/* 1개 드론위치 보내기 */
$body['action'] = 'position';
$body['daction'] = 'set';
$body['clientid'] = 'EMAILID';
$body['lat'] = 12.134132;
$body['lng'] = 12.1324;
$body['alt'] = 5;
$body['act'] = 0;
$body['yaw'] = 15;
$body['pitch'] = 10;
$body['roll'] = 10;
$body['kind'] = 'drone';
$body['dsec'] = 10;

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;

```

```javascript

var jdata = {"action":"position", "daction": "set", "clientid" : "EMAILID", "lat" : 12.134132, "lng" : 12.1324, "alt" : 5, "yaw":10, "pitch" : 10, "roll": 10, "act" : 0, "kind" : "drone", "dsec" : 0};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           alert("Successfully, recorded.");
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action' : 'position',
    'daction' : 'set',
    'clientid' : 'EMAILID'
    'lat' : 12.134132,
    'lng' : 12.1324,
    'alt' : 5.2,
    'dsec' : 1,
    'yaw' :10,
    'pitch' : 10,
    'roll' : 10,
    'kind' : 'drone',
    'act' : 0
}
url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result": "success"
  }
```

드론의 현재 위치와 정보를 저장하고 공유합니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'set'을 입력합니다. / 위치를 다른이에게 공유할 경우 'set_share' 입력 : 'targets' 파라메터 필수
lat | latitude 좌표값를 입력합니다. (double)
lng | longitude 좌표값를 입력합니다. (double)
alt | 고도값을 입력합니다. (double, 미터)
act | 해당위치에서 수행한 행동 (개발자 임의 정의 가능, int)
yaw | 기체의 yaw 값 입력 (double, degree, Optional)
pitch | 기체의 pitch 값 입력 (double, degree, Optional)
roll | 기체의 roll 값 입력 (double, degree, Optional)
dsec | 영상 녹화시 현재 시각부터 녹화 시각의 차 : 초 (int, Optional)
kind | object의 이름 (Optional, ex: 'drone')
targets | 공유하고자 하는 대상의 emailid 값 배열 ('daction' 파라메터 참고, '사용자 clientid 불러오기 API' 참고, 공유대상 수 10개 이하 제한)


## 1개 이상 드론의 현재위치 저장/공유


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"set", "objects" : [ {"lat" : 12.134132, "lng" : 12.1324, "alt" : 5, "yaw":10, "pitch" : 10, "roll": 10, "act" : 0, "kind": "drone", "dsec" : 1}, {"lat" : 12.134132, "lng" : 12.1344, "alt" : 5, "yaw":10, "pitch" : 10, "roll": 10, "act" : 0, "kind": "people", "dsec" : 1} ] }' https://api.duni.io/v1/

```

```php

/* 1개 드론위치 보내기 */
$body['action'] = 'position';
$body['daction'] = 'set';
$body['clientid'] = 'EMAILID';
$body['objects'] = array();
$objects['lat'] = 12.134132;
$objects['lng'] = 12.1324;
$objects['alt'] = 5;
$objects['act'] = 0;
$objects['yaw'] = 15;
$objects['pitch'] = 10;
$objects['roll'] = 10;
$objects['kind'] = 'drone';
$objects['dsec'] = 10;
array_push($body['objects'], $objects);

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;

```

```javascript


var objects = [];
objects.push({"lat" : 12.134132, "lng" : 12.1324, "alt" : 5, "yaw":10, "pitch" : 10, "roll": 10, "act" : 0, "kind" : "drone", "dsec" : 0});
var jdata = {"action":"position", "daction": "set", "clientid" : "EMAILID", "objects" : objects};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           alert("Successfully, recorded.");
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}

objects = [{
    'lat' : 12.134132,
    'lng' : 12.1324,
    'alt' : 5.2,
    'dsec' : 1,
    "yaw":10,
    "pitch" : 10,
    "roll" : 10,
    "kind" : "drone",
    "act" : 0
}]

data = {
    'action': 'position',
    'daction': 'set',
    'clientid' : 'EMAILID'
    'objects' : objects
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result": "success"
  }
```

1개 이상의 드론이나 객체의 현재 위치와 정보를 저장하고 공유합니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'set'을 입력합니다. 위치를 다른이에게도 공유할 경우 'set_share' (입력시 'targets' 파라메터 필수)
objects | 여러 드론의 위치를 보낼때 사용하는 배열 (array, 아래 objects 배열 참고, 5개 이하 제한)
targets | 공유하고자 하는 대상의 emailid 값 배열 ('daction' 파라메터 참고, '사용자 clientid 불러오기 API' 참고, 10개 이하 제한)

### objects 배열

파라메터 | 설명
--------- | -----------
lat | latitude 좌표값를 입력합니다. (double)
lng | longitude 좌표값를 입력합니다. (double)
alt | 고도값을 입력합니다. (double, 미터)
act | 해당위치에서 수행한 행동 (개발자 임의 정의 가능, int)
yaw | 기체의 yaw 값 입력 (double, degree, Optional)
pitch | 기체의 pitch 값 입력 (double, degree, Optional)
roll | 기체의 roll 값 입력 (double, degree, Optional)
kind | object의 이름 (Optional, ex: 'drone')
dsec | 영상 녹화시 현재 시각부터 녹화 시각의 차 : 초(int, Optional)
<aside class="warning">
objects : [
  {
    "lat" : 123.12,
    "lng" : 31.12,
    "alt" : 11.6,
    "yaw" : 120.2,
    "pitch" : 10.5,
    "roll" : 21.1,
    "kind" : "drone",
    "dsec" : 123
  },
  {
    "lat" : 123.12,
    "lng" : 31.12,
    "alt" : 11.6,
    "yaw" : 120.2,
    "pitch" : 10.5,
    "roll" : 21.1,
    "kind" : "drone",
    "dsec" : 123
  }
]
</aside>


## 드론의 최근 위치 읽어오기

```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"get"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'position';
$body['daction'] = 'get';
$body['clientid'] = 'EMAILID';

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;

```

```javascript


var jdata = {"action": "position", "daction": "get", "clientid" : "EMAILID" };

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'position'
    'daction': 'get',
    'clientid' : 'EMAILID'
}
url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()


```
> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
{
  "result" : "success",
  "data" :
   {
     "dtimestamp" : 1518536680763,
     "lat" : 37.2435813,
     "lng" : 131.8661992,
     "alt" : 1.2,
     "yaw" : 10,
     "roll" : 10,
     "pitch" : 10.1,
     "act" : 0
   }
}

//또는, 1개 이상의 드론이 객체가 공유되고 있을 경우 아래와 같이 응답

{
  "result" : "success",
  "owner" : "emailaddress",
  "data" :
   {
     "objects" : [
      {
         "lat" : 37.2435813,
         "lng" : 131.8661992,
         "alt" : 1.2,
         "yaw" : 10,
         "roll" : 10,
         "pitch" : 10.1,
         "act" : 0
       },
       {
          "lat" : 37.2435813,
          "lng" : 131.8661992,
          "alt" : 1.2,
          "yaw" : 10,
          "roll" : 10,
          "pitch" : 10.1,
          "act" : 0
       }
    ]
   }
}

```
<aside class="warning">dtimestamp는 GMT+0 기준입니다. 서울기준이 아닙니다.</aside>

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
action | 'position'을 입력합니다.
daction | 'get'을 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.


# 비행계획 저장/불러오기

## 비행계획 저장


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"mission", "daction":"set", "mname" : "MISSIONNAME", "speed" : 1, "missiondata" : [{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"act":1,"actparam":1,"id":"mission-1"},{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"act":1,"actparam":1,"id":"mission-2"}]}' https://api.duni.io/v1/

```

```php

$body['action'] = 'mission';
$body['daction'] = 'set';
$body['clientid'] = 'EMAILID';
$body['mname'] = "MISSIONNAME";
$body['speed'] = 1;
$body['missiondata'] = json_decode('[{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"act":1,"actparam":1,"id":"mission-1"},{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"act":1,"actparam":1,"id":"mission-2"}]');

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"clientid":"EMAILID", "action":"mission", "daction":"set", "mname" : "MISSIONNAME", "speed" : 1, "missiondata" : [{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"act":1,"actparam":1,"id":"mission-1"},{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"act":1,"actparam":1,"id":"mission-2"}];

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'mission',
    'daction': 'set',
    'clientid' : 'EMAILID'
    "mname" : "MISSIONNAME",
    "speed" : 1,
    "missiondata" : [{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"act":1,"actparam":1,"id":"mission-1"},{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"act":1,"actparam":1,"id":"mission-2"]
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result": "success"
  }
```

DUNI 파일럿 센터에 비행계획을 저장합니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'mission'을 입력합니다.
daction | 'set'을 입력합니다.
mname | 비행계획의 이름을 입력합니다.
speed | 비행 속도를 입력합니다. (m/s, double)
missiondata | 비행계획 데이터를 입력합니다.

### missiondata : 비행계획 데이터 구조
[{lat:latitude, lng:longitude, alt:altitude, act:action, actparam:actionparam, speed:speed, id:mission-id}]

파라메터 | 설명
--------- | -----------
lat | 위도 (double)
lng | 경도 (double)
alt | 고도 (double, 미터)
act | 해당위치에서 드론이 수행할 행동 (int, DJI기준, 또는 개발자 임의 정의)
actparam | action 에 대한 파라메터
speed | 비행 속도(m/s)를 입력합니다. (double : Deprecated)
id | 비행계획의 고유 아이디 (부여한 비행계획 이름의 범위내에서 고유한 아이디, 개발자 임의입력 가능)

### act, action param 값 참고 (DJI 기준)
액션 | act 값
--------- | -----------
STAY|0
START_TAKE_PHOTO|1
START_RECORD|2
STOP_RECORD|3
ROTATE_AIRCRAFT|4
GIMBAL_PITCH|5

[DJI사의 WayPoint Action 값을 참고해 주세요](https://developer.dji.com/api-reference/android-api/Components/Missions/DJIWaypoint_DJIWaypointAction.html#djiwaypoint_djiwaypointactiontype_inline).


## 비행계획 목록 불러오기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"mission", "daction":"get"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'mission';
$body['daction'] = 'get';
$body['clientid'] = 'EMAILID';

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "mission", "daction": "get", "clientid" : "EMAILID"};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'mission',
    'daction': 'get',
    'clientid' : 'EMAILID'
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success",
    "data":[
          {
          "regtime":"Sun Dec 30 2018 13:11:39 GMT+0000 (UTC)",
          "mission":[
              {"alt":3,"lng":131.86471756082,"act":0,"id":"mission-1","lat":37.243835988516,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86645915266,"act":0,"id":"mission-2","lat":37.244423805175,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86671844684,"act":0,"id":"mission-3","lat":37.243568918929,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86493079644,"act":0,"id":"mission-4","lat":37.243182141771,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86491855886,"act":0,"id":"mission-5","lat":37.243758419995,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86492249835,"act":0,"id":"mission-6","lat":37.243906083699,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86492249835,"act":0,"id":"mission-7","lat":37.243903981846,"actparam":1, "speed":10}
            ],
          "name":"MISSIONNAME",
          "clientid":"EMAILID",
          "speed" : 1
      },

      {
          "regtime":"Sun Dec 30 2018 13:11:39 GMT+0000 (UTC)",
          "mission":[
              {"alt":3,"lng":131.86471756082,"act":0,"id":"mission-1","lat":37.243835988516,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86645915266,"act":0,"id":"mission-2","lat":37.244423805175,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86671844684,"act":0,"id":"mission-3","lat":37.243568918929,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86493079644,"act":0,"id":"mission-4","lat":37.243182141771,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86491855886,"act":0,"id":"mission-5","lat":37.243758419995,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86492249835,"act":0,"id":"mission-6","lat":37.243906083699,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86492249835,"act":0,"id":"mission-7","lat":37.243903981846,"actparam":1, "speed":10}
            ],
          "name":"MISSIONNAME_2",
          "clientid":"EMAILID",
          "speed" : 1
      }
    ],
    "morekey" : "<some value>"
  }
```
DUNI 파일럿 센터의 비행계획 목록 10개를 불러옵니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'mission'을 입력합니다.
daction | 'get'을 입력합니다.
morekey | 이전에 받은 morekey 값을 입력하면 다음 10개의 목록을 가져 옵니다. (Optional)


## 비행계획 1개 불러오기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"mission", "daction":"get", "mname" : "MISSIONNAME_1"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'mission';
$body['daction'] = 'get';
$body['clientid'] = 'EMAILID';
$body['mname'] = 'MISSIONNAME_1';

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "mission", "daction": "get", "clientid" : "EMAILID", "mname" : "MISSIONNAME_1"};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'mission',
    'daction': 'get',
    'mname' : 'MISSIONNAME_1',
    'clientid' : 'EMAILID'
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success",
      "data" : {
          "regtime":"Sun Dec 30 2018 13:11:39 GMT+0000 (UTC)",
          "mission":[
              {"alt":3,"lng":131.86471756082,"act":0,"id":"mission-1","lat":37.243835988516,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86645915266,"act":0,"id":"mission-2","lat":37.244423805175,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86671844684,"act":0,"id":"mission-3","lat":37.243568918929,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86493079644,"act":0,"id":"mission-4","lat":37.243182141771,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86491855886,"act":0,"id":"mission-5","lat":37.243758419995,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86492249835,"act":0,"id":"mission-6","lat":37.243906083699,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86492249835,"act":0,"id":"mission-7","lat":37.243903981846,"actparam":1, "speed":10}
            ],
          "name":"MISSIONNAME_1",
          "clientid":"EMAILID",
          "speed" : 1
      }
```
DUNI 파일럿 센터의 비행계획 1개를 불러옵니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'mission'을 입력합니다.
daction | 'get'을 입력합니다.
mname | 비행계획의 이름을 입력합니다.

## 비행계획 검색하기

```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"mission", "daction":"find_mission", "keyword" : "JEJU"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'mission';
$body['daction'] = 'find_mission';
$body['clientid'] = 'EMAILID';
$body['keyword'] = 'JEJU';

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "mission", "daction": "find_mission", "clientid" : "EMAILID", "keyword" : "JEJU"};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'mission',
    'daction': 'find_mission',
    'clientid' : 'EMAILID',
    'keyword' : 'JEJU'
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success",
    "data":[
          {
          "regtime":"Sun Dec 30 2018 13:11:39 GMT+0000 (UTC)",
          "mission":[
              {"alt":3,"lng":131.86471756082,"act":0,"id":"mission-1","lat":37.243835988516,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86645915266,"act":0,"id":"mission-2","lat":37.244423805175,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86671844684,"act":0,"id":"mission-3","lat":37.243568918929,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86493079644,"act":0,"id":"mission-4","lat":37.243182141771,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86491855886,"act":0,"id":"mission-5","lat":37.243758419995,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86492249835,"act":0,"id":"mission-6","lat":37.243906083699,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86492249835,"act":0,"id":"mission-7","lat":37.243903981846,"actparam":1, "speed":10}
            ],
          "name":"MISSIONNAME",
          "clientid":"EMAILID",
          "speed" : 1
      },

      {
          "regtime":"Sun Dec 30 2018 13:11:39 GMT+0000 (UTC)",
          "mission":[
              {"alt":3,"lng":131.86471756082,"act":0,"id":"mission-1","lat":37.243835988516,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86645915266,"act":0,"id":"mission-2","lat":37.244423805175,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86671844684,"act":0,"id":"mission-3","lat":37.243568918929,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86493079644,"act":0,"id":"mission-4","lat":37.243182141771,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86491855886,"act":0,"id":"mission-5","lat":37.243758419995,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86492249835,"act":0,"id":"mission-6","lat":37.243906083699,"actparam":1, "speed":10},
              {"alt":3,"lng":131.86492249835,"act":0,"id":"mission-7","lat":37.243903981846,"actparam":1, "speed":10}
            ],
          "name":"MISSIONNAME_2",
          "clientid":"EMAILID",
          "speed" : 1
      }
    ],
    "morekey" : "<some value>"
  }
```

제목에 검색어를 포함하는 비행계획 목록을 10개씩 불러옵니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'mission'을 입력합니다.
daction | 'find_mission'을 입력합니다.
keyword | 검색어를 입력합니다.
morekey | 이전에 받은 morekey 값을 입력하면 다음 10개의 목록을 가져 옵니다. (Optional)



## 비행계획 삭제하기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"mission", "daction":"delete", "mname":"MISSIONNAME"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'mission';
$body['daction'] = 'delete';
$body['clientid'] = 'EMAILID';
$body['mname'] = "MISSIONNAME";

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action":"mission", "daction": "delete", "clientid" : "EMAILID", "mname" : "MISSIONNAME"};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'mission',
    'daction': 'delete',
    'clientid' : 'EMAILID',
    'mname' : 'MISSIONNAME'
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success"
  }
```
DUNI 파일럿 센터의 비행계획 1개를 삭제합니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'mission' 입력합니다.
daction | 'delete' 입력합니다.
mname | 삭제할 비행계획의 이름을 입력합니다.




# 비행기록 저장/불러오기

## 비행기록 저장


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"upload", "name" : "FLIGHTRECORDNAME", "memo": "MEMO", "data" : [{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"yaw" : 10, "pitch" : 10, "roll" : 10,"act":1,"actparam":1,"id":"rec-1", "youtube_data_id":"https://wwww.youtube.com/watch?v=ABCDE", "dtimestamp" : 1569903583000},{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"yaw" : 10, "pitch" : 10, "roll" : 10,"act":1,"actparam":1,"id":"rec-2", "dtimestamp" : 1569903584000}]}' https://api.duni.io/v1/

```

```php

$body['action'] = 'position';
$body['daction'] = 'upload';
$body['clientid'] = 'EMAILID';
$body['name'] = "FLIGHTRECORDNAME";
$body['memo'] = "MEMO";
$body['youtube_data_id'] = "https://wwww.youtube.com/watch?v=ABCDE";
$body['data'] = json_decode('[{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"yaw" : 10, "pitch" : 10, "roll" : 10,"act":1,"actparam":1,"id":"rec-1", "dtimestamp" : 1569903583000},{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"yaw" : 10, "pitch" : 10, "roll" : 10,"act":1,"actparam":1,"id":"rec-2", "dtimestamp" : 1569903584000}]');

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"clientid":"EMAILID", "action":"position", "daction":"upload", "name" : "FLIGHTRECORDNAME", "memo" : "MEMO", "youtube_data_id" : "https://wwww.youtube.com/watch?v=ABCDE", "data" :[{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0, "yaw" : 10, "pitch" : 10, "roll" : 10, act":1,"actparam":1,"id":"rec-1", "dtimestamp" : 1569903583000},{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0, "yaw" : 10, "pitch" : 10, "roll" : 10,"act":1,"actparam":1,"id":"rec-2", "dtimestamp" : 1569903584000}]};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'position',
    'daction': 'upload',
    'clientid' : 'EMAILID'
    "name" : "FLIGHTRECORDNAME",
    "memo" : "MEMO",
    "youtube_data_id" : "https://wwww.youtube.com/watch?v=ABCDE",
    "data" : [{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0, "yaw" : 10, "pitch" : 10, "roll" : 10, "act":1,"actparam":1,"id":"rec-1", "dtimestamp" : 1569903583000},{"lat":12.134132,"lng": 12.1324 ,"alt":5,"speed":0, "yaw" : 10, "pitch" : 10, "roll" : 10, "act":1,"actparam":1,"id":"rec-2", "dtimestamp" : 1569903583000}]
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result": "success"
  }
```

DUNI 파일럿 센터에 비행기록을 저장합니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'upload'를 입력합니다.
name | 비행기록 이름을 입력합니다.
memo | 메모를 입력합니다.
youtube_data_id | 비행영상의 유튜브 주소를 입력합니다. (ex: https://wwww.youtube.com/watch?v=ABCDE, Optional)
data | 비행기록 목록을 입력합니다.

### data 파라메터 포멧
[{lat:latitude, lng:longitude, alt:altitude, act:action, actparam:actionparam, speed:speed, dsec:time, yaw:yaw, pitch:pitch, roll:roll, id:rec-id, dtimestamp:timestamp}]

파라메터 | 설명
--------- | -----------
lat | 위도
lng | 경도
alt | 고도 (double, 미터)
speed | 속도 (double, 미터/s)
roll | roll 각도(Degree)
pitch | pitch 각도(Degree)
yaw | yaw 각도(Degree)
dsec | 녹화시작후 시간값 (milli second)
act | 해당위치에서 드론이 수행한 행동 (DJI기준, 또는 개발자 임의 정의, Optional)
actparam | action 에 대한 파라메터 (Optional)
id | 비행계획의 고유 아이디 (부여한 비행계획 이름의 범위내에서 고유한 아이디, 개발자 임의입력 가능, Optional)
dtimestamp | 기록시점의 timestamp (13자리)

### act, action param 값 참고 (DJI 기준)
액션 | act 값
--------- | -----------
STAY|0
START_TAKE_PHOTO|1
START_RECORD|2
STOP_RECORD|3
ROTATE_AIRCRAFT|4
GIMBAL_PITCH|5

[DJI사의 WayPoint Action 값을 참고해 주세요](https://developer.dji.com/api-reference/android-api/Components/Missions/DJIWaypoint_DJIWaypointAction.html#djiwaypoint_djiwaypointactiontype_inline).


## 비행기록 목록 불러오기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"download"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'position';
$body['daction'] = 'download';
$body['clientid'] = 'EMAILID';

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "position", "daction": "download", "clientid" : "EMAILID"};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'position',
    'daction': 'download',
    'clientid' : 'EMAILID'
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success",
    "data":[
          {
          "regtime":"Sun Dec 30 2018 13:11:39 GMT+0000 (UTC)",
          "name":"RECNAME_1",
          "clientid":"EMAILID",
          "flat" : 127.122,
          "flng" : 37.1122,
          "youtube_data_id" : "https://wwww.youtube.com/watch?v=ABCDE",
          "memo" : "MYMEMO"
      },

      {
          "regtime":"Sun Dec 30 2018 13:11:39 GMT+0000 (UTC)",
          "name":"RECNAME_2",
          "clientid":"EMAILID",
          "flat" : 127.122,
          "flng" : 37.1122,
          "youtube_data_id" : "https://wwww.youtube.com/watch?v=ABCDE",
          "memo" : "MYMEMO",
      }
    ],
    "morekey" : "<some value>"
  }
```

비행기록을 10개씩 불러옵니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'download'을 입력합니다.
public | 공개 비행기록을 원할 경우 true, 개인 비행기록을 원할 경우 false를 입력합니다. (기본값: false, Optional)
owner_email | 회원의 이메일을 입력합니다. 해당 회원의 공개 비행기록을 가지고 옵니다. 'public' 값이 true 이어야 합니다. (Optional)
morekey | 이전에 받은 morekey 값을 입력하면 다음 10개의 목록을 가져 옵니다. (Optional)




## 상세 비행기록 불러오기

```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"download_spe", "name": "FLIGHTRECORDNAME"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'position';
$body['daction'] = 'download_spe';
$body['name'] = 'FLIGHTRECORDNAME';
$body['clientid'] = 'EMAILID';

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "position", "daction": "download_spe", "clientid" : "EMAILID", 'name': 'FLIGHTRECORDNAME'};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'position',
    'daction': 'download_spe',
    'name': 'FLIGHTRECORDNAME',
    'clientid' : 'EMAILID'
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success",
    "data":[
          {
          "regtime":"Sun Dec 30 2018 13:11:39 GMT+0000 (UTC)",
          "data":[
              {"alt":3,"lng":131.86471756082,"act":0,"id":"rec-1","lat":37.243835988516,"actparam":1, "speed":10, "yaw" : 10, "roll" : 10, "pitch" : 10, "dsec" : 0, "dtimestamp" : 1234567890111},
              {"alt":3,"lng":131.86645915266,"act":0,"id":"rec-2","lat":37.244423805175,"actparam":1, "speed":10, "yaw" : 10, "roll" : 10, "pitch" : 10, "dsec" : 1, "dtimestamp" : 1234567891111},
              {"alt":3,"lng":131.86671844684,"act":0,"id":"rec-3","lat":37.243568918929,"actparam":1, "speed":10, "yaw" : 10, "roll" : 10, "pitch" : 10, "dsec" : 2, "dtimestamp" : 1234567892111},
              {"alt":3,"lng":131.86493079644,"act":0,"id":"rec-4","lat":37.243182141771,"actparam":1, "speed":10, "yaw" : 10, "roll" : 10, "pitch" : 10, "dsec" : 3, "dtimestamp" : 1234567893111},
              {"alt":3,"lng":131.86491855886,"act":0,"id":"rec-5","lat":37.243758419995,"actparam":1, "speed":10, "yaw" : 10, "roll" : 10, "pitch" : 10, "dsec" : 4, "dtimestamp" : 1234567894111},
              {"alt":3,"lng":131.86492249835,"act":0,"id":"rec-6","lat":37.243906083699,"actparam":1, "speed":10, "yaw" : 10, "roll" : 10, "pitch" : 10, "dsec" : 5, "dtimestamp" : 1234567895111},
              {"alt":3,"lng":131.86492249835,"act":0,"id":"rec-7","lat":37.243903981846,"actparam":1, "speed":10, "yaw" : 10, "roll" : 10, "pitch" : 10, "dsec" : 6, "dtimestamp" : 1234567896111}
            ],
          "name":"RECORDNAME",
          "clientid":"EMAILID",
          "flat" : 37.243835988516, //대표 좌표
          "flng" : 131.86471756082, //대표 좌표
          "memo" : "MYMEMO"
      }
    ]
  }
```

지정한 비행기록 이름의 상세 비행기록 1개를 불러옵니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'download_spe'을 입력합니다.
public | 공개 비행기록일 경우 'true', 개인 비행기록일 경우 'false'를 입력합니다. (기본값: 'false', Optional)
name | 비행기록 이름을 입력합니다.


## 비행기록 검색하기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"find_record", "keyworkd":"JEJU"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'position';
$body['daction'] = 'find_record';
$body['clientid'] = 'EMAILID';
$body['keyword'] = 'JEJU';

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "position", "daction": "find_record", "clientid" : "EMAILID", "keyword" : "JEJU"};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'position',
    'daction': 'find_record',
    'clientid' : 'EMAILID',
    'keyword' : 'JEJU'
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success",
    "data":[
          {
          "regtime":"Sun Dec 30 2018 13:11:39 GMT+0000 (UTC)",
          "name":"RECNAME_1",
          "clientid":"EMAILID",
          "flat" : 127.122,
          "flng" : 37.1122,
          "youtube_data_id" : "https://wwww.youtube.com/watch?v=ABCDE",
          "memo" : "MYMEMO"
      },

      {
          "regtime":"Sun Dec 30 2018 13:11:39 GMT+0000 (UTC)",
          "name":"RECNAME_2",
          "clientid":"EMAILID",
          "flat" : 127.122,
          "flng" : 37.1122,
          "youtube_data_id" : "https://wwww.youtube.com/watch?v=ABCDE",
          "memo" : "MYMEMO",
      }
    ],
    "morekey" : "<some value>"
  }
```

제목과 주소에 검색어를 포함하는 비행기록 목록을 10개씩 불러옵니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'find_record'을 입력합니다.
keyword | 검색어를 입력합니다.
public | 공개 비행기록에서 검색을 원할 경우 'true', 개인 비행기록에서 검색을 원할 경우 'false'를 입력합니다. (기본값: 'false', Optional)
morekey | 이전에 받은 morekey 값을 입력하면 다음 10개의 목록을 가져 옵니다. (Optional)


## 주소로 비행기록 검색하기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"media_by_address", "address" : "제주시 조천읍 두니리 000-1"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'position';
$body['daction'] = 'media_by_address';
$body['clientid'] = 'EMAILID';
$body['address'] = '제주시 조천읍 두니리 000-1';

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "position", "daction": "media_by_address", "clientid" : "EMAILID", "address" : "제주시 조천읍 두니리 000-1"};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'position',
    'daction': 'media_by_address',
    'clientid' : 'EMAILID',
    'address' : '제주시 조천읍 두니리 000-1'
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success",
    "data":[
          {
          "regtime":"Sun Dec 30 2018 13:11:39 GMT+0000 (UTC)",
          "name":"RECNAME_1",
          "clientid":"EMAILID",
          "flat" : 127.122,
          "flng" : 37.1122,
          "memo" : "MYMEMO",
          "youtube_data_id" : "https://wwww.youtube.com/watch?v=ABCDE"
      },

      {
          "regtime":"Sun Dec 30 2018 13:11:39 GMT+0000 (UTC)",
          "name":"RECNAME_2",
          "clientid":"EMAILID",
          "flat" : 127.122,
          "flng" : 37.1122,
          "memo" : "MYMEMO",
          "youtube_data_id" : "https://wwww.youtube.com/watch?v=ABCDE"
      }
    ],
    "morekey" : "<some value>"
  }
```

요청한 주소 근처의 비행기록을 검색하고 결과를 10개씩 응답 합니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'media_by_address'을 입력합니다.
address | 정확한 주소(번지까지)를 입력합니다.
public | 공개 비행기록에서 검색을 원할 경우 'true', 개인 비행기록에서 검색을 원할 경우 'false'를 입력합니다. (기본값: 'false', Optional)
morekey | 이전에 받은 morekey 값을 입력하면 다음 10개의 목록을 가져 옵니다. (Optional)



## GPS좌표로 비행기록 검색하기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"media", "lat":33.1232, "lng":121.11}' https://api.duni.io/v1/

```

```php

$body['action'] = 'position';
$body['daction'] = 'media';
$body['clientid'] = 'EMAILID';
$body['lat'] = 33.1232;
$body['lng'] = 33.1232;

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "position", "daction": "media", "clientid" : "EMAILID", "lat" : 33.123, "lng" : 123.11};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'position',
    'daction': 'media',
    'clientid' : 'EMAILID',
    'lat' : 33.123,
    'lng' : 123.121
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success",
    "data":[
          {
          "regtime":"Sun Dec 30 2018 13:11:39 GMT+0000 (UTC)",
          "name":"RECNAME_1",
          "clientid":"EMAILID",
          "flat" : 127.122,
          "flng" : 37.1122,
          "memo" : "MYMEMO",
          "youtube_data_id" : "https://wwww.youtube.com/watch?v=ABCDE"
      },

      {
          "regtime":"Sun Dec 30 2018 13:11:39 GMT+0000 (UTC)",
          "name":"RECNAME_2",
          "clientid":"EMAILID",
          "flat" : 127.122,
          "flng" : 37.1122,
          "memo" : "MYMEMO",
          "youtube_data_id" : "https://wwww.youtube.com/watch?v=ABCDE"
      }
    ],
    "morekey" : "<some value>"
  }
```

요청한 GPS 좌표 근처의 비행기록을 검색하고 결과를 10개씩 응답합니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'media'을 입력합니다.
lat | 위도
lng | 경도
public | 공개 비행기록에서 검색을 원할 경우 'true', 개인 비행기록에서 검색을 원할 경우 'false'를 입력합니다. (기본값: 'false', Optional)
morekey | 이전에 받은 morekey 값을 입력하면 다음 10개의 목록을 가져 옵니다. (Optional)


## 비행기록 삭제하기

```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"delete", "name":"FLIGHTRECORDNAME"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'position';
$body['daction'] = 'delete';
$body['clientid'] = 'EMAILID';
$body['name'] = "FLIGHTRECORDNAME";

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action":"position", "daction": "delete", "clientid" : "EMAILID", "name" : "FLIGHTRECORDNAME"};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'position',
    'daction': 'delete',
    'clientid' : 'EMAILID',
    'mname' : 'MISSIONNAME'
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success"
  }
```

비행기록 1개를 삭제합니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position' 입력합니다.
daction | 'delete' 입력합니다.
name | 삭제할 비행기록의 이름을 입력합니다.



# 비행기록 업로드

## DJI 비행기록 파일 업로드 하기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"convert", "reocordfile":"BASE64_ENCODED_DJI_FLIGHTRECORD_FILE"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'position';
$body['daction'] = 'convert';
$body['clientid'] = 'EMAILID';
$body['reocordfile'] = 'BASE64_ENCODED_DJI_FLIGHTRECORD_FILE';

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "position", "daction": "convert", "clientid" : "EMAILID", "reocordfile":"BASE64_ENCODED_DJI_FLIGHTRECORD_FILE"};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'position',
    'daction': 'convert',
    'clientid' : 'EMAILID',
    'reocordfile' : 'BASE64_ENCODED_DJI_FLIGHTRECORD_FILE'
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success"
  }
```

DJI 비행기록 파일을 분석하여 비행기록으로 저장합니다.
저장한 비행기록 파일은 비행기록 목록에서 확인할 수 있습니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'convert'을 입력합니다.
recordfile | Base64로 인코딩된 DJI Flight Record File 입니다. (포멧. "파일정보,Base64 Encoded Text")
youtube_data_id | 유튜브 URL을 입력합니다. ex) https://youtube.com/watch?v=k12hadf (Optional)

DJI Flight Record file 위치:
<a href=https://forum.dji.com/thread-98213-1-1.html>https://forum.dji.com/thread-98213-1-1.html</a>


## DUNI 비행기록 파일 업로드 하기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"duni_file_upload", "reocordfile":"BASE64_ENCODED_DUNI_FLIGHTRECORD_FILE"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'position';
$body['daction'] = 'duni_file_upload';
$body['clientid'] = 'EMAILID';
$body['reocordfile'] = 'BASE64_ENCODED_DUNI_FLIGHTRECORD_FILE';

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "position", "daction": "duni_file_upload", "clientid" : "EMAILID", "reocordfile":"BASE64_ENCODED_DUNI_FLIGHTRECORD_FILE"};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'position',
    'daction': 'duni_file_upload',
    'clientid' : 'EMAILID',
    'reocordfile' : 'BASE64_ENCODED_DUNI_FLIGHTRECORD_FILE'
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success"
  }
```

DUNI 비행기록 파일을 비행기록으로 저장합니다.
저장한 비행기록 파일은 비행기록 목록에서 확인할 수 있습니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'duni_file_upload'을 입력합니다.
recordfile | Base64로 인코딩된 DUNO Flight Record File 입니다. (포멧. "파일정보,Base64 Encoded Text")
youtube_data_id | 유튜브 URL을 입력합니다. ex) https://youtube.com/watch?v=k12hadf (Optional)

> DUNI Flight Record file 의 포맷:

```json
[
	{
		"lat" : 123.123, // Latitude
		"lng" : 37.11, // Longitude
		"alt" : 5.52, // Altitude
		"dsec" : 0, //영상녹화 시작후 시각. (밀리초) (Optional)
		"yaw" : 20, // The yaw value of the aircraft, where 0 corresponds to a True North heading. Yawing clockwise will increase yaw value. (Optional)
		"pitch" : -2, // The pitch value of the aircraft: forward is positive, backward is negative. Units are in degrees. (Optional)
		"roll" : 12, // The roll value of the aircraft: forward is positive, backward is negative. Units are in degrees. (Optional)
		"speed" : 2.1, // Speed (Optional)
		"act"	: 0, //Action - 임의값 또는 개발자 지정 ex) 녹화시작:1, 녹화종료:2 (Optional)
		"actparam" : 0, //Action을 위한 파라메터 ex) 1 (Optional)
		"dtimestamp" : 1569903583000, // timestamp
		"etc" : { "battery" : 12 } // 배터리 잔여량 (%) (Optional)
	},

	{
		"lat" : 123.123, // Latitude
		"lng" : 37.11, // Longitude
		"alt" : 5.52, // Altitude
		"dsec" : 10, //영상녹화 시작후 시각. (밀리초) (Optional)
		"yaw" : 20, // The yaw value of the aircraft, where 0 corresponds to a True North heading. Yawing clockwise will increase yaw value. (Optional)
		"pitch" : -2, // The pitch value of the aircraft: forward is positive, backward is negative. Units are in degrees. (Optional)
		"roll" : 12, // The roll value of the aircraft: forward is positive, backward is negative. Units are in degrees. (Optional)
		"speed" : 2.1, // Speed (Optional)
		"act"	: 0, //Action - 임의값 또는 개발자 지정 ex) 녹화시작:1, 녹화종료:2 (Optional)
		"actparam" : 0, //Action을 위한 파라메터 ex) 1 (Optional)
		"dtimestamp" : 1569903593000, // timestamp
		"etc" : { "battery" : 12 } // 배터리 잔여량 (%) (Optional)
	},

	{
		"lat" : 123.123, // Latitude
		"lng" : 37.11, // Longitude
		"alt" : 5.52, // Altitude
		"dsec" : 20, //영상녹화 시작후 시각. (밀리초) (Optional)
		"yaw" : 20, // The yaw value of the aircraft, where 0 corresponds to a True North heading. Yawing clockwise will increase yaw value. (Optional)
		"pitch" : -0, // The pitch value of the aircraft: forward is positive, backward is negative. Units are in degrees. (Optional)
		"roll" : 12, // The roll value of the aircraft: forward is positive, backward is negative. Units are in degrees. (Optional)
		"speed" : 2.1, // Speed (Optional)
		"act"	: 0, //Action - 임의값 또는 개발자 지정 ex) 녹화시작:1, 녹화종료:2 (Optional)
		"actparam" : 0, //Action을 위한 파라메터 ex) 1 (Optional)
		"dtimestamp" : 1569903703000, // timestamp
		"etc" : { "battery" : 12 } // 배터리 잔여량 (%) (Optional)
	}
]
```


## 비행기록에 유튜브영상 반영하기

```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"youtube", "name":"FLIGHTRECORDNAME", "youtube_data_id" : "https://youtube.com/watch?v=k12hadf" }' https://api.duni.io/v1/

```

```php

$body['action'] = 'position';
$body['daction'] = 'youtube';
$body['clientid'] = 'EMAILID';
$body['name'] = "FLIGHTRECORDNAME";
$body['youtube_data_id'] = "https://youtube.com/watch?v=k12hadf";

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action":"position", "daction": "youtube", "clientid" : "EMAILID", "name" : "FLIGHTRECORDNAME", "youtube_data_id" : "https://youtube.com/watch?v=k12hadf"};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'position',
    'daction': 'youtube',
    'clientid' : 'EMAILID',
    'youtube_data_id' : 'https://youtube.com/watch?v=k12hadf',
    'name' : 'NAME'
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success"
  }
```
비행기록에 유튜브 영상 링크를 설정합니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position' 입력합니다.
daction | 'youtube' 입력합니다.
name | 비행기록의 이름을 입력합니다.
youtube_data_id | 유튜브 URL을 입력합니다. ex) https://youtube.com/watch?v=k12hadf


# 기타 Helper API

## GPS좌표로 드론기업 검색하기

```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"company", "lat":33.1232, "lng":121.11}' https://api.duni.io/v1/

```

```php

$body['action'] = 'position';
$body['daction'] = 'company';
$body['clientid'] = 'EMAILID';
$body['lat'] = 33.1232;
$body['lng'] = 33.1232;

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "position", "daction": "company", "clientid" : "EMAILID", "lat" : 33.123, "lng" : 123.11};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'position',
    'daction': 'company',
    'clientid' : 'EMAILID',
    'lat' : 33.123,
    'lng' : 123.121
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success",
    "data":[
          {
          "name":"drone company 1",
          "lat" : 127.122,
          "lng" : 37.1122,
          "cid" : 55
      },

      {
        "name":"drone company 2",
        "lat" : 128.122,
        "lng" : 37.1522,
        "cid" : 23
      }
    ],
    "morekey" : "<some value>"
  }
```

요청한 GPS 좌표 근처의 드론기업을 검색하고 결과를 10개씩 응답합니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'company'을 입력합니다.
lat | 위도
lng | 경도
morekey | 이전에 받은 morekey 값을 입력하면 다음 10개의 목록을 가져 옵니다. (Optional)


## 드론기업 상세보기

```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"company_detail", "cid":55}' https://api.duni.io/v1/

```

```php

$body['action'] = 'position';
$body['daction'] = 'company_detail';
$body['clientid'] = 'EMAILID';
$body['cid'] = 55;

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "position", "daction": "company_detail", "clientid" : "EMAILID", "cid" : 55};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'position',
    'daction': 'company_detail',
    'clientid' : 'EMAILID',
    'cid' : 55
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success",
    "data":
          {
          "name":"drone company 1",
          "lat" : 127.122,
          "lng" : 37.1122,
          "cid" : 55,
          "address" : "somewhere",
          "phone_num_1" : "00-0000-0000",
          "phone_num_2" : "00-0000-1111",
          "etc" ... (to be added many things more :))
          }
  }
```

드론기업의 상세정보를 응답합니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'company_detail'을 입력합니다.
cid | 'cid'값을 입력합니다. "GPS좌표로 드론기업 검색하기" API를 참고해 주세요.


## 기상정보 불러오기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"util", "daction":"weather", "lat":"123.122", "lng":"32.111"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'util';
$body['daction'] = 'weather';
$body['clientid'] = 'EMAILID';
$body['lat'] = '123.122';
$body['lng'] = '32.111';

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "util", "daction": "weather", "clientid" : "EMAILID", "lat":"123.122", "lng":"32.111"};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'util',
    'daction': 'weather',
    'clientid' : 'EMAILID',
    'lat' : '123.122',
    'lng' : '33.111'
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success",
    "temp" : "20.2", //온도(섭씨)
    "wind" : "2", //풍속(m/s)
    "pty" : "rain", //기상 - "rain/snow", "snow", "sun",
    "vec" : "293", //풍향(각도, degree), 0:북, 90:동, 180:남, 270:서 - ex) 븍북동풍 : 0 ~ 45사이의 값
    "currentk" : "1", //자기장지수(Kp)
    "sunset" : "1730", //일몰시각
    "sunrise" : "0749", //일출시각
    "clouds" : "10", //구름이 낀 정도(%)
    "visibility" : "10000", //가시거리(m)
    "rain_p" : "10" //강수확률(%)
  }
```

온도, 풍속, 기상, 자기장 등의 기상정보를 응답합니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'util'을 입력합니다.
daction | 'weather'을 입력합니다.
lat | 위도
lng | 경도


## 사용자 clientid 불러오기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"util", "daction":"check_email", "target":"email@address.com"}' https://api.duni.io/v1/

```

```php

$body['action'] = 'util';
$body['daction'] = 'check_email';
$body['clientid'] = 'EMAILID';
$body['target'] = 'email@address.com';

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.duni.io/v1/');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "util", "daction": "check_email", "clientid" : "EMAILID", "target":"email@address.com"};

$.ajax({url : "https://api.duni.io/v1/",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("droneplay-token", "DRONEPLAYTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'droneplay-token' : 'DRONEPLAYTOKEN'
}
data = {
    'action': 'util',
    'daction': 'check_email',
    'clientid' : 'EMAILID',
    'target' : 'email@adress.com'
}

url = 'https://api.duni.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 이 요청은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success",
    "emailid" : "emailid"
  }
```

해당 email을 보유한 DUNI 파일럿 센터 회원의 clientid를 불러옵니다.

### HTTP 요청

`POST https://api.duni.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'util'을 입력합니다.
daction | 'check_email'을 입력합니다.
target | 이메일 주소를 입력합니다.

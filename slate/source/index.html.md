---
title: DUNI Open API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - php
  - javascript
  - python

toc_footers:
  - <div class="fb-like" data-href="https://www.facebook.com/386832955100142" data-width="100" data-layout="button_count" data-action="like" data-size="small" data-show-faces="false" data-share="false"></div>
  - <a href='https://pilot.duni.io/'>DUNI PILOT 홈</a>
  - <a href='https://pilot.duni.io/center'>DUNI PILOT Center</a>
  - <a href='https://developer.duni.io/'>DUNI 개발자홈</a>
  - <a href='https://code.duni.io/'>DUNI Codes</a>
  - <a href='https://duni.io/'>DUNI 홈</a>
  - <a href='https://www.facebook.com/DuniPilotPage/'>DUNI PILOT 페이스북</a>
  - <a href='https://groups.google.com/forum/#!forum/droneplay2018'>개발관련 문의게시판</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>
  - © 2020 APLY Inc.
includes:
  - errors

search: true
---

# 소개

'우리는 드론을 세계일주 시킬겁니다'

이곳은 드론 소프트웨어 개발자분들을 위한 예제코드와 Open API 정보를 제공하는 사이트 입니다.
뿐만아니라 드론을 '세계일주' 시키기 위한 관련 코드들도 계속해서 추가할 예정입니다.
쌈박하고 깔끔한 아이디어가 녹아든 쉽고 간편한 Open API와 코드들을 둘러 보세요.


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
개발자 Token은 아래의 DUNI PILOT CENTER에 가입해서 받으실 수 있습니다.

[DUNI PILOT CENTER](https://pilot.duni.io/center).

또는, "가입하기" API를 통해 발급 받을 수도 있습니다.




#가입 및 로그인

##가입하기

```shell

curl -H "Content-type: application/json" -X POST -d '{"action":"member", "daction":"register", "socialid" : "EMAILADDRESS1", "phone_number" : "USER_PHONE_NUMBER", "name" : "USER_NAME", "sns_token" : "SNS_ID_TOKEN", "sns_kind" : "SNS_KIND"}' https://api.droneplay.io/v1/

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
curl_setopt($ch, CURLOPT_URL, 'https://api.droneplay.io/v1/');
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

$.ajax({url : "https://api.droneplay.io/v1/",
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
url = 'https://api.droneplay.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

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

전화번호와 이메일주소 그리고 이름을 입력을 받아 회원을 등록합니다.

### HTTP 요청

`POST https://api.droneplay.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
action | 'member'을 입력합니다.
daction | 'register'을 입력합니다.
name | 가입자명을 입력합니다.
sns_kind | facebook, naver, apple, kakao, google 중 하나를 입력합니다.
sns_token | sns 로그인 후 받은 id token 값을 입력합니다.
phone_number | 가입자의 전화번호를 입력합니다.
socialid | 가입자의 이메일주소를 입력합니다.



##로그인

```shell

curl -H "Content-type: application/json" -X POST -d '{"action":"member", "daction":"login", "sns_token" : "SNS_ID_TOKEN", "sns_kind" : "SNS_KIND"}' https://api.droneplay.io/v1/

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
curl_setopt($ch, CURLOPT_URL, 'https://api.droneplay.io/v1/');
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

$.ajax({url : "https://api.droneplay.io/v1/",
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
url = 'https://api.droneplay.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result": "success",
    "token": "USER_TOKEN",
    "emailid": "aadsfasf@naver.com",
    "socialid" : "test@test.com"
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

`POST https://api.droneplay.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
action | 'member'을 입력합니다.
daction | 'login'을 입력합니다.
sns_kind | facebook, naver, apple, kakao, google 중 하나를 입력합니다.
sns_token | sns 로그인 후 받은 id token 값을 입력합니다.

# 드론의 현재위치 기록/읽기

## 드론의 현재위치 기록하기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"set", "lat" : 12.134132, "lng" : 12.1324, "alt" : 5, "yaw":10, "pitch" : 10, "roll": 10, "act" : 0, "missionname" : "TESTMISSION1", "missionid" : "mission-1"}' https://api.droneplay.io/v1/

```

```php

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
$body['missionid'] = "mission-1";
$body['missionname'] = "TESTMISSION1";

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.droneplay.io/v1/');
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

var jdata = {"action":"position", "daction": "set", "clientid" : "EMAILID", "lat" : 12.134132, "lng" : 12.1324, "alt" : 5, "yaw":10, "pitch" : 10, "roll": 10, "act" : 0, "missionid" : "mission-1", "missionname" : "TESTMISSION1"};

$.ajax({url : "https://api.droneplay.io/v1/",
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
    'action': 'position',
    'daction': 'set',
    'clientid' : 'EMAILID'
    'lat' : 12.134132,
    'lng' : 12.1324,
    'alt' : 5.2,
    "missionid" : "mission-1",
    "missionname" : "TESTMISSION1",
    "yaw":10,
    "pitch" : 10,
    "roll": 10,
    "act" : 0
}
url = 'https://api.droneplay.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result": "success"
  }
```

현재의 좌표와 고도를 기록합니다.

### HTTP 요청

`POST https://api.droneplay.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'set'을 입력합니다.
lat | latitude 좌표값를 입력합니다. (double)
lng | longitude 좌표값를 입력합니다. (double)
alt | 고도값을 입력합니다. (double, 미터)
act | 해당위치에서 수행한 행동 (개발자 임의 정의 가능, int)
yaw | 기체의 yaw 값 입력 (double, degree, Optional)
pitch | 기체의 pitch 값 입력 (double, degree, Optional)
roll | 기체의 roll 값 입력 (double, degree, Optional)
missionid | MISSION의 ID (미션 저장하기 참고 - Optional)
missionname | MISSION의 이름 (미션 저장하기 참고 - Optional)

<aside class="warning">
Token의 노출에 유의하세요!
</aside>

## 드론의 최근 위치 읽어오기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"get", "start" : 1518534859144, "end" : 1518534861111}' https://api.droneplay.io/v1/

```

```php

$body['action'] = 'position';
$body['daction'] = 'get';
$body['clientid'] = 'EMAILID';
$body['start'] = 1518534859144;
$body['end'] = 1518534861111;

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.droneplay.io/v1/');
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


var jdata = {"action": "position", "daction": "get", "clientid" : "EMAILID", "start" : 1518534859144, "end" : 1518534861111 };

$.ajax({url : "https://api.droneplay.io/v1/",
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
    'start' : 1518534859144,
    'end' : 1518534861111
}
url = 'https://api.droneplay.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()


```
> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
{
  "result" : "success",
  "data" : [
   {
     "positiontime" : "Tue Feb 13 2018 15:44:40 GMT+0000 (UTC)",
     "dtimestamp" : 1518536680763,
     "lat" : 37.2435813,
     "lng" : 131.8661992,
     "alt" : 1.2,
     "yaw" : 10,
     "roll" : 10,
     "pitch" : 10.1,
     "act" : 0,
     "missionname" : "TESTMISSION1",
     "missionid" : "mission-1",
     "clientid" : "EMAILID"
   },
   {
     "positiontime" : "Tue Feb 13 2018 15:44:40 GMT+0000 (UTC)",
     "dtimestamp" : 1518536680765,
     "lat" : 37.2424227,
     "lng" : 131.8673264,
     "alt" : 3.33,
     "yaw" : 10,
     "roll" : 10,
     "pitch" : 10.1,
     "act" : 0,
     "missionname" : "TESTMISSION1",
     "missionid" : "mission-2",
     "clientid" : "EMAILID"
   },
   {
     "positiontime" : "Tue Feb 13 2018 15:44:40 GMT+0000 (UTC)",
     "dtimestamp" : 1518536680763,
     "lat" : 37.2421004,
     "lng" : 131.8680063,
     "alt" : 5.55,
     "yaw" : 10,
     "roll" : 10,
     "pitch" : 10.1,
     "act" : 0,
     "missionname" : "TESTMISSION1",
     "missionid" : "mission-3",
     "clientid" : "EMAILID"
   }
  ]
}

```

<aside class="warning">positiontime은 GMT+0 기준입니다. 서울기준이 아닙니다.</aside>
<aside class="warning">dtimestamp는 GMT+0 기준입니다. 서울기준이 아닙니다.</aside>

### HTTP 요청

`POST https://api.droneplay.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
action | 'position'을 입력합니다.
daction | 'get'을 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
start (optional) | timestamp 값입니다. GMT+0 기준입니다. start ~ end 시각 사이의 결과를 요청할 때 사용합니다.
end (optional) | timestamp 값입니다. GMT+0 기준입니다.

# Mission 저장/불러오기

## Mission 저장


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"mission", "daction":"set", "mname" : MISSIONNAME, "missiondata" : [{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"act":1,"actparam":1,"id":"mission-1"},{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"act":1,"actparam":1,"id":"mission-2"}]}' https://api.droneplay.io/v1/

```

```php

$body['action'] = 'mission';
$body['daction'] = 'set';
$body['clientid'] = 'EMAILID';
$body['mname'] = "MISSIONNAME";
$body['missiondata'] = json_decode('[{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"act":1,"actparam":1,"id":"mission-1"},{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"act":1,"actparam":1,"id":"mission-2"}]');

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.droneplay.io/v1/');
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

var jdata = [{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"act":1,"actparam":1,"id":"mission-1"},{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"act":1,"actparam":1,"id":"mission-2"}];

$.ajax({url : "https://api.droneplay.io/v1/",
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
    "missiondata" : [{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"act":1,"actparam":1,"id":"mission-1"},{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"act":1,"actparam":1,"id":"mission-2"]
}

url = 'https://api.droneplay.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result": "success"
  }
```

DUNI Pilot Center에 Mission 데이터를 기록합니다.

### HTTP 요청

`POST https://api.droneplay.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'mission'을 입력합니다.
daction | 'set'을 입력합니다.
mname | Mission 이름을 입력합니다.
speed | 비행 속도(m/s)를 입력합니다. (int)
missiondata | Mission 데이터 목록을 입력합니다.

### missiondata 파라메터 포멧
[{lat:latitude, lng:longitude, alt:altitude, act:action, actparam:actionparam, speed:speed, id:mission-id}]

파라메터 | 설명
--------- | -----------
lat | 위도 (double)
lng | 경도 (double)
alt | 고도 (double, 미터)
act | 해당위치에서 드론이 수행할 행동 (int, DJI기준, 또는 개발자 임의 정의)
actparam | action 에 대한 파라메터
speed | 비행 속도(m/s)를 입력합니다. (int : Deprecated)
id | Mission의 고유 아이디 (부여한 Mission 이름의 범위내에서 고유한 아이디, 개발자 임의입력 가능)

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


## Mission 불러오기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"mission", "daction":"get"}' https://api.droneplay.io/v1/

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
curl_setopt($ch, CURLOPT_URL, 'https://api.droneplay.io/v1/');
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

$.ajax({url : "https://api.droneplay.io/v1/",
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

url = 'https://api.droneplay.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

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
          "clientid":"EMAILID"
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
          "clientid":"EMAILID"
      }
    ]
  }
```
DUNI Pilot Center의 Mission 목록을 불러옵니다.

### HTTP 요청

`POST https://api.droneplay.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'mission'을 입력합니다.
daction | 'get'을 입력합니다.


## Mission 삭제하기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"mission", "daction":"delete", "mname":"MISSIONNAME"}' https://api.droneplay.io/v1/

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
curl_setopt($ch, CURLOPT_URL, 'https://api.droneplay.io/v1/');
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

$.ajax({url : "https://api.droneplay.io/v1/",
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

url = 'https://api.droneplay.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success"
  }
```
DUNI Pilot Center의 Mission 1개를 삭제합니다.

### HTTP 요청

`POST https://api.droneplay.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'mission' 입력합니다.
daction | 'delete' 입력합니다.
mname | 삭제할 Mission 이름을 입력합니다.




# 비행기록 저장하기/가져오기

## 비행기록 저장하기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"upload", "name" : "FLIGHTRECORDNAME", "memo": "MEMO", "flat" : 37.243835988516, "flng" : 127.1122, "data" : [{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"yaw" : 10, "pitch" : 10, "roll" : 10,"act":1,"actparam":1,"id":"mission-1"},{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"yaw" : 10, "pitch" : 10, "roll" : 10,"act":1,"actparam":1,"id":"mission-2"}]}' https://api.droneplay.io/v1/

```

```php

$body['action'] = 'position';
$body['daction'] = 'upload';
$body['clientid'] = 'EMAILID';
$body['name'] = "FLIGHTRECORDNAME";
$body['memo'] = "MEMO";
$body['flat'] = 37.243835988516;
$body['flng'] = 127.1122;
$body['missiondata'] = json_decode('[{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"yaw" : 10, "pitch" : 10, "roll" : 10,"act":1,"actparam":1,"id":"mission-1"},{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0,"yaw" : 10, "pitch" : 10, "roll" : 10,"act":1,"actparam":1,"id":"mission-2"}]');

$headers = array(
        'Content-Type: application/json',
        'droneplay-token: DRONEPLAYTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.droneplay.io/v1/');
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

var jdata = {"clientid":"EMAILID", "action":"position", "daction":"upload", "name" : "FLIGHTRECORDNAME", "memo" : "MEMO", "flat": 37.12341232, "flng": 127.1122, "data" :[{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0, "yaw" : 10, "pitch" : 10, "roll" : 10, act":1,"actparam":1,"id":"mission-1"},{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0, "yaw" : 10, "pitch" : 10, "roll" : 10,"act":1,"actparam":1,"id":"mission-2"}]};

$.ajax({url : "https://api.droneplay.io/v1/",
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
    "flat" : 37.112,
    "flng" : 127.12312,
    "data" : [{"lat":12.134132,"lng":12.1324,"alt":5,"speed":0, "yaw" : 10, "pitch" : 10, "roll" : 10, "act":1,"actparam":1,"id":"mission-1"},{"lat":12.134132,"lng": 12.1324 ,"alt":5,"speed":0, "yaw" : 10, "pitch" : 10, "roll" : 10, "act":1,"actparam":1,"id":"mission-2"}]
}

url = 'https://api.droneplay.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result": "success"
  }
```

DUNI Pilot Center에 비행 데이터를 기록합니다.

### HTTP 요청

`POST https://api.droneplay.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'upload'를 입력합니다.
name | 비행기록 이름을 입력합니다.
memo | 메모를 입력합니다.
flat | 비행기록을 기록한 위치의 latitude 좌표를 입력합니다.
flng | 비행기록을 기록한 위치의 longitude 좌표를 입력합니다.
data | 비행기록 목록을 입력합니다.

### missiondata 파라메터 포멧
[{lat:latitude, lng:longitude, alt:altitude, act:action, actparam:actionparam, speed:speed, dsec:time, yaw:yaw, pitch:pitch, roll:roll, id:mission-id}]

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
act | 해당위치에서 드론이 수행한 행동 (DJI기준, 또는 개발자 임의 정의)
actparam | action 에 대한 파라메터
id | Mission의 고유 아이디 (부여한 Mission 이름의 범위내에서 고유한 아이디, 개발자 임의입력 가능)

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


## 모든 비행기록 불러오기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"download"}' https://api.droneplay.io/v1/

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
curl_setopt($ch, CURLOPT_URL, 'https://api.droneplay.io/v1/');
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

$.ajax({url : "https://api.droneplay.io/v1/",
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

url = 'https://api.droneplay.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success",
    "data":[
          {
          "regtime":"Sun Dec 30 2018 13:11:39 GMT+0000 (UTC)",
          "name":"MISSIONNAME",
          "clientid":"EMAILID",
          "flat" : 127.122,
          "flng" : 37.1122,
          "memo" : "MYMEMO"
      },

      {
          "regtime":"Sun Dec 30 2018 13:11:39 GMT+0000 (UTC)",
          "name":"MISSIONNAME_2",
          "clientid":"EMAILID",
          "flat" : 127.122,
          "flng" : 37.1122,
          "memo" : "MYMEMO"
      }
    ]
  }
```

비행기록을 목록을 가져옵니다.

### HTTP 요청

`POST https://api.droneplay.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'download'을 입력합니다.



## 비행기록 1개 불러오기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"download_spe", "name": "FLIGHTRECORDNAME"}' https://api.droneplay.io/v1/

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
curl_setopt($ch, CURLOPT_URL, 'https://api.droneplay.io/v1/');
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

$.ajax({url : "https://api.droneplay.io/v1/",
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

url = 'https://api.droneplay.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success",
    "data":[
          {
          "regtime":"Sun Dec 30 2018 13:11:39 GMT+0000 (UTC)",
          "data":[
              {"alt":3,"lng":131.86471756082,"act":0,"id":"mission-1","lat":37.243835988516,"actparam":1, "speed":10, "yaw" : 10, "roll" : 10, "pitch" : 10, "dsec" : 0},
              {"alt":3,"lng":131.86645915266,"act":0,"id":"mission-2","lat":37.244423805175,"actparam":1, "speed":10, "yaw" : 10, "roll" : 10, "pitch" : 10, "dsec" : 0},
              {"alt":3,"lng":131.86671844684,"act":0,"id":"mission-3","lat":37.243568918929,"actparam":1, "speed":10, "yaw" : 10, "roll" : 10, "pitch" : 10, "dsec" : 0},
              {"alt":3,"lng":131.86493079644,"act":0,"id":"mission-4","lat":37.243182141771,"actparam":1, "speed":10, "yaw" : 10, "roll" : 10, "pitch" : 10, "dsec" : 0},
              {"alt":3,"lng":131.86491855886,"act":0,"id":"mission-5","lat":37.243758419995,"actparam":1, "speed":10, "yaw" : 10, "roll" : 10, "pitch" : 10, "dsec" : 0},
              {"alt":3,"lng":131.86492249835,"act":0,"id":"mission-6","lat":37.243906083699,"actparam":1, "speed":10, "yaw" : 10, "roll" : 10, "pitch" : 10, "dsec" : 0},
              {"alt":3,"lng":131.86492249835,"act":0,"id":"mission-7","lat":37.243903981846,"actparam":1, "speed":10, "yaw" : 10, "roll" : 10, "pitch" : 10, "dsec" : 0}
            ],
          "name":"MISSIONNAME",
          "clientid":"EMAILID",
          "flat" : 37.243835988516,
          "flng" : 131.86471756082,
          "memo" : "MYMEMO"
      }
    ]
  }
```

지정한 이름의 비행기록 1개를 불러옵니다.

### HTTP 요청

`POST https://api.droneplay.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'download_spe'을 입력합니다.
name | 비행기록 이름을 입력합니다.


## 비행기록 삭제하기

```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"delete", "name":"FLIGHTRECORDNAME"}' https://api.droneplay.io/v1/

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
curl_setopt($ch, CURLOPT_URL, 'https://api.droneplay.io/v1/');
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

$.ajax({url : "https://api.droneplay.io/v1/",
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

url = 'https://api.droneplay.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success"
  }
```
비행기록 1개 삭제합니다.

### HTTP 요청

`POST https://api.droneplay.io/v1/`

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

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"convert", "reocordfile":"BASE64_ENCODED_DJI_FLIGHTRECORD_FILE"}' https://api.droneplay.io/v1/

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
curl_setopt($ch, CURLOPT_URL, 'https://api.droneplay.io/v1/');
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

$.ajax({url : "https://api.droneplay.io/v1/",
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

url = 'https://api.droneplay.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success"
  }
```

DJI 비행기록 파일을 분석하여 비행기록으로 저장합니다.
저장한 비행기록 파일은 비행기록 목록에서 확인할 수 있습니다.

### HTTP 요청

`POST https://api.droneplay.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'convert'을 입력합니다.
recordfile | Base64로 인코딩된 DJI Flight Record File 입니다. (포멧. "파일정보,Base64 Encoded Text")

DJI Flight Record file 위치:
https://forum.dji.com/thread-98213-1-1.html


## DUNI 비행기록 파일 업로드 하기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"position", "daction":"duni_file_upload", "reocordfile":"BASE64_ENCODED_DUNI_FLIGHTRECORD_FILE"}' https://api.droneplay.io/v1/

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
curl_setopt($ch, CURLOPT_URL, 'https://api.droneplay.io/v1/');
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

$.ajax({url : "https://api.droneplay.io/v1/",
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

url = 'https://api.droneplay.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success"
  }
```

DUNI 비행기록 파일을 비행기록으로 저장합니다.
저장한 비행기록 파일은 비행기록 목록에서 확인할 수 있습니다.

### HTTP 요청

`POST https://api.droneplay.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'position'을 입력합니다.
daction | 'duni_file_upload'을 입력합니다.
recordfile | Base64로 인코딩된 DUNO Flight Record File 입니다. (포멧. "파일정보,Base64 Encoded Text")

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
		"dtimestamp" : 1569903583000, // timestamp (Optional)
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
		"dtimestamp" : 1569903593000, // timestamp (Optional)
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
		"dtimestamp" : 1569903703000, // timestamp (Optional)
		"etc" : { "battery" : 12 } // 배터리 잔여량 (%) (Optional)
	}
]
```


# 기타 Helper API

## 날씨 정보 가져오기


```shell

curl -H "droneplay-token: DRONEPLAYTOKEN" -H "Content-type: application/json" -X POST -d '{"clientid":"EMAILID", "action":"util", "daction":"weather", "lat":"123.122", "lng":"32.111"}' https://api.droneplay.io/v1/

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
curl_setopt($ch, CURLOPT_URL, 'https://api.droneplay.io/v1/');
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

$.ajax({url : "https://api.droneplay.io/v1/",
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

url = 'https://api.droneplay.io/v1/'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success",
    "temp" : 20, //온도, 섭씨
    "wind" : 2, //풍속, m/s
    "pty" : "rain" //기상 - "rain/snow", "snow", "sun"
  }
```

온도, 풍속, 기상 정보를 가져옵니다.

### HTTP 요청

`POST https://api.droneplay.io/v1/`

### URL 파라메터

파라메터 | 설명
--------- | -----------
droneplay-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
clientid | 로그인 후 수신한 emailid 값을 입력합니다.
action | 'util'을 입력합니다.
daction | 'weather'을 입력합니다.
lat | 위도
lng | 경도

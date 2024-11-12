# JungJong 부통산 프로젝트
- FE - 육종호
- BE - 손정찬

--- 
### 목차
 - [1. 프로젝트 소개](#프로젝트_소개)
 - [2. 프론트엔드](#Frontend)
 - [3. 백엔드](#Backend)
   - [3.1. 공공 API 자료](#API)
     - [3.1.1 아파트 매매 실거래가 자료](#국토교통부_아파트_매매_실거래가_상세_자료_(24.08.23))
     - [3.1.2 아파트 전월세 실거래가 자료]()
     - [3.1.3 단독/다가구 매매 실거래가 자료]()
     - [3.1.4 단독/다가구 전월세 실거래가 자료]()
   - [3.2. 백엔드 API](#벡엔드-API)
     - [3.2.1 회원 도메인](#회원_도메인)
     - [3.2.2 아파트 도메인](#아파트_도메인_[Required_Access_Token])
     - [3.2.3 단독/다가구 도메인](#단독/다가구_도메인_[Required_Access_Token])
     - [3.2.4 지도 도메인](#지도-도메인-[Required-Access-Token]-*)
     - [3.2.5 AI 도메인](#AI-도메인-[Required-Access-Token])
     - [3.2.6 요청/응답 구조](#요청/응답-구조)
--- 
# 프로젝트 소개
...

--- 
# 프론트엔드
...  

---
# 백엔드
![back_architect](./backend/img/back_arch.svg)

# API
## 국토교통부_아파트 매매 실거래가 상세 자료 (24.08.23)
https://www.data.go.kr/data/15126468/openapi.do#/API%20%EB%AA%A9%EB%A1%9D/getRTMSDataSvcAptTradeDev

### Request Params
- LAWD_CD
    - 법종동코드 10자리 중 5자리
- DEAL_YMD
    - 계약년월 6자리
- serviceKey
    - 인증키
- pageNo
    - 페이지 번호
- numOfRows
    - 한 페이지 결과 수

### Reponse
```json
{
  "header": {
    "resultCode": "string",
    "resultMsg": "string"
  },
  "body": {
    "items": {
      "item": {
        "sggCd": "string",
        "umdCd": "string",
        "landCd": "string",
        "bonbun": "string",
        "bubun": "string",
        "roadNm": "string",
        "roadNmSggCd": "string",
        "roadNmCd": "string",
        "roadNmSeq": "string",
        "roadNmbCd": "string",
        "roadNmBonbun": "string",
        "roadNmBubun": "string",
        "umdNm": "string",
        "aptNm": "string",
        "jibun": "string",
        "excluUseAr": "string",
        "dealYear": "string",
        "dealMonth": "string",
        "dealDay": "string",
        "dealAmount": "string",
        "floor": "string",
        "buildYear": "string",
        "aptSeq": "string",
        "cdealType": "string",
        "cdealDay": "string",
        "dealingGbn": "string",
        "estateAgentSggNm": "string",
        "rgstDate": "string",
        "aptDong": "string",
        "slerGbn": "string",
        "buyerGbn": "string",
        "landLeaseholdGbn": "string"
      }
    },
    "numOfRows": 0,
    "pageNo": 0,
    "totalCount": 0
  }
}
```

## 국토교통부_아파트 전월세 실거래가 자료 (24.08.23)
### Request
- LAWD_CD
    - 법정동 앞 5자리
- DEAL_YMD
    - 계약년월 6자리
- serviceKey
    - 인증키
### Response#id1 
```json
{
  "header": {
    "resultCode": "string",
    "resultMsg": "string"
  },
  "body": {
    "items": {
      "item": {
        "sggCd": "string",
        "umdNm": "string",
        "aptNm": "string",
        "jibun": "string",
        "excluUseAr": "string",
        "dealYear": "string",
        "dealMonth": "string",
        "dealDay": "string",
        "deposit": "string",
        "monthlyRent": "string",
        "floor": "string",
        "buildYear": "string",
        "contractTerm": "string",
        "contractType": "string",
        "useRRRight": "string",
        "preDeposit": "string",
        "preMonthlyRent": "string"
      }
    },
    "totalCount": 0,
    "numOfRows": 0,
    "pageNo": 0
  }
}
```
## 국토교통부_단독/다가구 매매 실거래가 자료
### Request
- LAWD_CD
    - 법정동 앞 5자리
- DEAL_YMD
    - 계약년월
- serviceKey
    - 인증키
### Response
```json
{
  "header": {
    "resultCode": "string",
    "resultMsg": "string"
  },
  "body": {
    "items": {
      "item": {
        "sggCd": "string",
        "umdNm": "string",
        "houseType": "string",
        "jibun": "string",
        "totalFloorAr": "string",
        "plottageAr": "string",
        "dealYear": "string",
        "dealMonth": "string",
        "dealDay": "string",
        "dealAmount": "string",
        "buildYear": "string",
        "cdealType": "string",
        "cdealDay": "string",
        "dealingGbn": "string",
        "estateAgentSggNm": "string",
        "slerGbn": "string",
        "buyerGbn": "string"
      }
    },
    "totalCount": 0,
    "numOfRows": 0,
    "pageNo": 0
  }
}
```

## 국토교통부_단독/다가구 전월세 실거래가 자료
- LAWD_CD
    - 법정동 5자리
- DEAL_YMD
    - 계약 년월
- serviceKey
    - 인증키
# 백엔드 API
## 회원 도메인
### 로그인
- 네이버 소셜 로그인
    - [POST] /api/login/naver -> Tokens [HTTP 200]
### 회원가입
- 네이버 소셜 가입
    - [POST] /api/signup/naver -> Tokens [HTTP 201] ( 바로 Token 줄지, 성공 응답만 줄지 정하기)
### 회원 [Required Access Token]
- 유저 조회
    - [GET] /api/user -> User [HTTP 200]
- 유저 정보 수정
    - [PUT] /api/User -> [HTTP 200 OR 204]
    - [FETCH] /Api/User -> [HTTP 200 OR 204]
### 찜 [Required Access Token]
- 건물 찜하기
    - [POST] /api/favorite ->  [HTTP 201]
- 건물 찜한것들 조회
    - [GET] /api/favoite/list -> [HTTP 200]
        - 페이지네이션 ? -> offset, limit 추가하기
### 토큰
- Access Token 재발급 [Required Refresh Token]
    - [POST] /api/reissue -> [HTTP 200]  /  [HTTP 401 | 403]
## 아파트 도메인 [Required Access Token]
### 상세 정보
- 아파트 상세 정보 조회
    - [GET] /api/apt -> [HTTP 200]
## 단독/다가구 도메인 [Required Access Token]
### 상세 정보
- 아파트 상세 정보 조회
    - [GET] /api/single -> [HTTP 200]
## 지도 도메인 [Required Access Token] *


## AI 도메인 [Required Access Token]
### AI 평가 및 점수
- AI 평가 및 점수 요청
    - [POST] /api/ai/review -> [HTTP 200]

## 요청/응답 구조
### 요청
- 로그인 / 회원가입 제외하고는 항상 AccessToken을 헤더에 담아서 ...!
- AccessToken 만료 -> (성공 : [HTTP 200]) | (실패 : [HTTP 401] )
    - [HTTP 401] 받으면 Refresh Token으로 재발급
    - Refresh Token 도 [HTTP 401] OR [HTTP 403] 이면, 재로그인 시키기
    - (참고) 각 인가코드 및 인가상태코드는 1회용임,,, 재사용 불가능...!
### 응답
1. 구조 1
   ```json
   {
	   status: "success" | "fail" | HttpStatus,
	   massge: "데이터가 없습니다." | "성공" | "중복" 등...,
	   data: {
		   id: 1,
		   content: ~~,
		   ...
	   }
   }
   
   ```
2. 구조 2 (페이지네이션 추가할 경우)
   ```json
   {
	   status: "success" | "fail" | HttpStatus,
	   massge: "데이터가 없습니다." | "성공" | "중복" 등...,
	   data: {
		   id: 1,
		   content: ~~,
		   ...
	   },
	   pagenation : {
		   page: 0 | 1,
		   size: 10,
		   total: 10000,
		   totalPage: 1000,
		   isFirst: true,
		   isLast: false,
		   
		   (hasNext: true,) 
		   (hasprev: true )
	   }
   }
	```
3. 구조 3 (혹은 이렇게도 가능 편한걸루...)
```json
 {
   respons: {
	   status: "success" | "fail" | HttpStatus,
	   massge: "데이터가 없습니다." | "성공" | "중복" 등...,
	   data: {
		   id: 1,
		   content: ~~,
		   ...
	   }
   },
   pagenation : {
	   page: 0 | 1,
	   size: 10,
	   total: 10000,
	   totalPage: 1000,
	   isFirst: true,
	   isLast: false,
	   
	   (hasNext: true,) 
	   (hasprev: true )
   }
}
```

# 추가 사항
- Kotlin 써도 되는지?
- 익명 의견 or 댓글 기능은 어떨까?
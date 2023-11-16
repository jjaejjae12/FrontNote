
## 용어
---



## 정의
---
> AWS의 CDN (Content Delivery Network) 서비스
> 
> 작동 방식 : 
> 사용자가 엣지로케이션으로 리소스 요청 만약 엣지로케이션에 없다면 -> 실제 리소스가 있는 서버로 요청



> [!faq] CDN(Content Delivery Network)
> CDN이란 지리적으로 사용자와 가까운 CDN에 임시로 웹 컨텐츠나 동적 컨텐츠 (이미지, 영상)등을 캐싱
>사용자의  리소스의 로드 시간을 단축시키는 서비스 

> [!faq] 엣지로케이션
> 실제 CDN을 서비스를 지원하는 지리적 지점

## 구성
---

> [!abstract] 구성
>- ### Origin
>- ### Distridution
>- ### 주요 설정 및 용어
>- ### Cache Key
>- ### Policy

>[!faq] Origin
>실제 데이터가 존재하는 근원
>- AWS 서비스 ( S3, EC2, ELB, Route 53 등 )
>- 온프레미스 서버 ( 자체서버 )

>[!faq] Distridution
>CDN을 나누는 단위

>[!faq] 주요 설정 및 용어
>- ### TTL
>- ### Invalidate
>
>>[!note]  TTL ( Time to Live )
>>캐싱된 데이터가 살아있는 설정이 가능하고 TTL초 이후 자동으로 캐싱을 삭제한다.
>
>>[!note] 파일 무효화 ( invalidate ) 
>>TTL을 기달리지 않고 바로 캐시에서 삭제하는 것
>>- 업데이트된 파일을을 캐싱해야 할 때 사용
>>- 비용이 발생한다
>>- CloudFront API, 콘솔, Thrid-Party 툴등으로 사용 가능

>[!faq] Cache Key
>### 캐싱 기준 설정
> - 어떤 기준으로 리소스를 캐싱할것인지 결정
> - 기본값은 URL
> - 이후 header, cookie, 쿼리스트링으로 세밀한 구별 가능

>[!faq]  Policy
>캐싱 방법, 허용 헤더 등을 정의
>- Cache Control ( 캐싱 방법 및 압축 )
>TL 및 Cache key 정책, CloudFront가 어떻게 캐싱할지 결정
>---
>- Origin Request
>Origin에 쿠기, 헤더, 쿼리스트링등의 허용 정책을 정의
>---
>- 뷰어( 유저 ) 에게 보낼 http header
>CloudFront가 뷰어에게 응답과 같이 실어 보낼 http header설정 
>---
>- Origin에게 보낼 http header
>CloudFront가 뷰어 ( 유저 ) 정보를 header에 더해 Origin에 전송
>>[!note] CloudFrotn가 뷰어( 유저 )로 확인 가능한 정보
>>- 디바이스 정보 ( AOS, IOS, SmartTV 등 )
>>- IP 주소
>>- Country, 도시, 위도, 경도, 타임존 등





## 기능
---

> [!abstract] 기능
>- ### CDN
>- ### https 지원
>- ### 지리적 제한
>- ### 서비스 연계

>[!faq] CDN
>CloudFront는 정적, 동적 모두 최적화 해서 전송하는 특징이 있음
>
>> [!note] 최적화
>>정적 : 실제 로케이션 엣지를 통한 캐싱 속도 최적화
>>동적 : 네트워크 최적화 -> 통신전 전처리 과정의 최적화를 의미함(데이터 자체 최적화X)
>>
>>**DNS Lookup (DNS 조회)** => **TCP Connection (TCP 연결)** 
>>=> **Time to First Byte (TTFB, 첫 번째 바이트까지 걸리는 시간)**
>>
>>![[Pasted image 20231115161306.png]]
>
>> [!note] 정적, 동적 컨텐츠 통신 구별 방법 -> 경로 패턴으로 구별
>> ![[Pasted image 20231115150754.png]]
>

>[!faq] https 지원
>Origin에서 https를 지원하지 않더라도 CloudFront를 연결을 통한 https통신 지원
>
>>[!note] ACM ( AWS Certificate Manager )
>>AWS에서 지원하는  TLS, SSL 프로토컬
>
>![[Pasted image 20231116090930.png]]

>[!faq] 지리적 제한
>특정 지역 ( 국가 )의 접근을 제한 가능 

>[!faq] 서비스 연계
>- ## AWS WAF ( AWS 보안 서비스 )
>- ## Lambda@Edge & CloudFront Function
>
>>[!note] Lambda@Edge
>>엣지로케이션에서 실행되는 Lambda로 다양한 커스텀이 가능
>>- 한국에서 요청이 올 경우 한국 웹서버, 미국에서 요청이 올 경우 미국 웹서버로 분산  
>>- 커스텀 에러 페이지  
>>- Cookie를 검사해 다른 페이지로 리다이렉팅: A/B 테스팅 
>>- CloudFront에서 Origin 도착 이전에 인증 등
>>
>>![[Pasted image 20231116104910.png]]
>
>> [!note] CloudFront Function
>>Lambda@Edge의 6 / 1 비용으로 경량 함수 실행 ( 이때 언어는 JS만 가능 )
>>- 캐싱, 헤더 조작

## 리포팅
---

> [!faq] 리포팅
>CloudFront의 이용 지표 확인 기능
>- 캐시 상태
>- 가장 많이 요청 받은 컨텐츠
>- Top Referrer

## 보안
---

>[!abstract] 보안
>- Signed URL
>- Signed Cookie
>- Origin Access identity( OAI )
>- Field Level Encryption
> 
>>[!note] Signed URL
>>URL을 통한 단일 컨텐츠 접근 제한
>>- URL에는 시작시간, 종료시간, IP, 파일명, URL의 유효기간 등의 정보를 담을 수 있음
>>- 이 URL 접근 이외의 접근을 막고 허용된 유저에게만 URL을 전달하여 컨텐츠 제공을 제어 가능
>>- 단 하나의 파일 또는 컨텐츠에 대한 허용만 가능
>>- S3 Signed URL과 비슷한 방식
>
>>[!note] Signed Cookie
>>Cookie를 통한 다수 컨텐츠 접근 제한
>>- Signed URL과 마찬가지로 여러 제약사항 설정 가능
>>- 다수의 파일 및 스트리밍 접근 허용 가능
>>
>>Signed URL, Signed Cookie 사용사례: 프리미엄 유저만 볼 수 있는 강의 동영상 등
>
>>[!note] Origin Access identity( OAI )
>>S3의 http접근을 막고 CloudFront를 통한 접근만 허용하는 설정
>>( S3로 접근하면 CDN을 이용하지 못함, http통신이기에 보안 취약 )
>>- CloudFront만 권한을 가지고 S3에 접근하고 나머지 접근권한은 막음
>>- S3 Bucket Policy로 CloudFront의 접근을 허용해야 사용 가능
>
>





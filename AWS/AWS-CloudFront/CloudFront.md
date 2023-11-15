
## 용어
---



## 정의
---
> AWS의 CDN (Content Delivery Network) 서비스
> 
> 작동 방식 : 
> 사용자가 엣지로케이션으로 리소스 요청 만약 엣지로케이션에 없다면 -> 실제 리소스가 있는 서버로 요청



> [!faq]- CDN(Content Delivery Network)
> CDN이란 지리적으로 사용자와 가까운 CDN에 임시로 웹 컨텐츠나 동적 컨텐츠 (이미지, 영상)등을 캐싱
>사용자의  리소스의 로드 시간을 단축시키는 서비스 

> [!faq]- 엣지로케이션
> 실제 AWS에서 CDN을 서비스를 지원하는 지점

구성
---
> [!abstract]- 구성
>- ### Origin
>- ### Distridution
>- ### 주요 설정 및 용어
>- ### Cache Key
>- ### Policy

>[!faq]- Origin
>실제 데이터가 존재하는 근원
>- AWS 서비스 ( S3, EC2, ELB, Route 53 등 )
>- 온프레미스 서버 ( 자체서버 )

>[!faq]- Distridution
>CDN을 나누는 단위

>[!faq]- 주요 설정 및 용어
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

>[!faq]- Cache Key
>### 캐싱 기준 설정
> - 어떤 기준으로 리소스를 캐싱할것인지 결정
> - 기본값은 URL
> - 이후 header, cookie, 쿼리스트링으로 세밀한 구별 가능

>[!faq]- Policy
>## 동작 정챙 정의
>- 캐싱 방법, 허용 헤더 등을 정의


## 기능
> [!abstract]- 기능
>- ### CDN
>- ### https 지원
>- ### 지리적 제한
>- ### 서비스 연계

>[!faq]- CDN
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






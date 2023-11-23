
## 정의
---
>S3는 클래스별로 저장의 목적, 예산에 따른 다른 정장 밥법을 이용할 수 있고
>이러한 클래스가 총 8가지 존재 
>![[Pasted image 20231123135325.png]]

## Standard
---
> [!faq] Standard
> - 99.99% 가용성
> - 11 9's 내구성
> - 최소 3개 이상의 가용영역(AZ - Availability Zone)에 분산 저장
> - 최소 보관 기간, 보관 용량 없음
> - 파일 요청 비용 없음(전송 요금은 발생)
> - $0.025/gb(Seoul Reigon 기준)

## IA - Infrequently Accessed
---
>[!faq] IA - Infrequently Accessed
>- 자주 사용되지 않는 데이터를 저렴한 가격에 보관
>- 최소 3개 이상의 가용 영역에 분산 보관 - 11 9's 내구성
>- 최소 저장 용량 : 128kb(5kb를 저장 해도 128kb로 저장)
>- 최소 저장 기간 : 30일 (1일만 저장해도 30일 요금 발생!)
>- 데이터 요청 비용 발생(pre GB)
>- 자주 사용하진 않지만 중요한 파일일 때 사용
>- $0.0138/gb(Seoul Reigon 기준)

## One Zone IA
---
>[!faq] One Zone IA
>- 자주 사용되지 않고, 중요하지 않는 데이터를 저렴한 가격에 보관
>- 단 한 개의 가용 영역애 보관 - 11 9's 내구성 보장 x
>- 최소 저장 용량 : 128kb(5kb를 저장 해도 128kb로 저장)
>- 최소 저장 기간 : 30일 (1일만 저장해도 30일 요금 발생
>- 데이터 요청 비용 발생(pre GB)
>- 자주 사용하지 않으며 쉽게 복구할 수 있는 파일일 때 사용
>- $0.011/gb(Seoul Reigon 기준)

## Glacier Instant Retrieval
---
>[!faq] Glacier Instant Retrieval
>- 아카이브용 저장소
>- 최소 저장 용량 : 128kb(5kb를 저장 해도 128kb로 저장)
>- 최소 저장 기간 : 90일
>- 바로 액세스 가능
>- 의료 이미지 또는 뉴스 아카이브 등 사용
>- $0.005/gb(Seoul Reigon 기준) = Standard의 약 1/5

## Glacier Flexible Retrieval
---
>[!faq]  Glacier Flexible Retrieval
>- 아카이브용 저장소
>- 최소 저장 용량 : 40kb
>- 최소 저장 기간 : 90일
>- 분 ~ 시간 단위 이후 액세스 가능
>- 장애 복구용 데이터, 백업 데이터 등
>- $0.0045/gb(Seoul Reigon 기준)

## Glacier Deep Archive
---
>[!faq] Glacier Deep Archive
>- 아카이브용 저장소
>- 최소 저장 용량 : 40kb
>- 최소 저장 기간 : 90일
>- 데이터를 가져오는데 12 ~ 48시간 소요
>- 사용 사례 : 오래된 로그 저장, 사용할 일이 거의 없지만 법적으로 보관해야 하는 서류 등
>- $0.002/gb(Seoul Reigon 기준)

## Intelligent-Tiering
---
>[!faq] Intelligent-Tiering
>- 머신 러닝을 사용해 자동으로 클래스 변경
>- 퍼포먼스 손해/오버헤드 없이 요금 최적화

## S3 on Outposts
---
>[!faq] S3 on Outposts
>- 온프레미스 환경에 S3 제공
>- 내구성을 확보한 상태로 파일을 저장하도록 설계
>- IAM, S3 SDK등 사용 가능

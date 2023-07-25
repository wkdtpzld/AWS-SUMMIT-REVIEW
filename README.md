## AWS SUMMIT
제가 들었던 내용중 가장 유익하고 도입 가능성이 높은 AWS 상품을 글과 사진으로 기록해 두기 위해서 만들어 두었습니다.

### 스마트한 클라우드 스토리지 비용 관리 전략

AWS에서 스토리지 세개의 설명을 중심적으로 해주셨는데요.
1. S3
2. EBS
3. EFS

이 중에서 1번 S3에 대해서 한번 풀어보고자 합니다.

---
S3는 Simple Storage Service의 약자로, AWS에서 제공하는 인터넷 스토리지 서비스 입니다.

S3의 특징은 다음과 같습니다.
- 많은 사용자가 접속을 해도 시스템적인 작업이 없어도 된다.
- 저장할 수 있는 파일 수의 제한이 없다.
- 최소 1바이트에서 최대 5TB의 데이터를 저장하고 서비스 할 수 있다.
- 파일에 인증을 붙여서 무단으로 엑세스 하지 못하도록 할 수 있다.
- HTTP와 BitTorrent 프로토콜을 지원한다.
- REST, SOAP 인터페이스를 제공한다.
- 데이터를 여러 시설에서 중복으로 저장해 데이터의 손실이 발생할 경우 자동으로 복원한다.
- 버전관리 기능을 통해서 사용자에 의한 실수도 복원이 가능하다.
- 정보의 중요도에 따라서 보호 수준을 차등 할 수 있고, 이에 따라서 비용을 절감 할 수 있다. (RSS)
또한 버킷 생성이 비교적 쉬운 편이라서 이미지 스토리지를 생성하시는 많은 분들이 S3를 사용하시고 계십니다.

그런데 이 S3를 좀 더 스마트하게 사용할 수 있는 방법을 AWS SUMMIT 에서 소개해 주었는데요.

<img width="500" alt="image" src="https://github.com/wkdtpzld/AWS-SUMMIT-REVIEW/assets/87063105/1a17b4c1-2fa0-4bd0-811e-dbd054d62108">

스토리지 클래스의 요금과 접근 방식을 정리해 주셨는데요.

1. S3 Intelllgent-Tlering - 변화하는 액세스 패턴
> 하단 설명 참조
3. S3 Standard - 자주 액세스하는 데이터
> 가장 보편적으로 사용되는 스토리지 타입입니다. 
4. S3 Standard-Infrequent Access - 자주 액세스하지 않는 데이터
> 자주 접근되지 않지만 빠르게 데이터를 불러올 수 있는 스토리지 타입입니다. 데이터를 불러올 때 추가 비용이 발생합니다.
5. S3 One Zone-Infrequent Access - 재생성 가능하고 덜 엑세스되는 데이터
> IA 와 비슷하지만 가용영역이 하나밖에 없음
6. S3 Glacler Instant Retrleval - 거의 엑세스 되지 않는 데이터
> 아카이브 데이터지만 데이터 접근 자체는 빠르고 분기에 한, 두번 정도 불러올 때 적합
7. S3 Glacler Flexible Retrieval - 아카이브 데이터
> 수 분 ~ 몇 시간 이상의 검색 시간, 백업, 재해 복구에 적합
8. S3 Glacler Deep Archive - 장기 아카이브 데이터
> 제~~일 깊은 아카이브, 제일 저렴하고 제일 느림, 데이터 집합을 오랫동안 보관하는 서비스에 적합

---

많은 스토리지가 존재하는데요. S3의 스토리지 접근 빈도에 따라서 클래스를 고를 필요가 있습니다.

하지만 어느 데이터는 매우 많이, 자주 접근될 경우도 있고, 오래된 데이터는 접근을 오랫동안 안 할 가능성이 높습니다.

서비스 업체는 데이터를 일일히 옮기는것은 매우 불편하고 귀찮은 일이 될 수 있습니다.

만약 옮기지 않고 Standard에 설정을 해두었다면?? 요금 폭탄을 떠안게 되겠지요.

---

S3 자체적으로 수명 주기 규칙을 지정할 수 있는데요.

밑 사진과 같이 어느 날짜를 기점으로 저렴한 클래스로 내려 끝에는 아카이브 클래스까지 낮추어 최대한 가격을 내리거나. 버킷에서 해당 데이터를 삭제 할 수 있습니다.

예를들어 수명 주기 규칙을 생성해서 객체 생성 후 경과 일수가 30일 마다 Standard -> Instant Retrleval -> Archive 이동을 시켜 비용을 절감 시킬 수 있습니다.

<img width="99" alt="image" src="https://github.com/wkdtpzld/AWS-SUMMIT-REVIEW/assets/87063105/a3ae7292-6092-4d51-b374-95c5578ea7d0">
<img width="160" alt="image" src="https://github.com/wkdtpzld/AWS-SUMMIT-REVIEW/assets/87063105/0ea0d867-43ff-4f50-9879-d905f2129894">
<img width="122" alt="image" src="https://github.com/wkdtpzld/AWS-SUMMIT-REVIEW/assets/87063105/64f75297-248f-48ac-8a9c-0aa46c5cb043">
<img width="160" alt="image" src="https://github.com/wkdtpzld/AWS-SUMMIT-REVIEW/assets/87063105/0ea0d867-43ff-4f50-9879-d905f2129894">
<img width="134" alt="image" src="https://github.com/wkdtpzld/AWS-SUMMIT-REVIEW/assets/87063105/07d4e24b-5f92-47c8-9b72-2a19027acba6">

하지만 오래된 데이터 또한 접근이 많을수도 있고 적을수도 있고 동적일 가능성이 높습니다. 

수명 주기 규칙을 위와 같이 설정해 두었는데? 빨랐던 데이터 로딩 속도가 점점 느려질 수 있다는것이죠.

---
### 해결법

그래서 이번 AWS SUMMIT 에서 추천하는 클래스는 인텔리전트 티어링 클래스입니다.

**액세스 패턴을 모니터링하고 액세스 빈도수를 체크하고 데이터 파일의 티어를 변경해주는 클래스입니다.**

<img width="641" alt="image" src="https://github.com/wkdtpzld/AWS-SUMMIT-REVIEW/assets/87063105/04e3932f-aa3d-4c1e-b03d-2471ee0975dc">





### 참고자료
#### https://dev.classmethod.jp/articles/for-beginner-s3-explanation/

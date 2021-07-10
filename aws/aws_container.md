# AWS Container

## 컨테이너 개요

표준화된 소프트웨어 단위.           

1. 애플리케이션
2. 공유 서비스 플랫폼
3. 엔터프라이즈 앱 마이그레이션
4. 기계 학습

> 컨테이너와 가상 머신의 차이   
> 컨테이너는 기본 호스트 시스템의 OS 커널을 공유한다

### 가상화 플랫폼 Docker

- 경량 컨테이너 가상화 플랫폼
- 컨테이너를 생성, 저장, 관리 및 실행할 수 있는 도구 제공
- 자동화된 구축, 테스트 및 배포

- `이동식` 런타임 애플리케이션 환경
- `불변의 단일 아티팩트`에 애플리케이션 및 종속성 패키지화
- 서로 다른 종속성을 가진 여러 애플리케이션 버전을 `동시에 실행`
- 개발 및 배포 주기 단축
- 리소스 활용도 및 효율성 향상

### 애플리케이션 환경 구성 요소

런타임 엔진, 코드, 설정, 종속성         

### 컨테이너와 도커의 이점

- 어디서나 안정적으로 실행
- 동시에 다른 앱 실행

## 마이크로서비스의 특징

- 분산되고 진화적인 설계
- 효율성 낮은 파이프, 스마트한 엔드포인트
- 프로젝트가 아닌 독립 제품
- 장애 대비 설계
- 일회성
- 개발 및 프로덕션 패리티

## 컨테이너 오케스트레이션 도구

컨테이너 관리, 확장 및 배포를 위한 프레임워크

## 컨테이너 기술

1. 오케스트레이션 도구 선택 : Amazon ECS, Amazon EKS
2. 실행 타입 선택 : EC2, Fargate

ECS : 강력한 단순성     
규모 있게 컨테이너를 실행하는 AWS가 제안하는 방법       
규모 또는 기능을 희생하지 않고 의사 결정 감소       

- 컨테이너 레벨 네트워킹
- 고급 작업 배치
- AWS 플랫폼과의 긴밀한 통합
- Amazon ECS CLI
- 국제적 입지
- 강력한 스케쥴링 엔진
- 자동 조정
- Amazon CloudWatch 지표
- 로드 밸런서

EKS : 열린 유연성       
AWS에 최적화 된 Kubernetes로 민첩성과 효율성을 확보하고 모든 곳에서 작업을 표준화       
모든 Kubernetes 배포에서 관찰 가능한 보안과 고가용성        

- 컨테이너 레벨 네트워킹
- 완전관리형 etcd과 마스터들
- AWS 플랫폼과의 긴밀한 통합
- Kubernetes APIs
- Kubernetes 에코시스템
- 시기 적절한 업그레이드
- 고가용성 마스터들
- 인증된 Kubernetes

AWS Fargate : 온디맨드 컨테이너

- 인프라스트럭쳐 없음
- 컨테이너 수준에서 모든 것을 관리
- 빠르게 실행되고 확장이 용이
- 리소스 기반 요금
- 프로비저닝, 확장 또는 관리 할 EC2 인스턴스 없음
- 원활하게 확장 및 축소

Amazon ECR

- AWS 플랫폼과의 긴밀한 통합
- Amazon ECS 및 Docker CLI와 통합
- 확장 가능하고 고가용성
- 100% 클라우드 기반 도커 컨테이너 레지스트리
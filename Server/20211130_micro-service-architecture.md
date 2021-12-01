



## MSA(Microservice Architecture)

- 경량화되고 독립적인 여러 개의 서비스를 조합하여 애플리케이션을 구현하는 방식
- 서비스마다 자체 데이터베이스를 가지고 동작
  - 개발부터 개발부터 빌드, 배포까지 효율적으로 수행 가능
  - 개발과 유지관리에 소요되는 시간과 비용을 줄일 수 있어 활용도가 높음
- 낮은 결합도와 높은 결집도(Loose Coupling, High Cohesion)
- 상호 의존없이 단일 기능을 수행



## Monotholic Architecture(모놀리식 아키텍처)

- 전통적인 아키텍쳐 스타일

- 하나의 서버에 모든 비즈니스 로직이 들어가 있는 형태 (통서버)
- 하나의 중앙 집중화된 데이터베이스에 모든 데이터가 저장됨
- 장점
  - 개발과 관리가 용이하다는 점
  - 기술 단일화
- 단점
  - 여러개의 기술을 혼용해서 사용하기 어렵다.
  - 배포 및 재기동 시간이 오래 걸린다.
  - 수정에 용이하지 않음 (타 컴포넌트 의존성)
- 시스템 규모가 작을 때는 
- 시스템 규모가 커질 경우 복잡도도 증가해 코드의 이해와 분석이 어려워지고 작은 수정사항에도 전체를 빌드, 배포해야 하는 비효율이 발생한다.
  - 개선과 확장이 어려워진다.



## Microservices Concerns

![img](../../Library/Application Support/typora-user-images/Screen%2BShot%2B2016-12-03%2Bat%2B09.32.38.png)

![img](../../Library/Application Support/typora-user-images/Screen%2BShot%2B2016-11-30%2Bat%2B08.45.11.png)

### 참고

https://www.samsungsds.com/kr/insights/1239180_4627.html

https://dzone.com/articles/deploying-microservices-spring-cloud-vs-kubernetes

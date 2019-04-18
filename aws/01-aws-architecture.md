# Architecuture

- 다음 내용은 AWS SUMMIT Seoul 2019에서 들은 내용을 정리한 것이다.

AWS에는 다양한 서비스가 존재한다. AWS 클라우드에서 아키텍쳐를 구성할 때 가장 중요한 것은 '시스템을 어디에 올릴 것인가?'이다.

EC2(Elastic Compute Cloud)에는 여러 종류의 인스턴스가 존재한다.

서버 사양을 정해보자. 아래 예시의 서버 사양은 어떤 서버인가?

```
 M5d.xlarge
```

M: instance family

5: instance의 세대

d: 추가 기능

xlarge: instance의 크기

약 175개의 인스턴스가 존재(2019.04.18 기준)하며, 제공된다. 175개의 인스턴스 중에 본인에게 맞는 인스턴스는 분명히 존재한다.

---

AWS에는 아래와 같은 유형의 [Elastic Load Balancing](https://docs.aws.amazon.com/elasticloadbalancing/index.html)이 존재한다.

> Application Load Balancer

- Application Layer인 Layer7에서 작동한다.

> Network Load Balancer

- 주로 Layer4에서 작동한다.

> Classic Load Balancer

---

스토리지 선택하기

> EBS(Elastic Block Store)

- EC2에 instance를 생성하면 기본으로 붙어있는 것!

- instacne가 날아가면 같이 사라지게 된다.(휘발성)

  이러한 휘발성은 [snapshot](https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/ebs-creating-snapshot.html)과 같은 백업기능으로 방지할 수 있다.

- SSD와 HDD 타입으로 나눠져있다.

> S3

- REST 방식으로 사용하는 저장장치. 5테라만 넘지 않으면 모든 파일을 처리할 수 있다.

- 버킷 단위로 접근 제어를 걸수 있다.

  버킷이란? 디렉토리 개념으로 이해하면 쉬울 것 같다. '여행'버킷에는 여행에 대한 파일만 저장, '야구'버킷에는 야구 관련 파일만 저장하는 방식으로 사용하면 될것 같다. 버킷을 무한정 생성할 수 있다.

- 기본적으로 [암호화](https://docs.aws.amazon.com/ko_kr/AmazonS3/latest/dev/bucket-encryption.html) 기능을 제공하기에 설정하면 된다.

* 글로벌 기능을 제공하는 서비스에서는 S3를 이용하면 Region간의 싱크를 맞출 수 있다. 즉, 서울 리젼에서 올린 데이터를 뉴욕 리젼에 싱크를 맞추게 되면 뉴욕에서 서비스를 이용하는 사람은 보다 빠르게 파일을 받을 수 있다.

* [Athena](https://aws.amazon.com/ko/athena/)를 이용하면 S3의 데이터를 쉽게 불러올 수 있다.

* S3의 [Life Cycle](https://docs.aws.amazon.com/ko_kr/AmazonS3/latest/user-guide/create-lifecycle.html)을 이용하면 Standard-IA(Infrequent Access), One Zone-IA 및 Glacier 스토리지 클래스로 옮기는 규칙을 정의해 수명 주기 규칙을 구성할 수 있다.

> EFS(Elastic File System)

- 용량이 탄력적으로 적용된다

---

VPC(Virtual Private Cloud)

가상 네트워크 서비스를 뜻하며, 여러개의 VPC를 만들어서 사용할 수 있다. 서로 통신하는 대역끼리는 ip가 다르면 안된다. 여러개의 VPC가 통신하기 위해서는 [라우팅 테이블](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/VPC_Route_Tables.html)이 필요하다. 하나의 subnet은 하나의 VPC를 보유한다.

> VPC를 만들기 위해서는?

1. ip주소 대역을 선정하고

2. subnet을 생성하고

3. 라우팅 테이블을 생성하고

4. 방화벽을 설정하면 된다.

   - 방화벽은 AWS에서 [Security Group](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/VPC_SecurityGroups.html)을 제공한다.

---

Database

AWS에서 제공하는 RDS를 사용하면 우리는 개발에 집중할 수 있다. AWS에서 Application 최적화를 제외한, auto scaling, 고가용성 구성, 백업 및 복구, DB 패치, OS 구성 등을 전부 처리해준다.

고가용성을 확보하기 위해 AWS에서는 Standby 서버를 갖고 있는데, 이 서버는 AWS가 위기 상황에 위험을 감지했을 경우 서비스의 DB 접속 정보를 바꿔도 계속해서 서비스를 사용할 수 있을 정도의 상태를 갖고 있다.

또한, DB에 트래픽을 방지하기 위해 지금까지는 읽기 전용 DB를 구성해서 사용해왔지만 AWS에서 [Read Replica](https://aws.amazon.com/ko/rds/details/read-replicas/)를 활용하면 보다 쉽게 트래픽을 분산할 수 있다.

---

AWS를 사용하는 방법

1. AWS console

2. [Command Line Interface](https://aws.amazon.com/ko/cli/)

3. SDK

   - Java, python, Javascript 등의 SDK를 사용하면 된다.

   - [node.js 전용 SDK](https://aws.amazon.com/ko/sdk-for-node-js/)

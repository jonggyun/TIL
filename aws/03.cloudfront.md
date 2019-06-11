# CloudFront

CloudFront는 AWS에서 제공하는 CDN서비스이다.

> CDN이란 무엇인가?

CDN은 Content Delivery Network의 약자이다. 내용을 배달해주는 네트워크?? 이게 무엇이란 말인가?

다른 말로, 세계 곧곧 흩어져있는 사용자들이 지리적으로 가까운 곳으로 부터 콘텐츠를 제공받는 것을 말한다. 여기서 지리적으로 가까운 곳은 CloudFront가 보유하고 있는 166개의 PoP(Point of Presence)를 말한다.

이러한 CDN은 왜 필요한가?

거리가 멀수록 혹은 데이터의 양이 많을 수록 먼거리 전송 성능이 저하되는 것은 당연하다. 이러한 문제를 해결하기 위해 CDN이 나타난 것이다.

> CloudFront의 기능

- Static Content Delivery

  - 정적 파일이기 때문에, 원본이 그대로 전송된다. 이렇게 전송된 원본은 캐싱 기능을 바탕으로 보다 빠르게 접근할 수 있도록 도와준다.

  - 정적 파일의 경우 반복적으로 접근하는 것이기 때문에 캐싱을 하면 훨씬 유용하다.

  - front-end에서 개발한 내용인 js, css 등의 정적 파일을 CloudFront로 연결하면 서비스를 보다 빠르게 사용할 수 있다.

* Dynamic Content Delivery

  - 매번 파일이 변경되기 때문에 오리진과 성능 차이가 나지 않는다.

  - 이러한 문제를 해결하기 위해 전송 기능을 향상시켰다.

    1. 최적의 엣지에 연결

    2. 오리진과 지속적으로 연결

    3. 네트워크의 최적화

    4. Gzip방식을 통한 압축 최적화

  - 일반적으로 Connection은 3way handshake로 전달된다. CloudFront에서는 3way handshake를 최초 설정 이후 다시 설정하는 등의 방식을 건너뛰기 때문에 빠르게 전송할 수 있는 상태를 유지한다.

    - 3way handshake는 client와 server과 통신을 할 때 client에서 synchronize sequence number를 전송하면 server에서 synchronize sequence number와 acknowledgement를 다시 client에게 전송한다. ack 신호를 받은 client는 server에 ack를 보내면서 Connection이 성립되는 것이다.

  - Gzip 압축 방식은 보통 1kb ~ 10mb정도의 사이즈를 유지하기 때문에 빠르게 전송할 수 있는 것이다.

    - 모든 파일이 Gzip으로 압축되는 것이 아니기 때문에 주의해야한다.

    - [Gzip 지원 타입](https://docs.aws.amazon.com/ko_kr/AmazonCloudFront/latest/DeveloperGuide/ServingCompressedFiles.html)

* SSL 기능 제공

  - Browser -> https -> cloudfront -> http -> webserver

* S3 업로드에 가속 기능

  - [accelerate endpoint](https://docs.aws.amazon.com/ko_kr/AmazonS3/latest/dev/transfer-acceleration.html)를 사용하면 S3를 사용하는 속도가 향상된다.

> CloudFront 활용방안

CloudFront + S3

CloudFront + ec2

CloudFront + route53

CloudFront + media service

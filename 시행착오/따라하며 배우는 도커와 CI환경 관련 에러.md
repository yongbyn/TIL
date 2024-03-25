> [따라하며 배우는 도커와 CI환경](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-%ED%95%B5%EC%8B%AC%EC%9B%90%EB%A6%AC-%ED%99%9C%EC%9A%A9/dashboard)관련 시행착오를 정리한 내용입니다.


## buildkit false 에러(Win 10)
내컴퓨터 → 속성 → 고급 시스템 설정 → 고급 → 환경 변수  → 시스템 변수에서
새로 만들기 클릭 → 변수 : DOCKER_BUILDKIT  값 : 0 입력하면 에러 해결
ref) https://github.com/docker/docs/pull/17635

## docker-compose up 에러
아래 링크 따라서 한 후 docker-compose up —build 하면 에러 해결
(노드 버전때문인 것 같은데 정확한 원인은 모르겠음..)
ref) https://www.inflearn.com/course/lecture?courseSlug=따라하며-배우는-도커-ci&unitId=52120&category=questionDetail&tab=community&q=804213

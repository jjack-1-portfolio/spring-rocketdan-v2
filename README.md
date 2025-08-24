# Spring Boot 기반 구인구직 플랫폼 → RESTful 자원 서버로 전환

<h2>RocketDan</h2>

> 기존에 웹 화면 중심으로 구현된 ‘Spring Boot 기반 구인구직 플랫폼’을 프론트엔드-백엔드 완전 분리 구조의 RESTful API 서버로 재구성한 프로젝트입니다.
> Spring REST Docs를 통해 API 문서를 자동 생성하여, API 명세 관리와 유지보수 효율성을 높였으며, JWT 기반 인증, 예외 처리 구조 고도화, 테스트 기반 개발까지 적용하여 실제 서비스 수준의
> 백엔드 아키텍처 설계 및 구현 경험을 목표로 삼았습니다.

## 프로젝트 시연영상

<video src="https://github.com/user-attachments/assets/0dbbb461-fc7e-40e3-863a-9d27123c53a5" controls width="600"></video>

## 목차

1. [🗓️ 개발 기간 및 참여 인원](#개발기간및참여인원)
2. [🔚 회고](#회고)
3. [📄 API 문서](#API문서)
4. [💡 주요 기능](#주요기능)
5. [✍️ 개인 기여도 및 역할](#개인기여도)
6. [👥 팀원](#팀원)
7. [🛠️ 기술 스택](#기술스택)
8. [🧩 문제 해결 경험](#문제해결경험)
9. [📋 ERD](#erd)

<a id="개발기간및참여인원"></a>

## 🗓️ 개발 기간 및 참여 인원

- 기간: 2025.05.12 ~ 2025.05.22
- 인원: 5인 팀 프로젝트

<a id="회고"></a>

## 🔚 회고

**1️⃣ 리팩토링의 어려움**

두 번째 프로젝트는 첫 번째의 REST API 전환이기 때문에 리팩토링을 하는 부분이 많았다

첫 번째 프로젝트에 작성된 코드를 가지고 REST API 로 리팩토링을 하는데 다른 팀원이 작성한 코드를 리팩토링을 해야하는데 코드가 너무 복잡하게 꼬여있어서 분석하는데 어려움이 있었다. 해당 부분을 수정할 때
작성한 팀원에게 가서 각 부분의 로직을 설명하고 지금 작성된 부분이 필요한지 물어보고 수정하였다

이 과정에서 무분별하게 작성된 DTO를 API 목적에 맞게 재분류하고, DTO-엔티티 변환 로직을 서비스 계층에서 분리하여 가독성을 높였다

또한, 이번 프로젝트를 통해 JPA의 활용도를 한 단계 끌어올렸다**.** 기존에 성능 저하의 원인이었던 N+1 문제를 패치 조인(Fetch Join)을 활용해 최적화하는 방법을 배웠고, 이를 팀원들에게 공유하며
협업의 효율을 높였다

리팩토링을 하면서 첫 번째 프로젝트 때 컨벤션을 더 잘 지켜서 만들었다면 빠르게 REST 전환이 됐을 것이라 느꼈다. 그리고 JPA 에 대해서 좀 더 공부를 하게 되었다. JPA 를 더 잘 활용하여 코드를 더
깔끔하게 작성하는 방법을 배우게 되었다. JPA 활용이 어려운 팀원에게 설명해주면서 사용을 권유하였다

다음 프로젝트부터는 유지보수성이 높은 설계를 위해 디자인 패턴을 적극적으로 공부하고 적용할 계획이다

<a id="API문서"></a>

## 📄 API 문서

![api1](docs/images/api1.png)

![api2](docs/images/api2.png)

![api3](docs/images/api3.png)

<a id="주요기능"></a>

## 💡 주요 기능

### 👤 개인

- 회원가입 / 로그인 / 로그아웃 / 회원정보 수정 (REST API 설계 및 문서화)
- 채용공고 상세 조회 및 이력서 지원 API
- 이력서 등록 / 수정 / 삭제 API
- 지원 내역 / 스크랩 공고 마이페이지 API
- 합불 여부 결과 확인 API

### 🏢 기업

- 회원가입 / 로그인 / 로그아웃 / 기업 정보 수정 API
- 채용공고 등록 / 수정 / 조회 API
- 지원자 이력서 열람 / 스크랩 / 합격 여부 처리 API

<a id="개인기여도"></a>

## ✍️ 개인 기여도 및 역할

| 구분   | 기능명           | 설명                                                                                      |
|------|---------------|-----------------------------------------------------------------------------------------|
| (공통) | 회원 정보         | 회원 정보에 대한 상세보기(READ), 등록(CREATE), 수정(UPDATE) 기능 구현. 응답 DTO 설계 및 매핑                      |
| (기업) | 기업 회원의 공고 정보  | 기업이 작성한 공고 정보에 대해 상세보기(READ), 등록(CREATE), 수정(UPDATE) 기능 구현. 응답 DTO 설계 및 맵핑              |
| (개인) | 개인 회원의 공고 북마크 | 공고에 대한 북마크를 상세보기(READ), 등록(CREATE), 삭제(DELETE) 기능 구현. 응답 DTO 설계 및 맵핑                    |
| (개인) | 개인 회원의 이력서 정보 | 개인이 작성한 이력서 정보에 대해 상세보기(READ), 작성(CREATE), 수정(UPDATE), 삭제(DELETE) 기능 구현. 응답 DTO 설계 및 맵핑 |
| (개인) | 개인 회원의 공고 지원  | 개인이 공고에 지원하는 것에 대해 상세보기(READ), 등록(CREATE). 응답 DTO 설게 및 맵핑                               |

<a id="팀원"></a>

## 👥 팀원

| 이름  | 역할 | GitHub                                       |
|-----|----|----------------------------------------------|
| 최재원 | 팀장 | [@jjack-1](https://github.com/jjack-1)       |
| 김건우 | 팀원 | [@GUNWO0](https://github.com/GUNWO0)         |
| 김세리 | 팀원 | [@roni243](https://github.com/roni243)       |
| 이연호 | 팀원 | [@yh88888888](https://github.com/yh88888888) |
| 조하은 | 팀원 | [@TaengGyul](https://github.com/TaengGyul)   |

<a id="기술스택"></a>

## 🛠️기술스택

<table>
  <tr>
    <td align="center"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/java/java-original.svg" width="50"/><br/>Java</td>
    <td align="center"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/spring/spring-original.svg" width="50"/><br/>Spring Boot</td>
    <td align="center"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/sqlite/sqlite-original.svg" width="50"/><br/>H2</td>
    <td align="center"><img src="https://cdn-icons-png.flaticon.com/512/337/337946.png" width="50"/><br/>Spring REST Docs</td>
    <td align="center"><img src="https://jwt.io/img/pic_logo.svg" width="50"/><br/>JWT</td>
  </tr>
</table>

## 🧰 개발 환경

<table>
    <tr>
        <td align="center"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/intellij/intellij-original.svg" width="50"/><br/>IntelliJ</td>
    </tr>
</table>

## 🤝 협업 도구

<table>
    <tr>
        <td align="center"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/git/git-original.svg" width="50"/><br/>Git</td>
        <td align="center"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg" width="50"/><br/>GitHub</td>
        <td align="center"><img src="https://upload.wikimedia.org/wikipedia/commons/4/45/Notion_app_logo.png" width="50"/><br/>Notion</td>
        <td align="center"><img src="https://upload.wikimedia.org/wikipedia/commons/7/76/Slack_Icon.png" width="50"/><br/>Slack</td>
    </tr>
</table>

<a id="문제해결경험"></a>

## 🧩 문제 해결 경험

### 💬 문제 : 통합 테스트 시 테이블 id 자동 생성 문제

**[공고 등록]**

![p1](docs/images/p1.png)

**[공고 수정]**

![p2](docs/images/p2.png)

- **문제 상황**
    - h2 db 에 더미를 넣어 놓은 상태에서 공고 등록 테스트, 공고 수정 테스트를 각각 진행하면 문제가 없었다
    - 공고에 대한 모든 컨트롤러 테스트를 만들고 **통합으로 실행**을 했을 때, **ID 자동 증가(Auto Increment) 문제**가 발생했다
- **원인 분석**
    - 공고를 등록하거나 수정할 때 공고의 기술 스택 목록을 전부 삭제하고 다시 등록을 하는데 공고 기술 스택 테이블의 **자동 증가가 롤백 되지 않아서 문제**가 생겼다
    - 공고 기술 스택 테이블은 계속 삭제되고 생성되는 과정을 반복하는데 **id 자동 증가 시퀀스**가 초기화 되지 않고 다음 테스트 진행에도 영향을 미친 것 같다
- **해결 방법**:
    - 테스트 진행 전에 id 자동 증가 시퀀스를 고정하는 방법을 사용하였다
      ![p3](docs/images/p3.png)
    - 새로 생성될 때 항상 고정된 id 시퀀스로 시작되기 때문에 문제가 해결되었다
    - 다음 해결 방법은
        - @DirtiesContext(classMode = DirtiesContext.ClassMode.BEFORE_EACH_TEST_METHOD) 를 사용하는 것이다
        - **각 테스트 메서드가 실행되기 전에** 스프링 애플리케이션 컨텍스트를 다시 로드한다
        - data.sql의 더미 데이터가 처음부터 다시 로드되고, 시퀀스 값도 초기 상태로 완벽하게 리셋 하기 때문에 매번 테스트를 진행할 때 db 를 독립적으로 초기화 할 수 있다
    - 두 방법 중에서 시퀀스 고정을 사용한 이유는 더미 데이터와 로직 진행이 어떻게 되는지 알고 있는 상황에선 매번 테스트마다 컨텍스트를 초기화 약간 오래 걸리는 작업을 하지 않아도 테스트가 잘 되었다는 것을
      알 수 있기 때문이다
    - 만약 더미 데이터와 로직을 잘 모른다면 컨텍스트를 초기화 하는 방법이 더 좋을 수 있다

<a id="erd"></a>

## 📋 ERD

![table](docs/images/table.png)
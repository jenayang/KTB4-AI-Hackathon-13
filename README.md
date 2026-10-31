<a id="readme-top"></a>

<!-- PROJECT SHIELDS -->
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]

<!-- PROJECT LOGO -->
<br />
<div align="center">
  <h3 align="center">JustDO</h3>

  <p align="center">
    AI가 계획의 부담을 줄이고, 매일의 실행을 퍼즐로 보여주는 목표 실행 지원 서비스
    <br />
    <a href="./docs/SERVICE_PLANNING.md"><strong>서비스 기획 보고서 요약 »</strong></a>
    <br />
    <br />
    <a href="#시연-영상">View Demo</a>
    &middot;
    <a href="https://github.com/jenayang/KTB4-AI-Hackathon-13/issues/new?labels=bug">Report Bug</a>
    &middot;
    <a href="https://github.com/jenayang/KTB4-AI-Hackathon-13/issues/new?labels=enhancement">Request Feature</a>
  </p>
</div>

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#시연-영상">시연 영상</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>

<!-- ABOUT THE PROJECT -->
## About The Project

**JustDO**는 "목표는 세웠는데 왜 실행은 멈출까?"라는 질문에서 출발한 목표 실행 지원
서비스다. 사용자는 목표를 한 문장으로 말하면 끝 — AI가 되물어 세부 정보를 모으고,
실행 가능한 날짜별 작업으로 계획을 쪼개준다. 매일 작업을 완료하면 퍼즐 한 조각이
채워지고, 누적된 실행은 랭킹으로 이어진다.

- 사용자는 **목표와 실행**에만 집중한다 — 계획 작성 · 등록의 부담은 AI가 맡는다.
- AI 초안은 사용자가 **확인 · 수정한 뒤에만 확정**된다 — 자동화는 통제권을 빼앗지 않는다.
- 일정이 밀려도 실패로 보지 않는다 — 남은 기간과 작업량 기준으로 **다시 분배**한다.

왜 이 문제를 풀기로 했는지(설문 데이터, 경쟁 서비스 포지셔닝, 서비스 원칙, 출시 후
검증 지표)는 [`docs/SERVICE_PLANNING.md`](./docs/SERVICE_PLANNING.md)에 정리했다.

KTB4-AI-Hackathon-13(13조) 팀 프로젝트로, AI · 풀스택 · 클라우드 담당이 함께
2026-08-19~20 이틀간 만들고 08-21에 발표했다.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Built With

* [![FastAPI][FastAPI.com]][FastAPI-url]
* [![SpringBoot][SpringBoot.com]][SpringBoot-url]
* [![React][React.js]][React-url]
* [![Vite][Vite.com]][Vite-url]
* [![TailwindCSS][TailwindCSS.com]][TailwindCSS-url]
* [![MySQL][MySQL.com]][MySQL-url]
* [![AmazonAWS][AWS.com]][AWS-url]

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- GETTING STARTED -->
## Getting Started

이 저장소는 세 서비스(`ai`, `backend`, `frontend`)를 하나로 모은 모노레포다. 각
팀원이 따로 개발하던 레포를 제출 시점에 합쳤다(`git log` 참고 — `Add 'ai/' from
commit ...` 형태의 커밋들).

```
frontend (React 19 + Vite + Tailwind)
        │  axios
        ▼
backend (Spring Boot + JPA + MySQL, S3)
        │  서버-서버 호출
        ▼
ai (FastAPI, 무상태 추론 서버)
```

### Prerequisites

* Node.js (버전은 `frontend/.nvmrc` 참고)
* JDK (버전은 `backend/build.gradle` 참고) + MySQL
* Python 3.11+
* 각 서비스 `.env.example`에 정의된 키(카카오 OAuth, AWS S3, LLM 프로바이더 등)

### Installation

1. 레포 클론
   ```sh
   git clone https://github.com/jenayang/KTB4-AI-Hackathon-13.git
   cd KTB4-AI-Hackathon-13
   ```
2. 세 서비스를 각각 띄운다 — 자세한 단계는 서브디렉토리 README/`.env.example` 참고:

   | 디렉토리 | 역할 | 실행 방법 |
   |---|---|---|
   | [`ai/`](./ai) | 목표 분석 · 계획 생성/수정 대화를 처리하는 무상태 LLM 추론 서버 | `ai/README.md` |
   | [`backend/`](./backend) | 인증, 캘린더/퍼즐/랭킹 상태 저장, AI 서비스 오케스트레이션 | `cd backend && ./gradlew bootRun` |
   | [`frontend/`](./frontend) | 목표 입력, 채팅 UI, 퍼즐 · 랭킹 화면 | `cd frontend && npm install && npm run dev` |

   세 서비스 모두 `docker-compose.yml`을 포함하고 있어 컨테이너로도 띄울 수 있다.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- USAGE EXAMPLES -->
## Usage

1. 목표를 한 문장으로 입력한다. (예: "10km 마라톤 완주")
2. AI가 기간 · 현재 수준 · 가능한 요일 등을 자연어로 되묻는다.
3. AI가 날짜별 실행 작업으로 계획 초안을 만들면, 사용자가 확인 · 수정 후 확정한다.
4. 매일 작업을 완료할 때마다 퍼즐 한 조각이 채워지고, 누적 결과가 랭킹에 반영된다.
5. 일정이 밀리면 대화로 "강도를 낮춰줘" 같은 수정 요청을 할 수 있고, 서비스가 남은
   기간 기준으로 다시 계획을 분배한다.

실제 동작은 아래 시연 영상에서 확인할 수 있다.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 시연 영상

<!--
  GitHub는 리포지토리에 커밋된 동영상 파일(수십 MB 이하)도 <video> 태그로 바로 재생해준다.
  이 README는 영상 파일 자체를 git에 커밋하지 않은 상태로 유지한다 — 아래 경로/파일명에
  맞춰 영상을 추가(`git add "13조_동영상.mp4"`)하면 임베드가 바로 재생된다.
  YouTube 등 외부에 올린 링크를 쓰고 싶다면 <video> 블록을 아래처럼 바꾸면 된다:
  [![시연 영상](썸네일.png)](https://youtu.be/xxxxxxxx)
-->

<video src="13조_동영상.mp4" controls width="720">
  브라우저가 비디오 태그를 지원하지 않으면 아래 링크에서 직접 다운로드해서 재생하세요.
</video>

▶ [시연 영상 다운로드 (13조_동영상.mp4)](./13조_동영상.mp4)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- ROADMAP -->
## Roadmap

- [x] 작업 완료 시 퍼즐 조각 지급
- [x] 작업 추가 후 퍼즐 다시 열기 · 중복 지급 방지
- [x] 전체 · 카테고리 랭킹
- [ ] AI 목표 분석 및 질문 템플릿
- [ ] 날짜별 계획 초안 생성 · 사용자 피드백 기반 수정
- [ ] 확정 계획 자동 등록
- [ ] 자동 리스케줄링 (최우선 — 설문에서 가장 큰 이탈 원인에 직접 대응)
- [ ] 변경 이력(AI 수정 전후 비교 · 되돌리기)
- [ ] 계획 템플릿 (반복 목표의 시작 비용 절감)

우선순위를 정한 근거와 출시 후 검증 지표는 [`docs/SERVICE_PLANNING.md`](./docs/SERVICE_PLANNING.md)
참고.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- CONTRIBUTING -->
## Contributing

KTB4-AI-Hackathon-13(13조), 총 6명 — AI 2명 · 풀스택 2명 · 클라우드 2명이 이틀간
기획부터 구현까지 함께했다. 각 서비스의 상세한 담당/작업 로그는 서브디렉토리별 git
히스토리와 `ai/docs/`의 설계 문서에 남아있다.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- LICENSE -->
## License

해커톤 제출용 프로젝트로 별도 라이선스를 지정하지 않았다.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- CONTACT -->
## Contact

Project Link: [https://github.com/jenayang/KTB4-AI-Hackathon-13](https://github.com/jenayang/KTB4-AI-Hackathon-13)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- ACKNOWLEDGMENTS -->
## Acknowledgments

* [서비스 기획 보고서 — 읽기 쉬운 버전](./JustDO_서비스기획보고서_읽기쉬운버전.pdf) / [원본](<./서비스기획보고서 (1).pdf>)
* [Best-README-Template](https://github.com/othneildrew/Best-README-Template) — 이 README의 구조를 참고했다.
* [Img Shields](https://shields.io)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- MARKDOWN LINKS & IMAGES -->
[contributors-shield]: https://img.shields.io/github/contributors/jenayang/KTB4-AI-Hackathon-13.svg?style=for-the-badge
[contributors-url]: https://github.com/jenayang/KTB4-AI-Hackathon-13/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/jenayang/KTB4-AI-Hackathon-13.svg?style=for-the-badge
[forks-url]: https://github.com/jenayang/KTB4-AI-Hackathon-13/network/members
[stars-shield]: https://img.shields.io/github/stars/jenayang/KTB4-AI-Hackathon-13.svg?style=for-the-badge
[stars-url]: https://github.com/jenayang/KTB4-AI-Hackathon-13/stargazers
[issues-shield]: https://img.shields.io/github/issues/jenayang/KTB4-AI-Hackathon-13.svg?style=for-the-badge
[issues-url]: https://github.com/jenayang/KTB4-AI-Hackathon-13/issues
[FastAPI.com]: https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white
[FastAPI-url]: https://fastapi.tiangolo.com/
[SpringBoot.com]: https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white
[SpringBoot-url]: https://spring.io/projects/spring-boot
[React.js]: https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB
[React-url]: https://reactjs.org/
[Vite.com]: https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white
[Vite-url]: https://vitejs.dev/
[TailwindCSS.com]: https://img.shields.io/badge/Tailwind%20CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white
[TailwindCSS-url]: https://tailwindcss.com/
[MySQL.com]: https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white
[MySQL-url]: https://www.mysql.com/
[AWS.com]: https://img.shields.io/badge/AWS%20S3-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white
[AWS-url]: https://aws.amazon.com/s3/

# vulpes-harness

[English](README.md) | [한국어](README.ko.md)

Claude Code나 Codex 같은 AI 코딩 도구에 기획 작업용 반복 명령을 더해 주는 하니스.

요구사항과 기술 아키텍처를 일정한 규격으로 산출.

AI 도구에서 슬래시 명령을 실행하면 입력한 내용이 저장소의 Markdown 문서로 정리됨.

## 설치

프로젝트에 하니스를 한 번 추가 - [INSTALLATION.md](INSTALLATION.md) 참고.

## 사용법

- 한 번에 한 종류의 문서만 작업.
- 같은 작업은 기다리지 말고 그때그때 추가하거나 수정.
- 한 종류를 끝낸 뒤 다음으로 - 서로 다른 작업은 섞지 않음.

<img alt="작업 진행" src="assets/workflow.svg" width="80%">

- 요구사항: `/opsx:require {내용}`
- 아키텍처: `/opsx:architect {내용}`
- 작업 준비: `/opsx:propose {내용}`
- 실행: `/opsx:apply {내용}`

## 스키마

### require

요구사항 스키마. KAOS/GORE와 BABOK 기반.

비즈니스 요구사항, 목표/객체/책임/오퍼레이션 모델, 요구사항 종합본, 추적표를 산출.

### architect

아키텍처 스키마. Kruchten 4+1, arc42, ISO/IEC 42010, Nygard ADR, BABOK RTM 기반.

아키텍처 개요, 논리/프로세스/데이터/배포 뷰, 횡단 관심사, ADR, 설계 추적표를 산출.

### gdd

게임 디자인 스키마. 표준 GDD 구성 기반.

개요, 게임플레이, 메카닉, 세계관과 서사, 아트와 오디오 디렉션, UX/UI, 기술, 수익화, 프로덕션을 산출.

게임 프로젝트 전용.

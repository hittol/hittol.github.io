---
title: "Azure DevOps Learning-(1)"
excerpt: "Azure DevOps 기본 개념 정리"
date: 2025-12-18
categories: [CICD]
Tags: [CI/CD , AzureDevOps]
toc: true
toc_sticky: true
toc_label: "AzureDevOps"
sidebar_main: true
published: true
header:
   teaser: /assets/images/head_baner.jpg
---


# Azure DevOps Learning --- ( 1 )

---

---

## DevOps

### ● 개념

▶ 소프트웨어 개발(Dev), 개발 및 IT 운영 (Ops) 을 결합하는 일련의 사례로 개발 수명 주기를 단축하고

고품질 소프트웨어의 지속적인 제공을 보장하는 것을 목표로 한다.

### ● 원칙

1. 공유 계획

2. 공유 코드 베이스

3. 지속적인 통합

4. 테스트 기반 기술

5. 자동화된 제공 및 배포

### ● 자동화 측면에서 DevOps

1. 애플리케이션 수명 주기의 모든 것, 최소한 자동화할 수 있는 부분을 자동화하는 시도

2. 자동화된 빌드로 지속적 통합 또는 CI 프로세스의 핵심 구성 요소 역할

3. 공유 리포지토리에 대한 코드 통합을 자동화

4, 자동화된 배포 시도

5. 환경 프로비저닝 자동화

---

## Azure DevOps

### ● 개념

▶ 팀 워크플로를 개선하도록 설계된 별도의 클라우드 기반 도구 집합

### ● 접근 방법

1. Web Portal ( [https://dev.azure.com](https://dev.azure.com/) )

- 프로젝트 내 보드, 리포지토리 , 파이프라인, 테스트 계획 및 아티팩트에 액세스 가능

2. Command Line ( CLI )

- Azure 리소스를 만들고 관리하는 데 사용되는 명령 집합 제공

- Azure CLI 용 DevOps 확장 설치 필수

```java
az extenstion add --name azure-devops
```

3. Visual Studio & Visual Studio Code

- 개발 IDE 및 편집기를 통해 DevOps 서비스와의 통합 제공

○ 데모 생성기 (  [https://azuredevopsdemogenerator.azurewebsites.net/](https://azuredevopsdemogenerator.azurewebsites.net/)  )

- Azure DevOps 의 모든 부분을 확인할 수 있도록 샘플 데이터를 포함한 데모 프로젝트 생성

### ● 조직

- New Organization 을 선택해 새로운 조직을 생성

- 조직 이름이 URL 의 일부가 된다.

- 조직 블레이드 하단의 Organization Settings 를 통해 조직 설정으로 이동 가능

○ 조직 설정

- 한 조직의 모든 프로젝트에 적용되는 조직에 대한 기본 값을 설정

- 프로젝트, 사용자, 개인 정보 보호 , URL , 시간대 및 지역 설정 등…

### ● 초대

- Entra ID 를 사용하는 경우 디렉터리에서 조회 후 추가 가능

○ 초대 방법

1. 초대할 프로젝트에서 [Project Settings] - [Teams] 로 이동

2. New Team 선택 후 Members 혹은 기존의 Team 을 선택 후 Add 를 선택

3. 초대할 사용자의 메일 주소를 추가 후 Add

### ● 카테고리

1. Azure Borads
- 백로그, 팀 대시보드 및 사용자 지정 보고를 통해 Kanban 보드에 대한 작업을 추적
- 팀 간에 작업을 추적하거나 드래그 앤 드롭 스프린트 계획과 유연한 작업 항목 추적

1. Azure Pipelines
- 빌드, 통합 및 배포 프로세스를 자동화하는 서비스를 제공
- 여러 언어로 작동할 수 있는 CI/CD 시스템 제공 및 Github 또는 기타 Git 에서 인기 있는 소스 제어 시스템에서 코드를 가져올 수 있음
- Windows , MacOS, Linux 빌드 에이전트를 호스팅했으며 Visual Studio App Center 와의 통합으로 모바일 배포가 가능능

1. Azure Repos
- 소스 코드 리포지토리를 호스트 ( Git 지원 )

1. Azure Test Plans
- 애플리케이션에 대한 테스트 플랫폼을 제공
- 데스크톱 또는 웹 앱에서 테스트를 실행하여 애플리케이션, 브라우저에서 테스트 실행 및 품질 평가가

1. Azure Artifacts
- 코드 베이스의 종속성을 관리

---

## Azure Boards

### ● 목적

1. 프로젝트 수명 주기 동안 작업, 버그 및 사용자 스토리를 모니터링 및 관리 가능

2. Kanban 보드 및 대시보드를 사용해 Azure Boards 작업을 시각화하여 작업 항목의 상태와 진행,

상황을 추적 가능

3. 백로그 및 대시보드와 같은 작업을 구조화하고 우선 순위를 지정해 작업을 계획 및 구성

4. 스크럼을 간소화해 팀이 효율적으로 작업을 관리하고 커밋할 수 있도록 함.

5. 쿼리를 통한 차트를 대시보드에 추가해 프로젝트 상태 및 진행 상황 모니터링

### ● 기능

1. Work Items

- 사용자와 팀이 소프트웨어 프로젝트에서 완료해야 하는 작업 및 활동의 세부 정보를 설명하는 데 사용

- 모든 유형의 작업이나 활동 또는 작업을 나타내는 데 사용하는 작업 단위

○ 생성

1. New Work Item 선택

2. 작업 항목 유형 목록에서 원하는 유형 선택

- Epic : 하나의 공통된 목표를 가진 대규모 작업에 사용 ( 긴 타임라인 시 사용 )

- issue

- task : 수행해야 하는 실제 작업 추적에 주로 사용

3. Title 과 Description 에 제목과 설명을 작성

4. Details/Planning 에서 우선 순위,활동 종류 등 설정 가능

5. Related Work 에서 연결할 부모 링크 혹은 연결할 자식 링크를 선택/생성

6. Assigned People 를 통해 해당 Work Item 에 할당될 사람 지정

7.  Tag :  Work Item에 정의한 범주 별로 제품 백로그를 빠르게 확인하게 해줌

1. Boards

- kanban 보드를 사용해 작업 흐름을 시각화

- 모든 작업 항목을 보드의 카드에 배치해 전반적인 상태를 빠르게 확인 및 잠재적인 병목 현상 식별

- 카드로 표시되는 작업 영역 확인 가능

- `New Item` 을 통해 쉽고 빠르게 Work Item 생성

○ Settings

1. Cards

● Fields : 표시하거나 숨길 필드(Assigned To, Tag , Effort 등… ) 혹은 추가 필드 설정 가능

● Styles : 일련의 기준에 따라 카드의 배경색 변경 가능

![image_post1](/assets/images/DevOps/1/image-20250530-084533.png)

- `Add Styling Rule`을 통해 스타일 지정 규칙 추가

- field , Operator , Value 를 통해 원하는 규칙 설정 가능

- `Add Criteria` 를 통해 추가 규칙 설정 가능

● Tag Colors : 생성한 태그의 색상 설정 가능

2. Boards

● Columns : 새 열 추가 , 열 이름 변경, 열 위치 이동 등의 작업 가능

- `Split column into Doing and Done` 토글 활성화를 통해 한 열을 Doing 과 Done 으로 분할 가능

- 해당 열이 매핑되는 상태 ( To do / Doing ) 를 지정 가능

- `WIP 제한`을 통해 한 열에 등록할 수 있는 Work Item 수를 제한

다만, 직접적으로 옮기는 것을 제한하는 것이 아닌 한도 초과 여부 확인을 가능하게 해줌

● Swimlanes : Boards 에 행을 추가해 팀, 방식 등을 분리 가능

![image_post2](/assets/images/DevOps/1/image-20250530-084800.png)

- `Add swimlane` 을 통해 추가적인 행을 생성

1. Backlogs

- 작업하려고 하는 Work Items 에 대한 가시성을 제공하는 우선 순위가 지정된 작업 목록

1. Sprints

- 설정한 Sprint 별로 Work Items 의 Backlog , TaskBoard 등을 확인 가능

- 필터에서 원하는 Sprint 를 설정 가능

○ Sprint 지정

- Project Settings 의 [Boards] - [Project Configuration] 에서 Sprint 설정 가능

- 각 Sprint 별 시작 날짜 - 종료 날싸를 설정

1. Queries

- 사용자 지정 쿼리를 만들어 DashBoards 에서 사용자 지정 방식으로 Work Items을 볼 수 있음

- `New Queries` 를 통해 쿼리 생성 가능

![image_post3](/assets/images/DevOps/1/image-20250530-090128.png)

- Editor 에서 원하는 조건을 생성 후 Run Query 를 통해 쿼리 실행 테스트 가능

- Charts 를 통해 원하는 형태의 차트 생성 가능

![image_post4](/assets/images/DevOps/1/image-20250530-090618.png)

- Save 를 통해 공유 쿼리에 저장 필수 ( DashBoards 사용 시 반드시 **공유 폴더**에 저장 )

### ● DashBoards

- 팀의 진행 상황에 대한 가시성 확보 가능

- [Overview] - [DashBoards] 를 통해 확인 가능

- 위젯 또는 차트를 사용해 구성

- `Add Widget` 을 통해 Dashboard 에서 원하는 위젯들을 선택해 구성 가능

![image_post5](/assets/images/DevOps/1/image-20250530-091002.png)
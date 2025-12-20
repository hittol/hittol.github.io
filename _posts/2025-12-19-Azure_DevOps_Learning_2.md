---
title: "Azure DevOps Learning-(2)"
excerpt: "Azure DevOps 기본 개념 정리"
date: 2025-12-19
categories: [CI/CD]
Tags: [CI/CD , AzureDevOps]
toc: true
toc_sticky: true
toc_label: "AzureDevOps"
sidebar_main: true
header:
   teaser: /assets/images/azure_baner.jpg
---

## Azure Repos

### ● 목적

▶ 소프트웨어 개발 시 코드를 유지하고 관리하기 위해 사용

### ● 버전 제어

- 여러 개발자가 효율적으로 협업하고 시간이 지남에 따라 코드 베이스의 변경 사항을 추적 및 관리할 수 있도록 함
- 모든 수정 사항이 문서화 되어 문제 식별 및 해결이 용이함

### ● 구성

- Files
    
![image_post1](/assets/images/DevOps/2/image-20250508-042540.png)
    

- 파일 하위 페이지에서 저장소에 있는 모든 파일을 볼 수 있음

- History 에서 파일의 기록 , 누가 언제 커밋했는지 확인 가능

- Histroy 에서 원하는 커밋을 클릭 시 드릴다운을 통해 해당 커밋에 대한 세부 정보 확인 가능

- 직접 파일을 클릭해 온라인 편집기로 작업 가능

- Commits

- 코드를 분할하고 분기하는 경우 확인 가능 ( OFF 로 끌 수 있음 )

- Files 의 History 와 동일

- Push
    
![image_post2](/assets/images/DevOps/2/image-20250508-043005.png)
    

- Push 요청 및 세부 정보 확인 가능

- Branch

- 생성된 분기 정보 확인 가능

- Pull Requests

- 보류, 활성, 완료, 중단 된 Pull Request 에 대해 확인 및 작업 가능

### ● 사용 방법

**1. 레포지토리 생성**

![image_post3](/assets/images/DevOps/2/image-20250508-043534.png)

1-1. 해당 레포지토리 창을 선택해 New Repository 선택해 새 레포지토리를 생성

**2. Clone 생성**

<aside>
🗒️ IDE 에서 `Clone in VS Code` 를 통해 간단히 Clone 생성 및 VS Code 로 불러오기를 진행 가능

하위 방식은 Https URL 을 통해 생성하는 방법으로 진행

</aside>

2-1. 생성한 레포지토리의 Files 로 이동해 Clone 을 선택하여 URL 을 복사

![image_post4](/assets/images/DevOps/2/image-20250508-043815.png)

2-2. Windows Powershell 로 이동해 Clone 을 설치할 폴더로 이동

<aside>
⚠️ 해당 작업 전 반드시 컴퓨터에 Windows 용 Git 이 설치되어 있어야 합니다.

</aside>

![image_post5](/assets/images/DevOps/2/image-20250508-044032.png)

2-3. git clone ‘URL’ 을 입력해 해당 폴더에 클론 설치 확인 후 정상적으로 완료된 것 확인

![image_post6](/assets/images/DevOps/2/image-20250508-050046.png)

![image-20250609-065701.png](image-20250609-065701.png)

**3. Git Push**

![image_post7](/assets/images/DevOps/2/image-20250609-072303.png)

3-1. 해당 clone 파일에서 수정 사항 작성 후 저장

![image_post8](/assets/images/DevOps/2/image-20250609-065921.png)

3-2. 해당 폴더에서 **우클릭** - **터미널에서 열기** 클릭해 터미널 실행

![image_post9](/assets/images/DevOps/2/image-20250609-070036.png)

3-3. git branch 에서 현재 설정된 브랜치 확인

![image_post10](/assets/images/DevOps/2/image-20250609-070330.png)

- git branch [branch 이름] 을 통해 신규 branch 생성 후 git checkout [branch 이름] 으로 변경

혹은 , git checkout -b [branch 이름] 으로 신규 생성 후 이동

![image_post11](/assets/images/DevOps/2/image-20250609-070538.png)

3-4. git status 를 입력해 현재 git clone 디렉터리 내 파일 상태 확인

- git 에서 파일 상태는 Tracked ( 관리 대상 ) 과 Untracked (비관리대상 ) 으로 나뉜다.
- Tracked 파일만 파일 상태를 가짐짐

1. Untracked : git 이 파일을 추적하지 않아 새로 저장할 필요가 없는 파일

- 새로 생성되었으나 아직 git 에 추가되지 않은 파일

2. Modified : **Changes not staged for commit** 명단의 파일

- git 에 의해 추적되나 변경된 파일

3. Staged : git 에 의해 추적되며 변경된 파일이 Staging Area 에 추가된 파일

![image_post12](/assets/images/DevOps/2/image-20250609-071156.png)

3-5. git add 명령을 통해 변경 사항 및 Untracked 파일을 스테이징(Staging Area) 에 추가

1. git add [파일명] 으로 원하는 파일을 Staging area 로 보냄

2. git add . 로 현재 폴더 대상으로 git add 수행

![image_post13](/assets/images/DevOps/2/image-20250609-071337.png)

3-6. git commit 을 통해 `.git` 저장소의 branch 내에 Staging 파일 저장

- commit 전까지는 임시 저장 변경점으로 정식 Commit 에 포함되지 않는다.
1. git commit -m “메세지 이름” 을 통해 어떤 변화가 반영이 되었는지 설명

![image_post14](/assets/images/DevOps/2/image-20250609-072537.png)

3-7. git push 를 통해 Local 저장소에 있는 Commit 을 Remote 저장소로 업로드

- git push [remote url] [brench] 를 통해 PUSH
- 두 매개변수 미지정 시 기본적으로 Origin 을 원격 저장소, 현재 작업하는 브랜치를 PUSH 할 브랜치로 지정

![image_post15](/assets/images/DevOps/2/image-20250609-072916.png)

**4. Pull Request**

4-1. 업로드 한 Azure Repos 로 이동해 `Create a Pull Reqest` 요청 확인

![image_post16](/assets/images/DevOps/2/image-20250609-073443.png)

- 생성된 Pull Request 및 기록들은 Repos 블레이드의 Pull Requests 에서 확인 가능

![image_post17](/assets/images/DevOps/2/image-20250609-073741.png)

4-2. New Pull Request 에서 해당 정보 작성 후 Create

![image_post18](/assets/images/DevOps/2/image-20250609-073518.png)

1. Title

- pull request 의 제목

2. Description

- pull request 의 세부 내용

3. Reviewers

- pull request 를 승인할 검토자 지정

4. Work items to link

- boards 에 pull request 내용과 연관된 보드 선택

5. Tages

4-3. Create 시 Pull Request 생성. 해당 제목 , 설명 , Reviewers 검토 현황 , Comment 정보 확인 가능

![image_post19](/assets/images/DevOps/2/image-20250609-074207.png)

4-4. 검토자 승인 완료 시 Complete 를 눌러 Merge 진행

![image_post20](/assets/images/DevOps/2/image-20250609-074454.png)

## Azure Pipline

### ● 목적

- 애플리케이션 빌드 및 배포 단계를 자동화

### ● CI / CD

**1. CD ( Continuous Delivery , 지속적 전달 )**

- 소프트웨어가 언제든지 안정적이고 신속하게 프로덕션에 릴리스 될 수 있도록 함

- 철저히 테스트된 고품질 코드 또는 구성 요소를 가능한 빨리 배포해 프로덕션을 빠르고 효율적으로

상태로 유지하는 데 중점

- 최종 제품이 고객에게 제공되도록 하는 애플리케이션 배포를 자동화하는 프로세세스를 의미

○ 프로세스 ( Relase Pipline )

1. 스테이징 ( Stages )

- 빌드 파이프라인의 아티팩트로 시작

- 각 단계에서 고유한 배포 진행

2. 승인 ( Approvals )

3. 아티팩트 
        4. Release

- 자동 배포 설정 시 최종 배포 단계는 수동 개입 없이 수행

**2. CI ( Continuous Integration , 지속적 통합 )**

- 코드 변경 사항을 공유 리포지토리에 자주 병합하는 방식으로 자동화된 빌드 및 테스트가 실행되어

문제 조기 발견

- 자동화된 테스트를 통과하는 모든 코드 변경사항을 프로덕션 환경을 통해 배포해 소프트웨어가 항상

릴리스 가능한 상태로 유지

- 빌드 단계 후에 모든 코드 변경 사항을 테스트 , 또는 프로덕션 환경에 배포해 지속적 통합 보완

○ 프로세스 ( Build Pipline )

1. 트리거

- 파이프라인이 자동으로 최신 코드를 가져오고 YAML 파일 또는 클래식 편집기를 통해 정의된

빌드 프로세스를 실행함에 따라 트리거로 시작

2. 빌드

3. 테스트

- 코드 품질을 위한 테스트 진행 ( 단위 , 통합 등 … )

4. 아티팩트

- 애플리케이션의 배포 가능한 구성 요소 생성

- 컴파일된 코드 , 이진 파일 또는 빌드 중 생성된 파일을 포함할 수 있는 빌드 프로세스의 출력 의미

### ● 종류

![image_post21](/assets/images/DevOps/2/image-20250709-144922.png)

- 일반적으로 YAML 파일에서 Pipline 을 정의

**1. Agent**

- Pipline 의 중추 역할

- 작업이 실행되는 컴퓨팅 환경 ( 코드 확인 , 테스트 실행 및 결과 보고 같은 작업 수행 )

**2. Job**

- 에이전트에서 실행되며 일련의 단계 포

- 고유한 컨텍스트와 작업 공간이 있으므로 한 작업에서 생성된 변수와 파일은 다른 작업과 별도로 유지

**3. Stage**

- 개발 , 테스트 및 프로덕션과 같은 작업을 그룹화

**4. Step**

- 가장 작은 작업 단위

- 스크립트 실행 , 아티팩트 게시 또는 환경에 배포와 같은 작업 포함

**5. Tasks**

- Step 에 추가할 수 있는 미리 만들어진 스크립트 또는 확장

**6. Trigger**

- Pipline 을 실행하도록 지시

**7. Approval**

- 배포가 진행되기 전 게이트키퍼 역할

### ● 구성

![image_post22](/assets/images/DevOps/2/image-20250710-040143.png)

**1. Piplines**

- Build Pipline 확인 및 생성 가능

- 완료되면 Releases Pipline 이 실행되도록 트리거

**2. Environments**

- Piplines 의 배포의 대상이 될 수 있는 리소스의 모음

( ex ) Virtual Machine 의 클러스터 )

- 이름을 주로 dev , test , qa , staging , production 등으로 생성

### ● 사용 방법

**1. 구독 연결**

1-1.  project settings 에서 [**service connections**] 선택 후 Create Service Connections 선택

![image_post23](/assets/images/DevOps/2/image-20250710-042843.png)

1-2. Azure Resource Manager 클릭 후 사진과 같이 연결할 구독 , 리소스 그룹 지정 및

Service Connection Name 지정 후 모든 파이프라인에 대한 엑세스 권한 부여 옵션 선택

![image_post24](/assets/images/DevOps/2/image-20250710-043110.png)

1-3. 생성된 Service Connect확인

![image_post25](/assets/images/DevOps/2/image-20250710-043522.png)

**2. Build Pipline 생성**

2-1. Piplines - Create Piplines 선택

![image_post26](/assets/images/DevOps/2/image-20250710-043818.png)

2-2. Connect 편집기에서 YAML 파일을 생성하는 파이프라인을 만들거나 YAML 파일 없이 파이프라인 생성 중

원하는 편집 선택

- YAML 파일  장점 : 텍스트 파일이므로 해당 YAML 파일을 내 저장소에 포함 가능

![image_post27](/assets/images/DevOps/2/image-20250710-043851.png)
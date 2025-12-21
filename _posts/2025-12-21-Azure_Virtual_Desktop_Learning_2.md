---
title: "AVD Learning-(2)"
excerpt: "Azure Virtual Desktop 배포"
date: 2025-12-21
categories: [AVD]
Tags: [AVD]
toc: true
toc_sticky: true
toc_label: "AzureVirtualDesktop"
sidebar_main: true
published: true
header:
   teaser: /assets/images/avd_baner.jpg
---

## Azure Virtual Desktop

### ● 배포
\- Azure Portal 방식으로 Azure Virtual Desktop 배포를 진행합니다.<br>
\- 작업 전 사용할 OS 지원항목 및 배포 가능한 지역을 확인합니다.<br>
\- 배포 및 구성 시 필요한 RBAC이 부여되어 있는지 확인이 필요합니다.<br>

><br>[!info] 필요 RBAC 역할<br>
>호스트 풀, 작업 영역 및 애플리케이션 그룹 ▶ 데스크톱 가상화 기여자<br>
>세션호스트(Azure 및 Azure 확장 영역) ▶ Virtual Machine 기여자<br>
>세션호스트(Azure 로컬) ▶ Azure Stack HCI VM 기여자<br><br>

#### A. 호스트풀 생성
\- 세션 호스트로 Azure Virtual Desktop 에 등록된 Azure 가상 머신의 컬렉션입니다.<br>
  1. Azure Virtual Desktop 검색 후 호스트 풀을 선택합니다.<br>
![image_post1](/assets/images/AVD/2/avd1.png)<br>
  2. 기본 사항 탭에서 정보를 입력합니다.<br>
![image_post2](/assets/images/AVD/2/avd2.png)<br>
   - 구독 : 호스트 풀을 만들 구독 선택<br>
   - 리소스 그룹 : 기존 리소스그룹 혹은 새로 만들기를 선택<br>
   - 호스트 풀 이름 : 호스트 풀의 이름 입력<br>
   - 위치 : 호스트 풀을 만들 Azure 지역 선택<br>
   - 유효성 검사 환경 : 예 혹은 아니오로 유효성 검사 선택<br>
   - 호스트 풀 유형 : 개인 혹은 풀링됨 중 선택<br>
  3. (선택사항) 새션호스트, 작업영역에서 해당 리소스를 추가할 수 있습니다. <br>
  4. (선택사항) 고급에서 진단 설정을 추가할 수 있습니다. <br>
  5. 만들기를 선택해 리소스를 배포합니다. <br><br>

#### B. 작업영역 생성
\- 사용자가 게시된 데스크톱 및 애플리케이션을 보려면 각 애플리케이션 그룹을 작업영역과 연결해야 합니다. <br>
  1. Azure Virtual Desktop 개요에서 작업 영역 선택 후 만들기를 선택합니다.<br>
![image_post3](/assets/images/AVD/2/avd3.png)<br>
  2. 기본 사항 탭에서 정보를 입력<br>
![image_post4](/assets/images/AVD/2/avd4.png)<br>
   - 구독 : 작업영역을 만들 구독 선택<br>
   - 리소스 그룹 : 기존 리소스그룹 혹은 새로 만들기를 선택<br>
   - 작업영역 이름 : 작업 영역의 이름을 입력합니다.<br>
   - (선택사항) 이름 : 작업영역의 표시 이름을 입력합니다.<br>
   - (선택사항) 설명 : 작업영역의 설명을 입력합니다.<br>
   - 위치 : 작업영역을 배포할 지역을 입력합니다.<br>
  3. (선택사항) 애플리케이션 그룹에서 해당 리소스를 추가할 수 있습니다. <br>
  4. (선택사항) 고급에서 진단 설정을 추가할 수 있습니다. <br>
  5. 만들기를 선택해 리소스를 배포합니다. <br><br>

#### C. 애플리케이션 그룹 생성
\- 전체 데스크톱 또는 단일 호스트풀의 세션 호스트에서 사용할 수 있는 애플리케이션의 논리적 그룹화에 대한 액세스 제어 역할입니다. <br>
><br>[!info]<br>
>호스트 풀 생성시 애플리케이션 그룹이 생성 됩니다.<br>
>생성되어지지 않은 경우 아래 방법으로 수동으로 생성해주세요.<br><br>

  1. Azure Virtual Desktop 개요에서 애플리케이션 그룹을 선택 후 만들기를 선택합니다.<br>
![image_post5](/assets/images/AVD/2/avd5.png)<br>
  2. 기본 사항 탭에서 정보를 입력<br>
![image_post6](/assets/images/AVD/2/avd6.png)<br>
   - 구독 : 작업영역을 만들 구독 선택<br>
   - 리소스 그룹 : 기존 리소스그룹 혹은 새로 만들기를 선택<br>
   - 호스트 풀 : 애플리케이션 그룹에 대한 호스트 풀을 선택합니다.<br>
   - 위치 : 메타데이터는 호스트 풀과 동일한 위치에 저장됩니다.<br>
   - 애플리케이션 그룹 유형 : 호스트풀에 대한 애플리케이션 그룹 유형을 선택합니다.<br>
   - 애플리케이션 그룹 이름 : 애플리케이션 그룹 이름을 입력합니다.<br>
  3. (선택사항) 할당에서 애플리케이션 그룹에 사용자 또는 그룹을 할당하려는 경우 `사용자 또는 사용자 그룹에 Microsoft Entra 추가` 릍 선택합니다. <br>
![image_post7](/assets/images/AVD/2/avd7.png)<br>
  4. (선택사항) 작업 영역에서 애플리케이션 그룹을 등록할 수 있습니다. <br>
  5. (선택사항) 고급에서 진단 설정을 추가할 수 있습니다. <br>
  6. 만들기를 선택해 리소스를 배포합니다. <br><br>

#### D. 애플리케이션 그룹 생성
\- 작업 영역에 애플리케이션 그룹 추가 시 아래 단계를 수행합니다. <br>
  1. Azure Virtual Desktop 개요에서 작업 영역을 선택 후 애플리케이션 그룹을 할당할 작업 영역을 선택합니다.<br>
  2. 작업 영역 개요에서 애플리케이션 그룹 선택 후 추가를 선택합니다.<br>
![image_post8](/assets/images/AVD/2/avd8.png)<br>
  3. 목록에서 애플리케이션 그룹 옆의 더하기로 확인 후 선택합니다.<br>
![image_post9](/assets/images/AVD/2/avd9.png)<br>

#### F. 애플리케이션 그룹에 사용자 할당
\- 사용자 혹은 사용자 그룹을 애플리케이션 그룹에 할당하려고 할 때 아래 단계를 수행합니다. <br>
  1. Azure Virtual Desktop 개요에서 애플리케이션 그룹을 선택 후 작업할 애플리케이션 그룹을 선택합니다.<br>
  2. 그룹 개요에서 할당을 선택합니다.<br>
![image_post10](/assets/images/AVD/2/avd10.png)<br>
  3. 추가를 선택해 할당할 사용자 계정 혹은 그룹을 검색해 선택합니다.<br>
![image_post11](/assets/images/AVD/2/avd11.png)<br>

#### G. 세션 호스트 추가
\- 사용자가 접근할 세션 호스트를 추가할 경우 아래 단계를 수행합니다. <br>
  1. Azure Virtual Desktop 개요에서 호스트 풀을 선택 후 작업할 호스트 풀을 선택합니다.<br>
  2. 그룹 개요에서 세션 호스트를 선택 후 추가를 선택합니다.<br>
![image_post12](/assets/images/AVD/2/avd12.png)<br>
  3. Virtual Machines 탭에서 정보를 입력<br>
![image_post13](/assets/images/AVD/2/avd13.png)<br>
   - 이름 접두사 : 생성할 세션 호스트의 이름을 입력합니다<br>
   - 가상머신 유형 : 생성할 가상머신 유형을 선택합니다.<br>
   - 가용성 옵션 : 가용성 옵션을 선택합니다.<br>
   - 이미지 : 배포할 세션호스트의 OS 이미지를 선택합니다.<br>
   - 가상 머신 크기 : 배포할 세션호스트의 SKU를 선택합니다.<br>
   - VM 수 : 배포할 세션 호스트의 수를 선택합니다.<br>
   - OS 디스크 유형 : 배포할 세션 호스트의 OS Disk 유형을 선택합니다.<br>
   - OS 디스크 크기 : 배포할 세션 호스트의 OS Disk 크기를 선택합니다.<br>
![image_post14](/assets/images/AVD/2/avd14.png)<br>
   - 가상 네트워크 : 베포할 세션 호스트가 위치할 가상 네트워크를 선택합니다.<br>
   - 서브넷 :  베포할 세션 호스트가 위치할 서브넷을 선택합니다.<br>
   - 가입할 도메인 : Active Directory 혹은 EntraID 를 선택합니다.<br>
   - OS 디스크 크기 : 배포할 세션 호스트의 OS Disk 크기를 선택합니다.<br>
  4. 만들기를 선택해 리소스를 배포합니다. <br><br>

#### H. 사용자 할당
\- 세션 호스트에 사용자를 할당하려는 경우 아래 단계를 수행합니다. <br>
  1. Azure Virtual Desktop 개요에서 호스트 풀을 선택 후 작업할 호스트 풀을 선택합니다.<br>
  2. 세션 호스트에서 생성된 세션 호스트를 선택 후 과제를 선택해 사용자 할당을 선택합니다.<br>
![image_post15](/assets/images/AVD/2/avd15.png)<br>
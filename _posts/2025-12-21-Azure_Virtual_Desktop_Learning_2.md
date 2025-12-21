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
   teaser: /assets/images/azure_baner.jpg
---

## Azure Virtual Desktop

### ● 배포

#### ∘ 호스트풀
\- 세션 호스트로 Azure Virtual Desktop 에 등록된 Azure 가상 머신의 컬렉션<br>
\- 일관된 사용자 환경을 위해 호스트풀의 모든 세션 호스트 가상 머신을 동일한 이미지에서 원본으로 제공<br>
 ● 유형<br>
  1.개인<br>
   - 각 세션 호스트가 개별 사용자에게 할당<br>
   - 최대 세션 1명 제한<br>
   - 각 사용자는 각 VM의 OS 디스크에 사용자 프로필 데이터 저장 가능<br>
  2.풀링된<br>
   - 단일 세션 호스트에 동시에 여러 다른 사용자 존재 가능<br>
   - 최대 세션 제한 값으로 구성<br>
   - 연결할 때마다 다른 세션호스트에 연결되어 FSLogix에 사용자 프로필 데이터 저장<br><br>

#### ∘ 애플리케이션 그룹

\- 전체 데스크톱 또는 단일 호스트풀의 세션 호스트에서 사용할 수 있는 애플리케이션의 논리적 그룹화에 대한 액세스 제어 <br>
 ● 유형<br>
  1.데스크톱<br>
   - 사용자는 세션호스트에서 전체 Windows 데스크톱에 액세스<br>
   - 풀 또는 개인 호스트 풀에서 사용<br>
  2.RemoteApp<br>
   - 사용자가 선택한 개별 애플리케이션에 액세스하고 애플리케이션 그룹에 게시<br>
   - 풀된 호스트 풀에서만 사용 가능<br><br>

#### ∘ 작업 영역
\- 애플리케이션 그룹의 논리적 그룹화 <br>
\- 사용자가 게시된 데스크톱 및 애플리케이션을 보려면 각 애플리케이션 그룹을 작업영역과 연결 <br>
\- 단일 작업 영역에만 할당 가능 <br><br>

### ● 배포


![image_post5](/assets/images/DevOps/1/image-20250530-091002.png)
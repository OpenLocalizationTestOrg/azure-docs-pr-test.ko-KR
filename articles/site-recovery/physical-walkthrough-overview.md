---
title: "실제 aaaReplicate 온-프레미스 Azure Site Recovery와 서버 tooAzure | Microsoft Docs"
description: "Hello Azure Site Recovery 서비스와 Windows/Linux 물리적 서버의 tooAzure 온-프레미스에서 실행 되는 작업을 복제 하기 위한 hello 단계의 개요를 제공 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a>사이트 복구와 실제 서버 tooAzure 복제

이 문서에서는 hello 단계 필요한 tooreplicate 온-프레미스 Windows/Linux 물리적 서버의 tooAzure, hello를 사용 하 여 간략하게 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.


## <a name="step-1-review-architecture-and-prerequisites"></a>1단계: 아키텍처 및 필수 구성 요소 검토

배포를 시작 하기 전에 hello 시나리오 아키텍처를 검토 하 고 tooset hello 배포를 필요한 모든 hello 구성 요소를 이해 해야 합니다.

너무 이동[1 단계: hello 아키텍처 검토](physical-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>2단계: 필수 구성 요소 검토

Hello 필수 구성 요소에서 각 배포 구성 요소에 대 한 있습니까 있는지 확인 합니다.

- **Azure 필수 구성 요소**: Microsoft Azure 계정, Azure 네트워크 및 저장소 계정이 필요합니다.
- **온-프레미스 Site Recovery 구성 요소**: 컴퓨터가 온-프레미스 Site Recovery 구성 요소를 실행해야 합니다.
- **복제 된 컴퓨터**: tooreplicate 원하는 서버 toocomply 온-프레미스 및 Azure 요구 사항을 적용 해야 합니다.

너무 이동[2 단계: 필수 구성 요소 및 제한 사항 검토](physical-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>3단계: 용량 계획

전체 배포를 수행 하는 경우 필요한 복제 리소스 아웃 toofigure를 해야 합니다. 빠른 tootest hello 환경을 설정 하 고,이 단계를 건너뛸 수 있습니다.

너무 이동[3 단계: 용량 계획](physical-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>4단계: 네트워킹 계획

Toodo 일부 네트워크 tooensure 있는지 Azure Vm 연결된 toonetworks 장애 조치가 발생 한 후와 hello 수 있는 올바른 IP 주소를 계획 해야 합니다.

너무 이동[4 단계: 네트워킹 계획](physical-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>5단계: Azure 리소스 준비

시작하기 전에 Azure 네트워크 및 저장소를 설정합니다. 

너무 이동[5 단계: Azure 준비](physical-walkthrough-prepare-azure.md)


## <a name="step-6-set-up-a-vault"></a>6단계: 자격 증명 모음 설정

복구 서비스 자격 증명 모음 tooorchestrate를 설정 하 고 복제를 관리 합니다. 수행할 hello 자격 증명 모음을 설정할 때 지정 tooreplicate, tooreplicate 원본 위치에 있습니다.

너무 이동[6 단계: 자격 증명 모음 설정](physical-walkthrough-create-vault.md)

## <a name="step-7-configure-source-and-target-settings"></a>7단계: 원본 및 대상 설정 구성

Hello 소스에 대 한 설정을 구성 하 고 대상 (Azure) 사이트로 합니다. 소스 설정 포함 통합 설치 tooinstall hello 온-프레미스 복구 사이트 구성 요소를 실행 합니다.

너무 이동[7 단계: hello 소스 및 대상 설정](physical-walkthrough-source-target.md)

## <a name="step-8-set-up-a-replication-policy"></a>8단계: 복제 정책 설정

설정한 정책 toospecify 물리적 서버에 복제 해야 합니다.

너무 이동[8 단계: 복제 정책 설정](physical-walkthrough-replication.md)

## <a name="step-9-install-hello-mobility-service"></a>9 단계: hello 모바일 서비스를 설치 합니다.

hello 모바일 서비스를 설치 해야 tooreplicate 구성할 각 서버. 밀어넣기 또는 끌어오기 설치로 hello 서비스를 몇 가지 방법으로 tooset 가지가 있습니다.

너무 이동[9 단계: hello Mobility service 설치](physical-walkthrough-install-mobility.md)

## <a name="step-10-enable-replication"></a>10단계: 복제 활성화

Hello 모바일 서비스를 서버에서 실행 한 후 복제를 사용할 수 있습니다. 를 사용 하도록 설정한 후 hello VM의 초기 복제가 발생합니다.

너무 이동[10 단계: 복제 사용](physical-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>11단계: 테스트 장애 조치(failover) 실행

초기 복제가 완료 된 후 델타 복제 실행 되 고 정상적으로 작동 하는지 테스트 장애 조치 toomake를 실행할 수 있습니다.

너무 이동[11 단계: 테스트 장애 조치 실행](physical-walkthrough-test-failover.md)


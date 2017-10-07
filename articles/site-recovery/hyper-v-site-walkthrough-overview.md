---
title: "Azure Site Recovery와 aaaReplicate Hyper-v Vm tooAzure | Microsoft Docs"
description: "설명 방법을 tooorchestrate 복제, 장애 조치 및 복구의 온-프레미스 하이퍼-V Vm tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a>Hyper-v 가상 컴퓨터 (VMM 없음) tooAzure 복제 

> [!div class="op_single_selector"]
> * [Azure 포털](site-recovery-hyper-v-site-to-azure.md)
> * [Azure 클래식](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell - Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

이 문서에서는 hello 필요한 단계 tooreplicate 온-프레미스 Hyper-v 가상 컴퓨터 tooAzure, hello를 사용 하 여 간략하게 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서. 이 배포에서는 Hyper-V VM이 System Center VMM(Virtual Machine Manager)을 통해 관리되지 않습니다.


이 문서를 읽은 후 hello 맨 아래에 모든 메모를 게시 하거나 hello에 대 한 기술적 질문 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="step-1-review-architecture-and-prerequisites"></a>1단계: 아키텍처 및 필수 구성 요소 검토

배포를 시작 하기 전에 hello 시나리오 아키텍처를 검토 하 고 toodeploy 필요한 모든 hello 구성 요소 이해

너무 이동[1 단계: hello 아키텍처 검토](hyper-v-site-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>2단계: 필수 구성 요소 검토

Hello 필수 구성 요소에서 각 배포 구성 요소에 대 한 있습니까 있는지 확인 합니다.

- **Azure 필수 구성 요소**: Microsoft Azure 계정, Azure 네트워크 및 저장소 계정이 필요합니다.
- **온-프레미스 Hyper-V 필수 구성 요소**: Hyper-V 호스트가 Site Recovery 배포에 준비되어 있는지 확인합니다.
- **Vm 복제**: tooreplicate toocomply Azure 요구 사항에 필요한 Vm을 합니다.

너무 이동[2 단계: 사전 요구 사항 및 제한 사항 확인](hyper-v-site-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>3단계: 용량 계획

전체 배포를 수행 하는 경우 필요한 복제 리소스 아웃 toofigure를 해야 합니다. 두 도구 사용 가능한 toohelp의이 작업을 수행 합니다. TooStep 2를 이동 합니다. 빠른 tootest hello 환경을 설정 하 고이 단계를 건너뛸 수 있습니다.

너무 이동[3 단계: 용량 계획](hyper-v-site-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>4단계: 네트워킹 계획

Toodo 일부 네트워크 tooensure 있는지 Azure Vm 연결된 toonetworks 장애 조치가 발생 한 후와 hello 수 있는 올바른 IP 주소를 계획 해야 합니다.

너무 이동[4 단계: 네트워킹 계획](hyper-v-site-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>5단계: Azure 리소스 준비

시작하기 전에 Azure 네트워크 및 저장소를 설정합니다. 이 작업은 배포하는 동안에도 수행할 수 있지만 시작하기 전에 수행하는 것이 좋습니다.

너무 이동[5 단계: Azure 준비](hyper-v-site-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-hyper-v"></a>6단계: Hyper-V 준비

Hyper-V 서버가 Site Recovery 배포 요구 사항을 충족하는지 확인합니다.

너무 이동[6 단계: 준비 Hyper-v](hyper-v-site-walkthrough-prepare-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>7단계: 자격 증명 모음 설정

복구 서비스 자격 증명 모음 tooorchestrate tooset 필요 하 고 복제를 관리 합니다. 수행할 hello 자격 증명 모음을 설정할 때 지정 tooreplicate, tooreplicate 원본 위치에 있습니다.

너무 이동[7 단계: 자격 증명 모음 만들기](hyper-v-site-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>8단계: 원본 및 대상 설정 구성

Hello 원본 및 복제에 사용 되는 대상을 설정 합니다. 소스 설정 설정 Hyper-v 호스트 tooa 하이퍼-V 사이트를 각 Hyper-v 호스트에서 Site Recovery Provider hello 및 복구 서비스 에이전트를 설치 하 고 hello 사이트 hello 복구 서비스 자격 증명 모음에 등록 추가 포함 됩니다.

너무 이동[8 단계: hello 소스 및 대상 설정](hyper-v-site-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>9단계: 복제 정책 설정

설정한 정책 toospecify 복제 설정을 Hyper-v Vm에 대 한 hello 자격 증명 모음에 있습니다.

너무 이동[9 단계: 복제 정책 설정](hyper-v-site-walkthrough-replication.md)


## <a name="step-10-enable-replication"></a>10단계: 복제 활성화

현재 위치에서 사용 하도록 설정한 후 복제 정책을 구성한 후 hello VM의 초기 복제가 발생 합니다.

너무 이동[10 단계: 복제 사용](hyper-v-site-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>11단계: 테스트 장애 조치(failover) 실행

초기 복제가 완료 된 후 델타 복제 실행 되 고 정상적으로 작동 하는지 테스트 장애 조치 toomake를 실행할 수 있습니다.

너무 이동[11 단계: 테스트 장애 조치 실행](hyper-v-site-walkthrough-test-failover.md)

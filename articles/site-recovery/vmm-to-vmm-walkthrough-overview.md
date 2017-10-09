---
title: "Azure Site Recovery와 aaaReplicate Hyper-v Vm tooa 보조 VMM 사이트 | Microsoft Docs"
description: "Hyper-v Vm tooa 보조 VMM 사이트 hello Azure 포털을 사용 하 여 복제에 대 한 개요를 제공 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>VMM 클라우드 tooa 보조 VMM 사이트에서 Hyper-v 가상 컴퓨터 복제

> [!div class="op_single_selector"]
> * [Azure 포털](site-recovery-vmm-to-vmm.md)
> * [클래식 포털](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

이 문서에서는 hello tooreplicate 온-프레미스 보조 VMM 위치 tooa System Center Virtual Machine Manager (VMM) 클라우드에서 관리 되는 Hyper-v 가상 컴퓨터 (Vm)는 데 필요한 단계에 대 한 개요를 사용 하 여 [Azure Site Recovery](site-recovery-overview.md)hello Azure 포털의에서.

이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="step-1-review-hello-scenario-architecture"></a>1 단계: hello 시나리오 아키텍처를 검토 합니다.

배포를 시작 하 고 hello 시나리오 아키텍처를 검토 hello에 대 한 구성 요소를 모두 이해 하기 전에 toodeploy를 해야 합니다.

너무 이동[1 단계: hello 아키텍처를 검토](vmm-to-vmm-walkthrough-architecture.md)합니다.

## <a name="step-2-review-prerequisites-and-limitations"></a>2단계: 필수 구성 요소 및 제한 사항 검토

Hello 배포 필수 구성 요소 및 제한 사항 이해 하 고 있는지 확인 합니다.

**Azure의 필수 구성 요소**: Azure 복구 서비스 자격 증명 모음 tooorchestrate 하 고 복제를 관리 및 Microsoft Azure 구독이 필요 합니다.
**온-프레미스 VMM 서버 및 Hyper-V 호스트**: VMM 서버 및 Hyper-V 호스트가 Site Recovery 배포용으로 준비되었으며 배포 규격에 맞는지 확인합니다.

너무 이동[2 단계: 사전 요구 사항 및 제한 사항 확인](vmm-to-vmm-walkthrough-prerequisites.md)합니다.

## <a name="step-3-plan-networking"></a>3단계: 네트워킹 계획

Toodo 일부 네트워크 tooensure hello 시나리오를 배포할 때 VMM VM 네트워크 간에 네트워크 매핑을 구성할 수 있는지를 계획 해야 합니다.

너무 이동[3 단계: 네트워킹 계획](vmm-to-vmm-walkthrough-network.md)합니다.


## <a name="step-4-prepare-vmm-and-hyper-v"></a>4단계: VMM 및 Hyper-V 준비

사이트 복구 배포에 대 한 hello VMM 서버와 Hyper-v 호스트를 준비 합니다.

너무 이동[4 단계: 온-프레미스 서버를 준비](vmm-to-vmm-walkthrough-vmm-hyper-v.md)합니다.

## <a name="step-5-set-up-a-vault"></a>5단계: 자격 증명 모음 설정

Recovery Services 자격 증명 모음을 설정합니다. hello 자격 증명 모음 구성 설정을 포함 하 고 복제를 조정 합니다.

[5단계: 자격 증명 모음 설정](vmm-to-vmm-walkthrough-create-vault.md).

## <a name="step-6-set-up-source-and-target-settings"></a>6단계: 원본 및 대상 설정 지정

Hello 원본 및 대상 복제 VMM 위치를 설정 합니다. Hello VMM 서버 toohello 자격 증명 모음을 추가 하 고 Site Recovery 구성 요소에 대 한 hello 설치 파일을 다운로드 합니다. Hello VMM 서버에 Azure Site Recovery Provider 설치 프로그램을 실행 합니다. 설치 프로그램 hello VMM 서버의 hello 공급자를 설치 하 고 hello 서버 hello 자격 증명 모음에 등록 합니다. 각 Hyper-v 호스트에 hello Microsoft 복구 서비스 에이전트를 설치 합니다.

너무 이동[6 단계: 원본 및 대상 설정을 지정 hello](vmm-to-vmm-walkthrough-source-target.md)합니다.

## <a name="step-7-configure-network-mapping"></a>7단계: 네트워크 매핑 구성

Hello 소스 및 대상 위치의 VMM VM 네트워크를 매핑하십시오. 장애 조치 후 Vm은 어떤 hello 원본 Hyper-v VM이 있는 해당 맵을 toohello 원본 VM 네트워크 hello 대상 네트워크에 생성 됩니다.

너무 이동[7 단계: 네트워크 매핑을 구성](vmm-to-vmm-walkthrough-network-mapping.md)합니다.


## <a name="step-8-set-up-a-replication-policy"></a>8단계: 복제 정책 설정

VMM 위치 간에 VM을 복제할 방법을 지정합니다.

너무 이동[8 단계: 복제 정책 설정](vmm-to-vmm-walkthrough-replication.md)합니다.


## <a name="step-9-enable-replication-for-vms"></a>9단계: VM을 복제하도록 설정

원하는 tooreplicate hello Vm을 선택 합니다. 진행 중인 델타 복제 뒤 복제 트리거 hello 초기 복제 toohello 보조 사이트에 대 한 VM을 사용 하도록 설정 합니다.

너무 이동[9 단계: 복제 사용](vmm-to-vmm-walkthrough-enable-replication.md)합니다.


## <a name="step-10-run-a-test-failover"></a>10단계: 테스트 장애 조치(failover) 실행

모든 것이 예상 대로 작동 하는지 테스트 장애 조치 toomake를 실행 합니다.

너무 이동[10 단계: 테스트 장애 조치 실행](vmm-to-vmm-walkthrough-test-failover.md)합니다.

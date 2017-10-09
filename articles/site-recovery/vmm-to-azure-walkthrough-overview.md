---
title: "aaaReplicate VMM에서 Hyper-v Vm 클라우드를 Azure Site Recovery와 tooAzure | Microsoft Docs"
description: "Hyper-v Vm에서 VMM 클라우드 tooAzure hello Azure Site Recovery 서비스를 사용 하 여 복제를 위한 개요를 제공 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>Hello Azure 포털에서에서 사이트 복구를 사용 하 여 VMM 클라우드에 tooAzure에서 Hyper-v 가상 컴퓨터 복제
> [!div class="op_single_selector"]
> * [Azure 포털](site-recovery-vmm-to-azure.md)
> * [Azure 클래식](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell 클래식](site-recovery-deploy-with-powershell.md)


이 문서에서는 hello 단계 필요한 tooreplicate 간략하게 온-프레미스 Hyper-v 가상 컴퓨터 (Vm)에서 System Center Virtual Machine Manager (VMM) 클라우드 tooAzure, hello를 사용 하 여 관리 되는 [Azure Site Recovery](site-recovery-overview.md) 서비스에 Azure 포털 번호입니다.

이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="step-1-review-hello-scenario-architecture"></a>1 단계: hello 시나리오 아키텍처를 검토 합니다.

배포를 시작 하 고 hello 시나리오 아키텍처를 검토 hello에 대 한 구성 요소를 모두 이해 하기 전에 toodeploy를 해야 합니다.

너무 이동[1 단계: hello 아키텍처 검토](vmm-to-azure-walkthrough-architecture.md)

## <a name="step-2-review-prerequisites-and-limitations"></a>2단계: 필수 구성 요소 및 제한 사항 검토

Hello 배포 필수 구성 요소 및 제한 사항 이해 하 고 있는지 확인 합니다.

**Azure 필수 구성 요소**: Microsoft Azure 계정, Azure 네트워크 및 저장소 계정이 필요합니다.
**온-프레미스 VMM 서버 및 Hyper-V 호스트**: VMM 서버 및 Hyper-V 호스트가 Site Recovery 배포용으로 준비되었으며 배포 규격에 맞는지 확인합니다.
**Vm 복제**: tooreplicate Vm을 Azure 요구 사항을 준수 확인 합니다.

너무 이동[2 단계: 사전 요구 사항 및 제한 사항 확인](vmm-to-azure-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>3단계: 용량 계획

전체 배포를 수행 하는 경우 필요한 복제 리소스 아웃 toofigure를 해야 합니다. 두 도구 사용 가능한 toohelp의이 작업을 수행 합니다. 빠른 tootest hello 환경을 설정 하 고,이 단계를 건너뛸 수 있습니다.

너무 이동[3 단계: 용량 계획](vmm-to-azure-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>4단계: 네트워킹 계획

필요한 toodo 계획 tooensure hello 시나리오를 배포할 때 네트워크 매핑을 구성할 수 있는 몇 가지 네트워크는 Azure Vm 가상 네트워크에 연결 된 tooAzure 후 됩니다 장애 조치가 발생 하 고 적절 한 IP를 할당 하는 주소입니다.

너무 이동[4 단계: 네트워킹 계획](vmm-to-azure-walkthrough-network.md)


## <a name="step-5-prepare-azure-resources"></a>5단계: Azure 리소스 준비

Azure 계정, 네트워크 및 저장소를 설정합니다. 이 작업은 배포하는 동안에도 수행할 수 있지만 시작하기 전에 수행하는 것이 좋습니다.

너무 이동[5 단계: Azure 준비](vmm-to-azure-walkthrough-prepare-azure.md)

## <a name="step-6-prepare-vmm-and-hyper-v"></a>6단계: VMM 및 Hyper-V 준비

사이트 복구 배포에 대 한 hello 온-프레미스 VMM 서버 및 Hyper-v 호스트를 준비 합니다.

너무 이동[6 단계: 온-프레미스 서버 준비](vmm-to-azure-walkthrough-vmm-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>7단계: 자격 증명 모음 설정

Recovery Services 자격 증명 모음을 설정합니다. hello 자격 증명 모음 구성 설정을 포함 하 고 복제를 조정 합니다.

[7단계: 자격 증명 모음 설정](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>8단계: 원본 및 대상 설정 구성

Hello 원본 및 대상 복제 위치를 설정 합니다. Hello VMM 서버 toohello 자격 증명 모음을 추가 하 고 Site Recovery 구성 요소에 대 한 hello 설치 파일을 다운로드 합니다. Hello VMM 서버에 Azure Site Recovery Provider 설치 프로그램을 실행 합니다. 설치 프로그램 hello VMM 서버의 hello 공급자를 설치 하 고 hello 서버 hello 자격 증명 모음에 등록 합니다. 각 Hyper-v 호스트에 hello Microsoft 복구 서비스 에이전트를 설치 합니다.

너무 이동[8 단계: 원본 및 대상 설정 구성](vmm-to-azure-walkthrough-source-target.md)

## <a name="step-9-configure-network-mapping"></a>9단계: 네트워크 매핑 구성

지도 온-프레미스 VMM VM 네트워크 tooAzure 가상 네트워크. 장애 조치 후 Azure Vm은 Azure 네트워크는 hello 원본 Hyper-v의 위치를 가리키는 toohello 온-프레미스 VM 네트워크를 매핑하는 hello에 생성 됩니다.

너무 이동[9 단계: 네트워크 매핑 구성](vmm-to-azure-walkthrough-network-mapping.md)


## <a name="step-10-set-up-a-replication-policy"></a>10단계: 복제 정책 설정

온-프레미스 Vm 복제 tooAzure 되는 방식을 지정 합니다.

너무 이동[10 단계: 복제 정책 설정](vmm-to-azure-walkthrough-replication.md)


## <a name="step-11-enable-replication-for-vms"></a>11단계: VM을 복제하도록 설정

원하는 tooreplicate hello Vm을 선택 합니다. 진행 중인 델타 복제 뒤 복제 트리거 hello 초기 복제 tooAzure에 대 한 VM을 사용 하도록 설정 합니다.

너무 이동[11 단계: 복제 사용](vmm-to-azure-walkthrough-enable-replication.md)


## <a name="step-12-run-a-test-failover"></a>12단계: 테스트 장애 조치(failover) 실행

모든 것이 예상 대로 작동 하는지 테스트 장애 조치 toomake를 실행 합니다.

너무 이동[12 단계: 테스트 장애 조치 실행](vmm-to-azure-walkthrough-test-failover.md)



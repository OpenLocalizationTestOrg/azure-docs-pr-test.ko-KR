---
title: "Azure Site Recovery를 사용하여 VMM 클라우드의 Hyper-V VM을 Azure로 복제 | Microsoft 문서"
description: "이 문서에서는 Azure Site Recovery 서비스를 사용하여 VMM 클라우드의 Hyper-V VM을 Azure로 복제하는 과정을 간략하게 설명합니다."
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
ms.openlocfilehash: af68d21184c137b2b0f1bb4c1afb9bf507e8332d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-azure-using-site-recovery-in-the-azure-portal"></a>Azure Portal에서 Site Recovery를 사용하여 VMM 클라우드의 Hyper-V 가상 컴퓨터를 Azure에 복제
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-azure.md)
> * [Azure 클래식](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell 클래식](site-recovery-deploy-with-powershell.md)


이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용해 System Center Virtual Machine Manager(VMM) 클라우드에서 관리되는 온-프레미스 Hyper-V VM(가상 컴퓨터)을 Azure로 복제하기 위해 수행해야 하는 단계를 간략하게 설명합니다.

이 문서를 읽은 후에 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견을 게시합니다.


## <a name="step-1-review-the-scenario-architecture"></a>1단계: 시나리오 아키텍처 검토

배포를 시작하기 전에 시나리오 아키텍처를 검토하고 배포에 필요한 모든 구성 요소를 이해해야 합니다.

[1단계: 아키텍처 검토](vmm-to-azure-walkthrough-architecture.md)로 이동합니다.

## <a name="step-2-review-prerequisites-and-limitations"></a>2단계: 필수 구성 요소 및 제한 사항 검토

배포 필수 구성 요소 및 제한 사항을 이해해야 합니다.

**Azure 필수 구성 요소**: Microsoft Azure 계정, Azure 네트워크 및 저장소 계정이 필요합니다.
**온-프레미스 VMM 서버 및 Hyper-V 호스트**: VMM 서버 및 Hyper-V 호스트가 Site Recovery 배포용으로 준비되었으며 배포 규격에 맞는지 확인합니다.
**복제된 VM**: 복제할 VM이 Azure 요구 사항을 준수하는지 확인합니다.

[2단계: 필수 구성 요소 및 제한 사항 확인](vmm-to-azure-walkthrough-prerequisites.md)으로 이동합니다.

## <a name="step-3-plan-capacity"></a>3단계: 용량 계획

전체 배포를 진행하려면 필요한 복제 리소스를 파악해야 합니다. 이 작업을 수행하는 데 도움이 되는 몇 가지 도구를 사용할 수 있습니다. 환경을 테스트하는 빠른 설정을 수행하려면 이 단계를 건너뛸 수 있습니다.

[3단계: 용량 계획](vmm-to-azure-walkthrough-capacity.md)으로 이동합니다.

## <a name="step-4-plan-networking"></a>4단계: 네트워킹 계획

시나리오를 배포할 때 네트워크 매핑을 구성할 수 있는지, 장애 조치(failover) 후에 Azure VM이 Azure Virtual Network에 연결되는지, 그리고 Azure VM에 적절한 IP 주소가 할당되는지를 확인하려면 몇 가지 네트워크 계획을 수행해야 합니다.

[4단계: 네트워킹 계획](vmm-to-azure-walkthrough-network.md)으로 이동합니다.


## <a name="step-5-prepare-azure-resources"></a>5단계: Azure 리소스 준비

Azure 계정, 네트워크 및 저장소를 설정합니다. 이 작업은 배포하는 동안에도 수행할 수 있지만 시작하기 전에 수행하는 것이 좋습니다.

[5단계: Azure 준비](vmm-to-azure-walkthrough-prepare-azure.md)로 이동합니다.

## <a name="step-6-prepare-vmm-and-hyper-v"></a>6단계: VMM 및 Hyper-V 준비

Site Recovery 배포용 온-프레미스 VMM 서버 및 Hyper-V 호스트를 준비합니다.

[6단계: 온-프레미스 서버 준비](vmm-to-azure-walkthrough-vmm-hyper-v.md)로 이동합니다.

## <a name="step-7-set-up-a-vault"></a>7단계: 자격 증명 모음 설정

Recovery Services 자격 증명 모음을 설정합니다. 자격 증명 모음은 구성 설정을 포함하며 복제를 오케스트레이션합니다.

[7단계: 자격 증명 모음 설정](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>8단계: 원본 및 대상 설정 구성

원본 및 대상을 복제 위치를 설정합니다. VMM 서버를 자격 증명 모음에 추가하고 Site Recovery 구성 요소의 설치 파일을 다운로드합니다. VMM 서버에서 Azure Site Recovery Provider 설치를 실행합니다. 설치를 실행하면 VMM 서버에 Azure Site Recovery Provider가 설치되고 자격 증명 모음에 서버가 등록됩니다. 각 Hyper-V 호스트에 Microsoft Recovery Services 에이전트를 설치합니다.

[8단계: 원본 및 대상 설정 구성](vmm-to-azure-walkthrough-source-target.md)으로 이동합니다.

## <a name="step-9-configure-network-mapping"></a>9단계: 네트워크 매핑 구성

온-프레미스 VMM VM 네트워크를 Azure Virtual Network에 매핑합니다. 장애 조치(failover) 후에는 원본 Hyper-V가 있는 온-프레미스 VM 네트워크에 매핑되는 Azure 네트워크에 Azure VM이 작성됩니다.

[9단계: 네트워크 매핑 구성](vmm-to-azure-walkthrough-network-mapping.md)으로 이동합니다.


## <a name="step-10-set-up-a-replication-policy"></a>10단계: 복제 정책 설정

온-프레미스 VM을 Azure로 복제할 방법을 지정합니다.

[10단계: 복제 정책 설정](vmm-to-azure-walkthrough-replication.md)으로 이동합니다.


## <a name="step-11-enable-replication-for-vms"></a>11단계: VM을 복제하도록 설정

복제할 VM을 선택합니다. VM을 복제할 수 있도록 설정하면 Azure로의 초기 복제가 트리거된 다음 델타 복제가 계속 진행됩니다.

[11단계: 복제 활성화](vmm-to-azure-walkthrough-enable-replication.md)로 이동합니다.


## <a name="step-12-run-a-test-failover"></a>12단계: 테스트 장애 조치(failover) 실행

모든 것이 예상대로 작동하는지 확인할 수 있도록 테스트 장애 조치를 실행합니다.

[12단계: 테스트 장애 조치(failover) 실행](vmm-to-azure-walkthrough-test-failover.md)으로 이동합니다.



---
title: "Azure Site Recovery를 사용하여 Azure로 Hyper-V VM(System Center VMM 포함)을 복제하기 위한 Azure 리소스 준비 | Microsoft 문서"
description: "Azure Site Recovery를 사용하여 Hyper-V VM(VMM 포함)을 Azure에 복제하기 전에 Azure에서 준비해야 하는 항목을 설명합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1568bdc3-e767-477b-b040-f13699ab5644
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 63b005f37ab5e15e8a1b4645446d65f1529f1bbd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-with-vmm-to-azure"></a>5단계: Azure로의 Hyper-V 복제(VMM 포함)를 위한 Azure 리소스 준비

[네트워크 요구 사항](vmm-to-azure-walkthrough-network.md)을 확인한 후 이 문서의 지침에 따라 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용해 System Center Virtual Machine Manager(VMM) 클라우드의 온-프레미스 Hyper-V VM을 Azure로 복제할 수 있도록 Azure 리소스를 준비할 수 있습니다.

이 문서를 읽은 후에는 하단에서 의견을 게시하거나 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 기술적인 질문을 합니다.


## <a name="set-up-an-azure-account"></a>Azure 계정 설정

- [Microsoft Azure 계정](http://azure.microsoft.com/)을 가져옵니다.
- [평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다.
- [Azure Site Recovery 가격 책정 세부 정보](https://azure.microsoft.com/pricing/details/site-recovery/)의 지역 가용성에서 Site Recovery에 지원되는 지역을 확인하세요.
- [Site Recovery 가격 책정](site-recovery-faq.md#pricing)에 대해 알아보고 [가격 책정 세부 정보](https://azure.microsoft.com/pricing/details/site-recovery/)를 가져옵니다.
- Azure 계정에 Azure VM을 만들기 위한 올바른 [권한](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)이 있는지 확인합니다. Azure 역할 기반 액세스 제어에 대해 자세히 알아보려면 [여기](../active-directory/role-based-access-built-in-roles.md)를 참조하세요.


## <a name="set-up-an-azure-network"></a>Azure 네트워크를 설정

- [Azure 네트워크](../virtual-network/virtual-network-get-started-vnet-subnet.md)를 설정합니다. Azure VM은 장애 조치 후 처음 만들 때 이 네트워크에 배치됩니다.
- 네트워크가 Recovery Services 자격 증명 모음과 같은 지역에 있어야 합니다.
- Azure Portal의 Site Recovery에서는 [리소스 관리자](../resource-manager-deployment-model.md) 또는 클래식 모드에서 설정된 네트워크를 사용할 수 있습니다.
- 시작하기 전에 네트워크를 설정하는 것이 좋습니다. 그렇지 않으면 Site Recovery를 배포하는 동안 설정해야 합니다.
- [가상 네트워크 가격 책정](https://azure.microsoft.com/pricing/details/virtual-network/)에 대해 알아봅니다.


## <a name="set-up-an-azure-storage-account"></a>Azure 저장소 계정을 설정

- Site Recovery는 온-프레미스 컴퓨터를 Azure Storage에 복제합니다. 장애 조치(failover)가 발생한 후에 저장소에서 Azure VM을 만듭니다.
- 표준/프리미엄 [Azure Storage 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account)을 설정하여 Azure로 복제된 데이터를 저장합니다.
- [Premium Storage](../storage/common/storage-premium-storage.md)는 IO를 많이 사용하는 워크로드를 호스트하기 위해 일관된 IO 고성능과 짧은 대기 시간이 요구되는 가상 컴퓨터에 일반적으로 사용됩니다.
- 프리미엄 계정을 사용하여 복제된 데이터를 저장하려는 경우 온-프레미스 데이터에 대한 지속적인 변화를 캡처하는 복제 로그를 저장하는 표준 저장소 계정이 필요할 수도 있습니다.
- 장애 조치(failover)된 Azure VM에 사용하려는 리소스 모델에 따라 [Resource Manager 모드](../storage/common/storage-create-storage-account.md) 또는 [클래식 모드](../storage/common/storage-create-storage-account.md)에서 계정을 설정합니다.
- 시작하기 전에 저장소 계정을 설정하는 것이 좋습니다. 그렇지 않으면 Site Recovery를 배포하는 동안 설정해야 합니다. 계정은 Recovery Services 자격 증명 모음과 동일한 지역에 있어야 합니다.
- Site Recovery에 사용되는 저장소 계정은 동일한 구독 내의 리소스 그룹 간이나 서로 다른 구독 간에 이동할 수 없습니다.


## <a name="next-steps"></a>다음 단계

[6단계: VMM 준비](vmm-to-azure-walkthrough-vmm-hyper-v.md)로 이동합니다.

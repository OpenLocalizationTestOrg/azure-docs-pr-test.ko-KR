---
title: "Azure Site Recovery를 사용 하 여 aaaPrepare Azure 리소스 tooreplicate (System Center VMM) 없이 Hyper-v Vm tooAzure | Microsoft Docs"
description: "필요한 Azure에서 위치에 Azure Site Recovery를 사용 하 여 Hyper-v Vm (없이 VMM) tooAzure 복제를 시작 하기 전에 설명"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 28fa722c-675e-4637-98eb-7ccbf3806d69
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f659e300c39253b0eaf7218bee9d39b11682edb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-tooazure"></a>5 단계: Hyper-v 복제 tooAzure Azure 리소스 준비

Hello 지침을 사용 하 여이 문서 tooprepare Azure의에서 리소스 복제할 수 있도록 온-프레미스 Hyper-v Vm (System Center VMM) 없이 hello를 사용 하 여 tooAzure [Azure Site Recovery](site-recovery-overview.md) 서비스입니다.

이 문서를 읽은 후 hello 맨 아래에 모든 메모를 게시 하거나 hello에 대 한 기술적 질문 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="before-you-start"></a>시작하기 전에

Hello 참고 있는지 확인 하십시오 [필수 구성 요소](hyper-v-site-walkthrough-prerequisites.md)

## <a name="set-up-an-azure-account"></a>Azure 계정 설정

- [Microsoft Azure 계정](http://azure.microsoft.com/)을 가져옵니다.
- [평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다.
- 사이트 복구를 아래에서 지역 가용성을 위한 지원 hello 영역 확인 [Azure 사이트 복구 가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.
- 에 대 한 자세한 내용은 [사이트 복구 가격](site-recovery-faq.md#pricing), 가져오고, hello [가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.


## <a name="set-up-an-azure-network"></a>Azure 네트워크를 설정

- Azure 네트워크 설정 Azure VM은 장애 조치 후 처음 만들 때 이 네트워크에 배치됩니다.
- hello 네트워크 hello에 있어야 hello와 동일한 지역 복구 서비스 자격 증명 모음
- Hello Azure 포털에서에서 사이트 복구에서를 설정 하는 네트워크를 사용할 수 있습니다 [리소스 관리자](../resource-manager-deployment-model.md), 또는 클래식 모드에서.
- 시작하기 전에 네트워크를 설정하는 것이 좋습니다. Toodo 필요 하지 않으면 사이트 복구 배포 시이 있습니다.
- [가상 네트워크 가격 책정](https://azure.microsoft.com/pricing/details/virtual-network/)에 대해 알아봅니다.


## <a name="set-up-an-azure-storage-account"></a>Azure 저장소 계정을 설정

- Site Recovery 온-프레미스 컴퓨터 tooAzure 저장소를 복제합니다. Azure Vm 장애 조치 발생 후 hello 저장소에서 생성 됩니다.
- 표준/프리미엄 설정 [Azure 저장소 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold 데이터 tooAzure 복제 합니다.
- [프리미엄 저장소](../storage/common/storage-premium-storage.md) 계속 높게 IO 성능과 짧은 대기 시간 toohost IO가 많은 작업을 필요로 하는 가상 컴퓨터에 대해 일반적으로 사용 됩니다.
- Toouse 프리미엄 계정 toostore 복제 된 데이터를 캡처 지속적인 tooon 온-프레미스 데이터를 변경 표준 저장소 계정을 toostore 복제 로그를 제공 해야 합니다.
- Hello 리소스 모델에 따라 원하는 toouse 장애 조치 Azure Vm에 대 한에서 계정을 설정한 [Resource Manager 모드](../storage/common/storage-create-storage-account.md), 또는 [클래식 모드](../storage/common/storage-create-storage-account.md)합니다.
- 시작하기 전에 저장소 계정을 설정하는 것이 좋습니다. 그렇지 않으면 toodo 해야 사이트 복구 배포 시이 있습니다. hello 계정은 hello에 있어야 hello와 동일한 지역 복구 서비스 자격 증명 모음입니다.
- 저장소 계정에서 사용 되는 사이트 복구 hello 내의 리소스 그룹 동일 이동할 수 없습니다, 구독 또는 다른 구독에서.


## <a name="next-steps"></a>다음 단계

너무 이동[6 단계: 준비 Hyper-v 리소스](hyper-v-site-walkthrough-prepare-hyper-v.md)

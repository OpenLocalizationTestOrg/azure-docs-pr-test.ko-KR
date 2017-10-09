---
title: "Azure 리소스 tooreplicate aaaPrepare 온-프레미스 Azure Site Recovery를 사용 하 여 실제 서버 tooAzure | Microsoft Docs"
description: "필요한 Azure에서 시작 하기 전에 온-프레미스 서버 tooAzure 복제 hello Azure Site Recovery 서비스를 사용 하 여 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: b1d008dac278bc7797188a3c9c15f2a3b5fe12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-tooazure"></a>5 단계: 복제 tooAzure 물리적 서버에 대 한 Azure 리소스 준비


이 문서 tooprepare Azure의에서 hello 지침을 사용 하 여 리소스 hello를 사용 하 여 온-프레미스 서버 tooAzure 복제할 수 있도록 [Azure Site Recovery](site-recovery-overview.md) 서비스입니다.

Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="before-you-start"></a>시작하기 전에

Hello 참고 있는지 확인 하십시오 [필수 구성 요소](physical-walkthrough-prerequisites.md)합니다.

## <a name="set-up-an-azure-account"></a>Azure 계정 설정

- [Microsoft Azure 계정](http://azure.microsoft.com/)을 가져옵니다.
- [평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다.
- 아래에서 사이트 복구에 대 한 지원 hello 영역 확인 **지리적 가용성** 에 [Azure 사이트 복구 가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.
- 에 대 한 자세한 내용은 [사이트 복구 가격](site-recovery-faq.md#pricing), 가져오고, hello [가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.



## <a name="set-up-an-azure-network"></a>Azure 네트워크를 설정

- Azure 네트워크 설정 Azure VM은 장애 조치 후 처음 만들 때 이 네트워크에 배치됩니다.
- Hello Azure 포털에서에서 사이트 복구에서를 설정 하는 네트워크를 사용할 수 있습니다 [리소스 관리자](../resource-manager-deployment-model.md), 또는 클래식 모드에서.
- hello 네트워크 hello에 있어야 hello와 동일한 지역 복구 서비스 자격 증명 모음입니다.
- [가상 네트워크 가격 책정](https://azure.microsoft.com/pricing/details/virtual-network/)에 대해 알아봅니다.
- 장애 조치 후에 [Azure VM 연결](physical-walkthrough-network.md)에 대해 알아봅니다.


## <a name="set-up-an-azure-storage-account"></a>Azure 저장소 계정을 설정

- Site Recovery 온-프레미스 서버 tooAzure 저장소를 복제합니다. Azure Vm 장애 조치 발생 후 hello 저장소에서 생성 됩니다.
- 복제 데이터를 저장할 [Azure Storage 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account)을 설정합니다.
- Hello Azure 포털에서에서 사이트 복구가 צ ְ ײ 저장소 계정 리소스 관리자, 또는 클래식 모드를 설정 합니다.
- 저장소 계정 hello 표준 수 또는 [프리미엄](../storage/common/storage-premium-storage.md)합니다.
- 프리미엄 계정을 설정하는 경우 로그 데이터에 추가 표준 계정이 필요합니다.


## <a name="next-steps"></a>다음 단계

너무 이동[6 단계: 자격 증명 모음 설정](physical-walkthrough-create-vault.md)

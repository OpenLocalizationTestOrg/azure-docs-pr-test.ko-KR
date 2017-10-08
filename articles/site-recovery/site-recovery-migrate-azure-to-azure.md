---
title: "Azure 지역 간의 Azure IaaS Vm aaaMigrate | Microsoft Docs"
description: "하나의 Azure 지역 tooanother에서 Azure Site Recovery toomigrate Azure IaaS 가상 컴퓨터를 사용 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a>Azure Site Recovery를 사용하여 Azure 지역 간에 Azure IaaS 가상 컴퓨터 마이그레이션
## <a name="overview"></a>개요
TooAzure 사이트 복구를 시작! 이 문서를 사용 하 여 Azure 지역 간 toomigrate Azure Vm에 들어 있습니다. 시작하기 전에 다음 사항에 주의하세요.

* Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 Azure Resource Manager 배포 모델과 클래식 배포 모델이 있습니다. Azure는 두 개의 포털 – hello 클래식 배포 모델을 지 원하는 Azure 클래식 포털 hello 및 두 가지 경우 모두 지원 하 여 Azure 포털 hello에 있습니다. hello 기본 단계 마이그레이션에 대 한 hello 같은 리소스 관리자에서 또는 기본에서 사이트 복구를 구성 하는 여부. 그러나 UI 지침 hello 이므로이 문서에서 스크린 샷 hello Azure 포털에 대 한 관련 있습니다.
* **현재 하나의 영역 tooanother에서만 마이그레이션할 수 있습니다. 한 Azure 지역 tooanother에서 Vm 장애 조치할 수 있습니다 하지만 있습니다 수 없는 다시 장애 복구에 다시.**

Hello 또는이 문서의 hello 맨 아래에 설명 이나 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="prerequisites"></a>필수 조건
이 배포에 대해 필요한 사항은 다음과 같습니다.

* **IaaS 가상 컴퓨터**: hello toomigrate 원하는 Vm입니다. 이러한 VM을 실제 컴퓨터로 간주하여 마이그레이션합니다.

## <a name="deployment-steps"></a>배포 단계
이 섹션에서는 hello 새 Azure 포털의 hello 배포 단계를 설명 합니다.

1. [자격 증명 모음을 만듭니다](site-recovery-vmware-to-azure.md).
2. [복제를 활성화합니다](site-recovery-vmware-to-azure.md). Hello, toomigrate을 원본으로 Azure를 선택 하는 Vm에 대 한 복제를 사용 하도록 설정 합니다. 
3. [ 계획되지 않은 장애 조치를 실행합니다](site-recovery-failover.md). 초기 복제가 완료 된 후에 하나의 Azure 지역 tooanother에서 예기치 않은 장애 조치가 실행할 수 있습니다. 필요에 따라 복구 계획을 만들어야 하 고 지역 간 예기치 않은 장애 조치가, toomigrate 여러 가상 컴퓨터를 실행할 수 있습니다. [자세히 알아봅니다](site-recovery-create-recovery-plans.md) .

## <a name="next-steps"></a>다음 단계
[Azure Site Recovery란?](site-recovery-overview.md)

---
title: "Azure 자동화를 사용 하 여 Azure 클라우드 서비스 aaaManage | Microsoft Docs"
description: "Azure 자동화 서비스 hello 규모에 사용 되는 toomanage Azure 클라우드 서비스를 수 있는 방법에 대해 알아봅니다."
services: cloud-services, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: 3789810a-2892-4eef-bf29-c781c1b5af48
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2016
ms.author: timlt
ms.openlocfilehash: 8e920fb94955466bfec71cc332444f5f0ee497a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a>Azure 자동화를 사용하여 Azure 클라우드 서비스 관리
이 가이드에서는 toohello Azure 자동화 서비스 및 Azure 클라우드 서비스의 관리를 사용 하는 toosimplify 수 있는 방법을 소개 합니다.

## <a name="what-is-azure-automation"></a>Azure 자동화 정의
[Azure 자동화](https://azure.microsoft.com/services/automation/) 는 프로세스 자동화를 통해 클라우드 관리를 간소화하기 위한 Azure 서비스입니다. Azure 자동화를 사용 하 여 장기 실행, 수동, 오류가 발생 하기 쉽고 자주 반복 되는 작업에 자동화 된 tooincrease 안정성, 효율성 및 조직에 대 한 시간 toovalue 수 있습니다.

Azure 자동화는 조직의 규모가 커짐에 toomeet 요구에 맞게 확장 되는 매우 안정적이 고 항상 사용 가능한 워크플로 실행 엔진을 제공 합니다. Azure 자동화에서는 작업이 정확히 필요한 시간에 수행되도록 수동, 타사 시스템 또는 예약된 간격에 의해 프로세스를 시작할 수 있습니다.

작동 오버 헤드를 줄이고 확보 IT / DevOps 직원 toofocus 프로그램 클라우드 관리 작업 toobe 이동 하 여 비즈니스 가치를 추가 하는 작업에는 Azure 자동화에 의해 자동으로 실행 합니다.

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a>Azure 자동화를 통해 Azure 클라우드 서비스 관리 향상
Hello에서 사용할 수 있는 hello PowerShell cmdlet을 사용 하 여 Azure 자동화에서 azure 클라우드 서비스를 관리할 수 있습니다 [Azure PowerShell 도구](https://msdn.microsoft.com/library/azure/jj156055.aspx)합니다. Azure 자동화에는 클라우드 서비스 PowerShell cmdlet를 사용할 수 있는 이러한 hello 상자 밖의 hello 서비스 내에서 클라우드 서비스 관리 작업을 모두 수행할 수 있도록 합니다. 또한 Azure 서비스 및 제 3 자 시스템에서 다른 Azure 서비스, tooautomate 복잡 한 작업에 대 한 hello cmdlet 통해 Azure 자동화에서 이러한 cmdlet을 페어링할 수 있는 합니다.

Azure 클라우드 서비스를 포함 하는 Azure 자동화 toomanage의 사용 하 여 몇 가지 예제:

* [Azure Blob 저장소에서 cscfg 또는 cspkg가 업데이트될 때마다 클라우드 서비스의 연속 배포](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [클라우드 서비스 인스턴스를 병렬로 다시 부팅할 때 한 번에 하나의 도메인 업그레이드](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a>다음 단계
Azure 자동화 및 사용 되는 toomanage Azure 클라우드 서비스 수 있는 방법의 hello 기본 사항 학습 한를 했으므로 이러한 링크 toolearn Azure 자동화에 대 한 자세한 수행 합니다.

* [Azure 자동화 개요](../automation/automation-intro.md)
* [내 첫 번째 runbook](../automation/automation-first-runbook-graphical.md)
* [Azure 자동화 학습 맵](https://azure.microsoft.com/documentation/learning-paths/automation/)

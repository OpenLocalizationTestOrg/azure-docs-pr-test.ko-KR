---
title: "Azure 자동화를 사용 하 여 Azure 저장소 aaaManage"
description: "Azure 자동화 서비스 hello 규모에 사용 되는 toomanage Azure 저장소를 수 있는 방법에 대해 알아봅니다."
services: storage, automation
documentationcenter: 
author: jodoglevy
manager: eamono
editor: 
ms.assetid: bac41c39-1d95-46aa-a481-ec17bbb21b40
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: eamono
ms.openlocfilehash: 5edfba1a9ce1f9c81b5bd0889de19099f3d86fc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a>Azure 자동화를 사용하여 Azure 저장소 관리
이 가이드에서는 toohello Azure 자동화 서비스 및 Azure 저장소 blob, 테이블 및 큐의 관리를 사용 하는 toosimplify 수 있는 방법을 소개 합니다.

## <a name="what-is-azure-automation"></a>Azure 자동화 정의
[Azure 자동화](https://azure.microsoft.com/services/automation/) 는 프로세스 자동화를 통해 클라우드 관리를 간소화하기 위한 Azure 서비스입니다. Azure 자동화를 사용 하 여 장기 실행, 수동, 오류가 발생 하기 쉽고 자주 반복 작업 자동화 된 tooincrease 안정성 및 효율성을 높일 수를 업데이트 하 고 조직에 대 한 시간 toovalue 줄일 수 있습니다.

Azure 자동화는 조직의 규모가 커짐에 toomeet 요구에 맞게 확장 되는 매우 안정적이 고 항상 사용 가능한 워크플로 실행 엔진을 제공 합니다. Azure 자동화에서는 작업이 정확히 필요한 시간에 수행되도록 수동, 타사 시스템 또는 예약된 간격에 의해 프로세스를 시작할 수 있습니다.

작동 오버 헤드를 줄이고 확보 IT / DevOps 직원 toofocus 프로그램 클라우드 관리 작업 toobe 이동 하 여 비즈니스 가치를 추가 하는 작업에는 Azure 자동화에 의해 자동으로 실행 합니다.

## <a name="how-can-azure-automation-help-manage-azure-storage"></a>Azure 자동화를 통해 Azure 저장소 관리 향상
사용할 수 있는 hello PowerShell cmdlet을 사용 하 여 Azure 자동화에서 azure 저장소를 관리할 수 있습니다 [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx)합니다. Azure 자동화에는 이러한 저장소 PowerShell cmdlet을 사용할 수 있는 hello 상자 밖의 모든 blob, 테이블 및 hello 서비스 내에서 큐 관리 작업을 수행할 수 있도록 합니다. 또한 Azure 서비스 및 제 3 자 시스템에서 다른 Azure 서비스, tooautomate 복잡 한 작업에 대 한 hello cmdlet 통해 Azure 자동화에서 이러한 cmdlet을 페어링할 수 있는 합니다.

hello [Azure 자동화 runbook 갤러리](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) 에 다양 한 제품 팀과 커뮤니티 runbook tooget Azure 저장소, 다른 Azure 서비스 및 제 3 자 시스템 관리를 자동화를 시작 합니다. Runbook 갤러리에는 다음이 포함됩니다.

* [자동화 서비스를 사용하여 특정 일 수가 지난 Azure 저장소 Blob 제거](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [Azure 저장소에서 Blob 다운로드](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [단일 Azure VM 또는 클라우드 서비스의 모든 VM에 대한 모든 디스크 백업](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a>다음 단계
Azure 자동화 및 사용 되는 toomanage Azure 저장소 blob, 테이블 및 큐 수 있는 방법의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn Azure 자동화에 대 한 자세한 수행 합니다.

Hello Azure 자동화 자습서 [만들기 또는 Azure 자동화에서 runbook을 가져와](../../automation/automation-creating-importing-runbook.md)합니다.


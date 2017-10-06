---
title: "Analysis Services 고가용성 aaaAzure | Microsoft Docs"
description: "Azure Analysis Services 고가용성 보장."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 6e09536c5bd7dc7f88f9b662e1a9f42d2b8c969b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analysis-services-high-availability"></a>Analysis Services 고가용성
이 문서에서는 Azure Analysis Services 서버에 대한 고가용성을 보장하는 방법을 설명합니다. 


## <a name="assuring-high-availability-during-a-service-disruption"></a>서비스가 중단된 동안 고가용성 보장
드문 경우지만 Azure 데이터 센터에서 가동 중단이 발생할 수 있습니다. 가동 중단이 발생하면 몇 분 내지 몇 시간 동안 지속될 수 있는 업무 중단이 발생합니다. 고가용성은 대부분 서버 중복을 통해 획득됩니다. Azure Analysis Services를 통해 하나 이상의 지역에서 추가적인 보조 서버를 만들어 중복을 획득할 수 있습니다. 지역에 대 한 hello 서버와는 오프 라인 상태가 해당 서버에 중복 된 서버, tooassure hello 데이터 및 메타 데이터를 만드는 동기화 할 때 할 수 있습니다.

* 다른 지역 들에 모델 tooredundant 서버를 배포 합니다. 이 방법을 적용할 경우 모든 서버가 동기화되도록 기본 서버와 중복 서버에서 모두 병렬로 데이터를 처리해야 합니다.

* 기본 서버에서 데이터베이스를 백업하고 중복 서버에 복원합니다. 예를 들어 야간 백업 tooAzure 저장소 자동화 하 고 다른 지역 들에 tooother 중복 서버를 복원할 수 있습니다. 

두 경우 모두 주 서버는 중단이 발생 하는 경우 변경 해야 hello 연결 문자열을 보고 클라이언트 tooconnect toohello 서버에서 다른 지역의 데이터 센터에서. 이 변경은 마지막 수단으로, 치명적인 지역 데이터 센터 작동 중단이 발생한 경우에만 고려해야 합니다. 모든 클라이언트에서 연결을 업데이트하기 전에 기본 서버를 호스트하는 데이터 센터 작동 중단 상태에서 다시 온라인 상태로 전환될 가능성이 높습니다. 



## <a name="related-information"></a>관련 정보
[백업 및 복원](analysis-services-backup.md)   
[Azure Analysis Services 관리](analysis-services-manage.md) 


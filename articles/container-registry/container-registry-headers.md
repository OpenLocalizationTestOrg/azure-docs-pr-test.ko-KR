---
title: "컨테이너 레지스트리 리포지토리 aaaAzure | Microsoft Docs"
description: "어떻게 Docker 이미지에 대 한 toouse Azure 컨테이너 레지스트리 리포지토리"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Azure 컨테이너 레지스트리 리포지토리

Azure Container Registry는 다양한 서비스 및 오케스트레이터와 호환됩니다. toomake 것 보다 쉽게 tootrack hello 소스 서비스 및 있는 ACR 사용 되는 에이전트 우리 시작 hello Docker 헤더 필드를 사용 하 여 hello Docker.config 파일에 있습니다.



## <a name="viewing-repositories-in-hello-portal"></a>Hello 포털에서에서 저장소 보기

hello ACR 헤더 hello 형식을 따릅니다.
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* Cloud: Azure, Azure Stack 또는 기타 정부 또는 국가별 Azure 클라우드입니다. Azure Stack 및 정부 클라우드가 현재 지원되지 않지만 이 매개 변수는 앞으로 지원될 수 있습니다.
* Hello 서비스의 서비스: 이름입니다.
* Optionalservicename: 하위 서비스, 또는 toospecify SKU 사용 하 여 서비스에 대 한 선택적 매개 변수 (예: 웹 응용 프로그램 Azure/앱-서비스/웹-앱에 해당).

파트너 서비스 및 orchestrators 것이 좋습니다 toouse 특정 헤더 값 toohelp 된 우리의 원격 분석은입니다. 원하는 경우 toohello 헤더를 전달 하는 hello 값도 수정할 수 있습니다.

hello 값을 원하는 ACR 파트너 toouse toopopulate hello "X-메타-소스-클라이언트" 필드 아래 있습니다.

| 서비스 이름              | 헤더                                |
| ------------------------- | ------------------------------------- |
| Azure Container Service   | azure/compute/azure-container-service |
| App Service - Web Apps    | azure/app-service/web-apps            |
| App Service - Logic Apps  | azure/app-service/logic-apps          |
| 배치                     | azure/compute/batch                   |
| 클라우드 콘솔             | azure/cloud-console                   |
| 함수                 | azure/compute/functions               |
| IoT(사물 인터넷) - 허브  | azure/iot/hub                         |
| HDInsight                 | azure/data/hdinsight                  |
| Jenkins                   | azure/jenkins                         |
| Machine Learning          | azure/data/machile-learning           |
| 서비스 패브릭            | azure/compute/service-fabric          |
| VSTS                      | azure/vsts                            |


## <a name="next-steps"></a>다음 단계
[Orchestrators 레지스트리 및 hello 지원 서비스에 대 한 자세한 정보](container-registry-intro.md)

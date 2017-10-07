---
title: "CLI 스크립트 샘플-Get hello 호스트 이름, 포트 및 Azure Redis Cache에 대 한 키 aaaAzure | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-Get hello 호스트 이름, 포트 및 Azure Redis 캐시 인스턴스에 대 한 키"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a>Azure Redis Cache에 대 한 hello 호스트 이름, 포트 및 키 가져오기

이 시나리오에서는 tooretrieve hello 호스트 이름, 포트 및 키 tooconnect tooan Azure Redis 캐시 인스턴스에 사용 되는 방법을 배웁니다.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 tooretrieve hello 호스트 이름, 키 및 Azure Redis Cache 인스턴스 포트를 수행 하는 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az redis show](https://docs.microsoft.com/cli/azure/redis#show) | Azure Redis Cache 인스턴스에 대한 세부 정보를 검색합니다. |
| [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys) | Azure Redis Cache 인스턴스에 대한 액세스 키를 검색합니다. |


## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 Azure Redis 캐시 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Redis Cache 설명서](../cli-samples.md)합니다.

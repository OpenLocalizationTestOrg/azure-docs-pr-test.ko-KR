---
title: "CLI 스크립트 샘플-Azure Redis Cache의 세부 정보를 가져올 aaaAzure | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Azure Redis Cache의 세부 정보 가져오기"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 155924e6-00d5-4a8c-ba99-5189f300464a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: a3ad1fdf000bbab52e84dbf9f002a5e9fa6d347a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-details-of-an-azure-redis-cache"></a>Azure Redis Cache의 세부 정보 가져오기

이 시나리오에서는 해당 프로 비전 상태를 포함 하 여 Azure Redis Cache의 tooretrieve hello 세부 정보 인스턴스 방법을 배웁니다.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli[main](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Azure Redis Cache")]

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 tooretrieve hello 세부 정보는 Azure Redis 캐시 인스턴스의 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az redis show](https://docs.microsoft.com/cli/azure/redis#show) | Azure Redis Cache 인스턴스에 대한 세부 정보를 검색합니다. |


## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 Azure Redis 캐시 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Redis Cache 설명서](../cli-samples.md)합니다.

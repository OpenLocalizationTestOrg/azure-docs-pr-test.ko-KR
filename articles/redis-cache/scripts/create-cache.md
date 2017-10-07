---
title: "aaaAzure CLI 스크립트 샘플-Azure Redis Cache 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Azure Redis Cache 만들기"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: afd7f6e0-9297-4c98-a95e-597be939cef7
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 85b007a426fbd4752034ec8663835963d140dd75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-redis-cache"></a>Azure Redis Cache 만들기

이 시나리오에서는 Azure Redis 캐시 하는 toocreate 방법을 배웁니다.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 리소스 그룹 및 redis 캐시 명령을 toocreate 다음 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az redis create](https://docs.microsoft.com/cli/azure/redis#create) | Redis Cache 인스턴스를 만듭니다. |


## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 Azure Redis 캐시 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Redis Cache 설명서](../cli-samples.md)합니다.

---
title: "CLI 스크립트 샘플-aaaAzure ACS 클러스터의 크기를 조정 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - ACS 클러스터 크기 조정"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: nepeters
ms.openlocfilehash: 1e07518fc2ca67476d9ef64bb22d75f848a37e43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-an-azure-container-service-cluster"></a>Azure Container Service 클러스터 크기 조정

이 샘플에서는 Azure Container Service의 크기를 조정합니다. 

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a>배포 정리 

Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate hello 배포한 후에 hello를 사용 합니다. Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 |
|---|---|
| [az acs scale](/cli/azure/acs#scale) | ACS 클러스터를 확장합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 Azure 컨테이너 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 컨테이너 서비스 설명서](../cli-samples.md)합니다.


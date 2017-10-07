---
title: "aaaAzure CLI 스크립트 샘플-일괄 처리의 풀 관리 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Batch에서 풀 관리"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a>Azure CLI를 사용하여 Azure Batch 풀 관리

이러한 스크립트 hello Azure CLI toocreate에서 사용할 수 있는 hello 도구 중 일부를 보여 주고 hello Azure 배치 서비스에서 계산 노드는 풀을 관리 합니다.

> [!NOTE]
> 이 샘플의 hello 명령은 Azure 가상 컴퓨터를 만듭니다. 실행 중인 Vm 요금 tooyour 계정을 계산 됩니다. toominimize 이러한 요금 hello 샘플 실행을 완료 하 고 나면 hello Vm을 삭제 합니다. [풀 정리](#clean-up-pools)를 참조하세요.

Batch 풀은 Cloud Services 구성(Windows 전용)이나 Virtual Machine 구성(Windows 및 Linux)의 두 가지 방법을 구성할 수 있습니다. 아래의 hello 샘플 스크립트는 두 구성으로 toocreate 풀링 하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>필수 조건

- 설치 hello hello에 제공 된 hello 지침을 사용 하 여 Azure CLI [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)아직 수행 하지 않은 경우.
- 아직 배치 계정이 없는 경우 새로 만듭니다. 참조 [hello Azure CLI 일괄 처리 계정을 만들고](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) 가 계정을 만들고 하는 예제 스크립트에 대 한 합니다.
- 아직 수행 하지 않은 경우에 시작 작업에서 응용 프로그램 toorun 프로그램을 구성 합니다. 참조 [응용 프로그램 tooAzure Azure CLI 포함 된 일괄 처리 추가](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) 응용 프로그램을 만들고 응용 프로그램 패키지 tooAzure 업로드 하는 예제 스크립트에 대 한 합니다.

## <a name="pool-with-cloud-service-configuration-sample-script"></a>클라우드 서비스 구성이 있는 풀 샘플 스크립트

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a>가상 컴퓨터 구성이 있는 풀 샘플 스크립트

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a>풀 정리

Hello 위의 샘플 스크립트를 실행 한 후 다음 명령 toodelete hello 풀 hello를 실행 합니다.
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 toocreate hello를 사용 하 여 하 고 일괄 처리 풀 조작 합니다.
Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.

| 명령 | 참고 사항 |
|---|---|
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | 배치 계정에 대해 인증합니다.  |
| [az batch application summary list](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | Hello hello 일괄 처리 계정에에서 사용 가능한 응용 프로그램을 나열 합니다.  |
| [az batch pool create](https://docs.microsoft.com/cli/azure/batch/pool#create) | VM의 풀을 만듭니다.  |
| [az batch pool set](https://docs.microsoft.com/cli/azure/batch/pool#set) | 풀의 속성을 업데이트합니다.  |
| [az batch pool node-agent-skus list](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | 사용 가능한 노드 에이전트 SKU 및 이미지 정보를 나열합니다.  |
| [az batch pool resize](https://docs.microsoft.com/cli/azure/batch/pool#resize) | Hello에 실행 중인 Vm의 크기 조정 hello 번호 풀을 지정 합니다.  |
| [az batch pool show](https://docs.microsoft.com/cli/azure/batch/pool#show) | 풀의 hello 속성을 표시 합니다.  |
| [az batch pool delete](https://docs.microsoft.com/cli/azure/batch/pool#delete) | 지정 된 hello 삭제 풀입니다.  |
| [az batch pool autoscale enable](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | 풀에서 자동 확장을 사용하고 수식을 적용합니다.  |
| [az batch pool autoscale disable](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | 풀에서 자동 확장을 사용하지 않습니다.  |
| [az batch node list](https://docs.microsoft.com/cli/azure/batch/node#list) | 모든 나열 hello에 hello 계산 노드가 풀을 지정 합니다.  |
| [az batch node reboot](https://docs.microsoft.com/cli/azure/batch/node#reboot) | Hello 지정 된 계산 노드를 다시 부팅 합니다.  |
| [az batch node delete](https://docs.microsoft.com/cli/azure/batch/node#delete) | Hello에서 delete 나열 된 hello 노드 풀을 지정 합니다.  |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 일괄 처리 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 일괄 처리 CLI 설명서](../batch-cli-samples.md)합니다.


---
title: "aaaAzure CLI 스크립트 샘플-일괄 처리 작업을 실행 합니다. | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Batch로 작업 실행"
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
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a>Azure CLI를 사용하여 Azure Batch에서 실행 중인 작업

이 스크립트 일괄 처리 작업을 만들고 추가 하는 일련의 작업 toohello 작업 합니다. 에 대해서도 설명 방법을 toomonitor 작업 및 작업. 마지막으로, tooquery 효율적으로 hello 작업의 작업에 대 한 정보에 대 한 일괄 처리 서비스 hello 하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>필수 조건

- 설치 hello hello에 제공 된 hello 지침을 사용 하 여 Azure CLI [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)아직 수행 하지 않은 경우.
- 아직 배치 계정이 없는 경우 새로 만듭니다. 참조 [hello Azure CLI 일괄 처리 계정을 만들고](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) 가 계정을 만들고 하는 예제 스크립트에 대 한 합니다.
- 아직 수행 하지 않은 경우에 시작 작업에서 응용 프로그램 toorun 프로그램을 구성 합니다. 참조 [응용 프로그램 tooAzure Azure CLI 포함 된 일괄 처리 추가](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) 응용 프로그램을 만들고 응용 프로그램 패키지 tooAzure 업로드 하는 예제 스크립트에 대 한 합니다.
- 작업을 실행 하는 hello에 풀을 구성 합니다. 클라우드 서비스 구성 또는 가상 컴퓨터 구성으로 풀을 만드는 샘플 스크립트는 [Azure CLI를 사용한 Azure 배치 풀 관리](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool)를 참조하세요.

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a>작업 정리

Hello 위의 샘플 스크립트를 실행 한 후 작업 및 작업의 모든 명령을 tooremove 다음 hello를 실행 합니다. Hello 풀 별도로 삭제 toobe 필요 함을 확인 합니다. 풀 만들기 및 삭제에 대한 자세한 내용은 [Azure CLI를 사용한 Azure 배치 풀 관리](./batch-cli-sample-manage-pool.md)를 참조하세요.

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 일괄 작업 및 작업 명령을 toocreate 다음 hello를 사용 합니다. Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.

| 명령 | 참고 사항 |
|---|---|
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | 배치 계정에 대해 인증합니다.  |
| [az batch job create](https://docs.microsoft.com/cli/azure/batch/job#create) | 배치 작업을 만듭니다.  |
| [az batch job set](https://docs.microsoft.com/cli/azure/batch/job#set) | Batch 작업의 속성을 업데이트합니다.  |
| [az batch job show](https://docs.microsoft.com/cli/azure/batch/job#show) | 지정된 Batch 작업의 세부 정보를 검색합니다.  |
| [az batch task create](https://docs.microsoft.com/cli/azure/batch/task#create) | 추가 작업 toohello 일괄 작업을 지정 합니다.  |
| [az batch task show](https://docs.microsoft.com/cli/azure/batch/task#show) | Hello에서 작업의 검색 hello 세부 정보 일괄 작업을 지정 합니다.  |
| [az batch task list](https://docs.microsoft.com/cli/azure/batch/task#list) | Hello ְ  ¾ hello 지정 된 작업을 나열 합니다.  |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 일괄 처리 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 일괄 처리 CLI 설명서](../batch-cli-samples.md)합니다.

---
title: "Azure CLI 스크립트 샘플 - Batch로 작업 실행 | Microsoft Docs"
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
ms.openlocfilehash: 73d93622d418359be421e043d0af4e4befc6f4b4
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a>Azure CLI를 사용하여 Azure Batch에서 실행 중인 작업

이 스크립트는 Batch 작업을 만들고 일련의 태스크를 작업에 추가합니다. 또한 작업 및 태스크를 모니터링하는 방법도 보여 줍니다. 마지막으로, 작업 관련 정보에 대한 배치 서비스를 효과적으로 쿼리하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>필수 조건

- 아직 Azure CLI를 설치하지 않은 경우 [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)에 있는 지침을 사용하여 설치합니다.
- 아직 배치 계정이 없는 경우 새로 만듭니다. 계정을 만드는 샘플 스크립트에 대한 [Azure CLI로 배치 계정 만들기](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account)를 참조하세요.
- 시작 작업에서 실행할 응용 프로그램을 아직 구성하지 않은 경우 이를 수행합니다. 응용 프로그램을 만들고 Azure에 응용 프로그램 패키지를 업로드하는 샘플 스크립트는 [Azure CLI를 사용하여 응용 프로그램을 Azure 배치에 추가](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application)를 참조하세요.
- 작업이 실행될 풀을 구성합니다. 클라우드 서비스 구성 또는 가상 컴퓨터 구성으로 풀을 만드는 샘플 스크립트는 [Azure CLI를 사용한 Azure 배치 풀 관리](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool)를 참조하세요.

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a>작업 정리

위의 샘플 스크립트를 실행한 후 다음 명령을 실행하여 작업 및 작업의 모든 태스크를 제거합니다. 풀은 별도로 삭제해야 합니다. 풀 만들기 및 삭제에 대한 자세한 내용은 [Azure CLI를 사용한 Azure 배치 풀 관리](./batch-cli-sample-manage-pool.md)를 참조하세요.

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용하여 Batch 작업 및 태스크를 만듭니다. 표에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 참고 사항 |
|---|---|
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#az_batch_account_login) | 배치 계정에 대해 인증합니다.  |
| [az batch job create](https://docs.microsoft.com/cli/azure/batch/job#az_batch_job_create) | 배치 작업을 만듭니다.  |
| [az batch job set](https://docs.microsoft.com/cli/azure/batch/job#az_batch_job_set) | Batch 작업의 속성을 업데이트합니다.  |
| [az batch job show](https://docs.microsoft.com/cli/azure/batch/job#az_batch_job_show) | 지정된 Batch 작업의 세부 정보를 검색합니다.  |
| [az batch task create](https://docs.microsoft.com/cli/azure/batch/task#az_batch_task_create) | 지정된 Batch 작업에 태스크를 추가합니다.  |
| [az batch task show](https://docs.microsoft.com/cli/azure/batch/task#az_batch_task_show) | 지정된 Batch 작업에서 태스크의 세부 정보를 검색합니다.  |
| [az batch task list](https://docs.microsoft.com/cli/azure/batch/task#az_batch_task_list) | 지정된 작업과 연관된 작업을 나열합니다.  |

## <a name="next-steps"></a>다음 단계

Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.

추가 Batch CLI 스크립트 샘플은 [Azure Batch CLI 설명서](../batch-cli-samples.md)에서 확인할 수 있습니다.

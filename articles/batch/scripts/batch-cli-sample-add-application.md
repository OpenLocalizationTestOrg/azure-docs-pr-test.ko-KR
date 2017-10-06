---
title: "일괄 처리에서 응용 프로그램을 추가 하는 CLI 스크립트 샘플-aaaAzure | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Batch로 응용 프로그램 추가"
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
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a>응용 프로그램 tooAzure Azure CLI 포함 된 일괄 처리를 추가합니다.

이 스크립트에서는 어떻게 tooset Azure 배치 풀 또는 작업와 함께 사용할 응용 프로그램을 구성 합니다. 응용 프로그램을 tooset 패키지.zip 파일에 모든 종속 파일을 함께 실행 파일. 이 예제에서는 hello 실행 파일인 zip 파일은 라고 ' 내-응용 프로그램-exe.zip'.

## <a name="prerequisites"></a>필수 조건

- 설치 hello hello에 제공 된 hello 지침을 사용 하 여 Azure CLI [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)아직 수행 하지 않은 경우.
- 아직 배치 계정이 없는 경우 새로 만듭니다. 참조 [hello Azure CLI 일괄 처리 계정을 만들고](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) 가 계정을 만들고 하는 예제 스크립트에 대 한 합니다.

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a>응용 프로그램 정리

Hello 위의 샘플 스크립트를 실행 한 후 응용 프로그램 및 해당 업로드 된 응용 프로그램 패키지의 모든 명령을 tooremove 다음 hello를 실행 합니다.

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 응용 프로그램 및 응용 프로그램 패키지 업로드 명령을 toocreate 다음 hello를 사용 합니다.
Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.

| 명령 | 참고 사항 |
|---|---|
| [az batch application create](https://docs.microsoft.com/cli/azure/batch/application#create) | 응용 프로그램을 만듭니다.  |
| [az batch application set](https://docs.microsoft.com/cli/azure/batch/application#set) | 응용 프로그램의 속성을 업데이트합니다.  |
| [az batch application package create](https://docs.microsoft.com/cli/azure/batch/application/package#create) | 지정 하는 응용 프로그램 패키지 toohello 추가 하는 응용 프로그램입니다.  |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 일괄 처리 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 일괄 처리 CLI 설명서](../batch-cli-samples.md)합니다.

---
title: "CLI 스크립트 샘플-aaaAzure 앱 서비스 계획에서 함수 응용 프로그램 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - App Service 계획에서 함수 앱 만들기"
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c0ffbbbf022e5680e5ae3141e784e7c7bced0bc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a>App Service 계획에서 함수 앱 만들기

이 샘플 스크립트는 함수에 대한 컨테이너인 Azure 함수 앱을 만듭니다. hello 함수 응용 프로그램을 통해 서버 리소스에는 항상 의미 전용된 앱 서비스 계획을 사용 하 여 만들어집니다.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="sample-script"></a>샘플 스크립트

이 스크립트는 전용 [App Service 계획](../functions-scale.md#app-service-plan)을 사용하는 Azure 함수 앱을 만듭니다.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>스크립트 설명

Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다. 이 스크립트 명령 뒤 hello를 사용 합니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account#create) | Azure Storage 계정을 만듭니다. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appserviceplan#create) | App Service 계획을 만듭니다. |
| [az functionapp create](https://docs.microsoft.com/cli/azure/functionapp#delete) | Azure 함수 앱을 만듭니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 Azure 함수 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 함수 설명서](../functions-cli-samples.md)합니다.

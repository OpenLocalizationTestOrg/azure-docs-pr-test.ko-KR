---
title: "함수 앱 만들기 및 GitHub의 함수 코드 배포 | Microsoft Docs"
description: "함수 앱 만들기 및 GitHub의 함수 코드 배포"
services: functions
ms.service: functions
keywords: 
ms.devlang: azurecli
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.custom: mvc
ms.openlocfilehash: 67eb41d89328ab57741c419d8b718e19b947dab1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-app-service"></a>App Service 만들기

이 샘플 스크립트는 관련 리소스를 통해 [소비 계획](../functions-scale.md#consumption-plan)을 사용하여 함수 앱을 만들고 GitHub 리포지토리의 함수 코드를 연속적으로 배포합니다. 이 샘플에서는 다음이 필요합니다.

* 관리 권한이 있는 함수 코드를 포함하는 GitHub 리포지토리
* GitHub 계정에 대한 [PAT(개인 액세스 토큰)](https://help.github.com/articles/creating-an-access-token-for-command-line-use)

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다. `az --version`을 실행하여 버전을 찾습니다. 설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요. 

## <a name="sample-script"></a>샘플 스크립트

이 샘플은 Azure 함수 앱을 만들고 GitHub의 함수 코드를 배포합니다.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>스크립트 설명

테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다. 이 스크립트는 다음을 사용합니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az storage account create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | App Service 계획을 만듭니다. |
| [az functionapp create](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [az appservice web source-control config](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | Git 또는 Mercurial 리포지토리를 사용하여 함수 앱에 연결합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.

추가 Azure Functions CLI 스크립트 샘플은 [Azure Functions 설명서](../functions-cli-samples.md)에서 확인할 수 있습니다.

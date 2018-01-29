---
title: "Azure Storage에 연결하는 Azure Function 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Azure Storage에 연결하는 Azure Function 만들기"
services: functions
documentationcenter: functions
author: ggailey777
manager: cfowler
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 363a3fd1c80538495658720274840b921baa8675
ms.sourcegitcommit: 29bac59f1d62f38740b60274cb4912816ee775ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/29/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a>Azure Storage 계정에 함수 앱 통합

이 샘플 스크립트는 함수 앱 및 Storage 계정을 만듭니다.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

로컬로 CLI를 사용하면 Azure CLI 버전 2.0 이상을 실행하는지 확인합니다. 버전을 확인하려면 `az --version`을 실행합니다. 설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치](/cli/azure/install-azure-cli)를 참조하세요. 

## <a name="sample-script"></a>샘플 스크립트

이 샘플은 Azure 함수 앱을 만들고 앱 설정에 저장소 연결 문자열을 추가합니다.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]


## <a name="clean-up-deployment"></a>배포 정리

스크립트 샘플을 실행한 후에는 다음 명령을 실행하여 리소스 그룹 및 모든 관련된 리소스를 제거합니다.

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용합니다. 테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 참고 사항 |
|---|---|
| [az login](https://docs.microsoft.com/cli/azure/#login) | Azure에 로그인합니다. |
| [az group create](https://docs.microsoft.com/cli/azure/group#az_group_create) | 위치와 함께 리소스 그룹 만들기 |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account) | 저장소 계정 만들기 |
| [az functionapp create](https://docs.microsoft.com/cli/azure/functionapp#az_functionapp_create) | 새로운 함수 앱 만들기 |
| [az group delete](https://docs.microsoft.com/cli/azure/group#az_group_delete) | 정리 |

## <a name="next-steps"></a>다음 단계

Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.

추가 Azure Functions CLI 스크립트 샘플은 [Azure Functions 설명서](../functions-cli-samples.md)에서 확인할 수 있습니다.

---
title: "aaaCreate tooan Azure Cosmos DB에 연결 하는 Azure 함수 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-Azure Cosmos DB tooan 연결 하는 Azure 함수 만들기"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: 0fbc1ebec2dfd480e0cf3ca64f9febcec8af9a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-that-connects-tooan-azure-cosmos-db"></a>Tooan Azure Cosmos DB에 연결 하는 Azure 함수 만들기

이 샘플 스크립트는 Azure 함수 응용 프로그램을 만들고 tooan Azure Cosmos DB 데이터베이스를 연결 합니다.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="sample-script"></a>샘플 스크립트

이 샘플 Azure 함수 응용 프로그램을 만들고 Cosmos DB 끝점 및 액세스 키 tooapp 설정을 추가 합니다.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects tooan Azure Cosmos DB")]

## <a name="clean-up-deployment"></a>배포 정리

Hello 스크립트 예제를 실행 한 후 hello 다음 명령은 사용된 tooremove hello 리소스 그룹 수 및 모든 관련 리소스입니다.

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 뒤 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az login](https://docs.microsoft.com/cli/azure/#login) | 로그인 tooAzure 합니다. |
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 위치와 함께 리소스 그룹 만들기 |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account) | 저장소 계정 만들기 |
| [az functionapp create](https://docs.microsoft.com/cli/azure/functionapp#create) | 새로운 함수 앱 만들기 |
| [az documentdb create](https://docs.microsoft.com/cli/azure/documentdb#create) | DocumentDB 데이터베이스 만들기 |
| [az group delete](https://docs.microsoft.com/cli/azure/group#delete) | 정리 |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 Azure 함수 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 함수 설명서](../functions-cli-samples.md)합니다.





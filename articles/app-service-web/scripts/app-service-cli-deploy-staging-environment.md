---
title: "Azure CLI 스크립트 샘플 - 웹앱 만들기 및 스테이징 환경에 코드 배포 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 웹앱 만들기 및 스테이징 환경에 코드 배포"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 2b995dcd-e471-4355-9fda-00babcdb156e
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d586b50258c32e44f55859aad0a89475e9e4d2eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a>웹앱 만들기 및 스테이징 환경에 코드 배포

이 샘플 스크립트는 "스테이징"이라는 추가 배포 슬롯을 사용하여 App Service에서 웹앱을 만든 다음 "스테이징" 슬롯에 샘플 앱을 배포합니다.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다. `az --version`을 실행하여 버전을 찾습니다. 설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요. 

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli-interactive[기본](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "웹앱 만들기 및 스테이징 환경에 코드 배포")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용합니다. 테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | App Service 계획을 만듭니다. |
| [az webapp create](https://docs.microsoft.com/cli/azure/webapp#create) | Azure 웹앱을 만듭니다. |
| [az webapp deployment slot create](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | 배포 슬롯을 만듭니다. |
| [az webapp deployment source config](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | Git 또는 Mercurial 리포지토리를 사용하여 Azure 웹앱에 연결합니다. |
| [az webapp browse](https://docs.microsoft.com/cli/azure/webapp#browse) | 브라우저에서 Azure 웹앱을 엽니다. |
| [az webapp deployment slot swap](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | 지정된 배포 슬롯을 프로덕션으로 교환합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.

추가 App Service CLI 스크립트 샘플은 [Azure App Service 설명서](../app-service-cli-samples.md)에서 확인할 수 있습니다.

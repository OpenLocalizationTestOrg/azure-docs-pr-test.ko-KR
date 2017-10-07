---
title: "aaaAzure CLI 스크립트 샘플-웹 응용 프로그램을 높은 availabilty 아키텍처를 통해 전 세계 확장 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 전세계에 고가용성 아키텍처를 가진 웹앱 확장"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4033a50-0e05-4505-8ce8-c876204b2acc
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b72fbccd7f2aaab58e4b4721e14dca14146c7c72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a>전세계에 고가용성 아키텍처를 가진 웹앱 확장

이 시나리오에서는 리소스 그룹, 두 개의 App Service 계획, 두 개의 웹앱, Traffic Manager 프로필 및 두 개의 Traffic Manager 끝점을 만듭니다. 우선을 사용할 수 있는 나면 hello 실습 완료 되 면 수 있는 아키텍처는 hello 가장 낮은 네트워크 대기 시간에 따라 웹 응용 프로그램의 글로벌 가용성을 제공 합니다.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 


## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate 리소스 그룹, 웹 응용 프로그램, 트래픽 관리자 프로필 뒤 hello를 사용 하 고 모든 관련 리소스입니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | App Service 계획을 만듭니다. Azure 웹앱에 대한 서버 팜과 비슷합니다. |
| [az webapp create](https://docs.microsoft.com/cli/azure/webapp#create) | Azure 웹앱을 만듭니다. |
| [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | Azure Traffic Manager 프로필을 만듭니다. |
| [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | 끝점 tooan Azure 트래픽 관리자 프로필을 추가합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 응용 프로그램 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 앱 서비스 설명서](../app-service-cli-samples.md)합니다.

---
title: "CLI 스크립트 샘플 응용 프로그램의 고가용성에 대 한 트래픽 라우팅할 aaaAzure | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 응용 프로그램 고가용성을 위한 트래픽 라우팅"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a>응용 프로그램 고가용성을 위한 트래픽 라우팅

이 스크립트는 리소스 그룹, 2개 App Service 계획, 2개 웹앱, Traffic Manager 프로필 및 2개 Traffic Manager 끝점을 만듭니다. 트래픽 관리자는 hello 기본 지역의 hello 응용 프로그램을 사용할 수 없는 경우 hello 기본 지역으로 한 영역과 toohello 보조 지역에 트래픽을 toohello 응용 프로그램을 전달 합니다. Hello 스크립트를 실행 하기 전에 hello MyWebApp, MyWebAppL1 리소스 및 MyWebAppL2 Azure 간의 toounique 값 값입니다. Hello 스크립트를 실행 한 후 hello 앱 URL mywebapp.trafficmanager.net hello 사용 하 여 hello 기본 영역에 액세스할 수 있습니다.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a>배포 정리 

Hello 스크립트 예제를 실행 한 후 hello 다음 명령을 사용 하는 tooremove hello 리소스 그룹, 앱 서비스 앱 및 관련 된 모든 리소스 수 있습니다.

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate 리소스 그룹, 웹 응용 프로그램, 트래픽 관리자 프로필 뒤 hello를 사용 하 고 모든 관련 리소스입니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | App Service 계획을 만듭니다. Azure 웹앱에 대한 서버 팜과 비슷합니다. |
| [az appservice web create](https://docs.microsoft.com/cli/azure/appservice/web#create) | Hello 앱 서비스 계획 내에서 Azure 웹 앱을 만듭니다. |
| [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | Azure Traffic Manager 프로필을 만듭니다. |
| [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | 끝점 tooan Azure 트래픽 관리자 프로필을 추가합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 응용 프로그램 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 네트워킹 설명서](../cli-samples.md)합니다.

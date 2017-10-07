---
title: "PowerShell 스크립트 샘플-aaaAzure 고가용성 아키텍처를 통해 전 세계 웹 앱 확장 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 전세계에 고가용성 아키텍처를 가진 웹앱 확장"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1fcda23250efe4966d63c5dfa744b76c26f3762a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a>전세계에 고가용성 아키텍처를 가진 웹앱 확장

이 시나리오에서는 리소스 그룹, 두 개의 App Service 계획, 두 개의 웹앱, Traffic Manager 프로필 및 두 개의 Traffic Manager 끝점을 만듭니다. 우선을 사용할 수 있는 나면 hello 실습 완료 되 면 수 있는 아키텍처는 hello 가장 낮은 네트워크 대기 시간에 따라 웹 응용 프로그램의 글로벌 가용성을 제공 합니다.

필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]

## <a name="clean-up-deployment"></a>배포 정리 

Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹, 웹 앱 및 관련 된 모든 리소스를 수 있습니다.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 뒤 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [New-AzureRMTrafficManagerProfile](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | Traffic Manager 프로필을 만듭니다. |
| [New-AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | App Service 계획을 만듭니다. |
| [New-AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | 웹앱을 만듭니다. |
| [New-AzureRMTrafficManagerEndpoint](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | Traffic Manager 프로필에서 끝점을 만듭니다. |

## <a name="next-steps"></a>다음 단계

Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

Azure 앱 서비스 웹 앱에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../app-service-powershell-samples.md)합니다.

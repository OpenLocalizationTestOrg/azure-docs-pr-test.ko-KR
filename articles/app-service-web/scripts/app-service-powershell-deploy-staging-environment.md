---
title: "PowerShell 스크립트 샘플-aaaAzure 웹 앱 만들기 및 코드 tooa 스테이징 환경 배포 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플-웹 앱 만들기 및 코드 tooa 스테이징 환경 배포"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 27cf0680-c3a9-4a58-9f71-6dec09f6b874
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5c74b962955770637173f1fd4f49342fec54ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a>웹 앱을 만들고 코드 tooa 스테이징 환경 배포

이 샘플 스크립트 웹 응용 프로그램 앱 서비스의 "준비"를 호출 하는 추가 배포 슬롯으로 만들고 "스테이징" 슬롯 샘플 앱 toohello 다음 배포 합니다.

필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code tooa staging environment")]

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
| [New-AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | App Service 계획을 만듭니다. |
| [New-AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | 웹앱을 만듭니다. |
| [Set-AzureRmAppServicePlan](/powershell/module/azurerm.websites/set-azurermappserviceplan) | 앱 서비스 계획 toochange 해당 가격 책정 계층을 수정합니다. |
| [New-AzureRmWebAppSlot](/powershell/module/azurerm.websites/new-azurermwebappslot) | 웹앱에 대한 배포 슬롯을 만듭니다. |
| [Set-AzureRmResource](/powershell/module/azurerm.resources/set-azurermresource) | 리소스 그룹에서 리소스를 수정합니다. |
| [Swap-AzureRmWebAppSlot](/powershell/module/azurerm.websites/swap-azurermwebappslot) | 웹앱의 배포 슬롯을 프로덕션으로 교환합니다. |

## <a name="next-steps"></a>다음 단계

Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

Azure 앱 서비스 웹 앱에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../app-service-powershell-samples.md)합니다.

---
title: "PowerShell 스크립트 샘플-aaaAzure 웹 응용 프로그램을 수동으로 확장 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 수동으로 웹앱 크기 조정"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: de5d4285-9c7d-4735-a695-288264047375
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c749031fbe6c6bcbb25395387b4f32b2ba75cef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a>수동으로 웹앱 크기 조정

이 시나리오에서는 리소스 그룹 toocreate 배웁니다 앱 서비스 계획 및 웹 앱입니다. 단일 인스턴스 toomultiple 인스턴스에서 hello 앱 서비스 계획을 확장 한 다음 됩니다.

필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]

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
| [Set-AzureRmWebApp](/powershell/module/azurerm.websites/set-azurermwebapp) | 웹앱의 구성을 수정합니다. |

## <a name="next-steps"></a>다음 단계

Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

Azure 앱 서비스 웹 앱에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../app-service-powershell-samples.md)합니다.

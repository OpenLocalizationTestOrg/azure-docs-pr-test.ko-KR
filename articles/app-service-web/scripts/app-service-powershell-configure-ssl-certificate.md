---
title: "PowerShell 스크립트 샘플-aaaAzure 바인딩할 사용자 지정 SSL 인증서 tooa 웹 앱 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플-바인딩 사용자 지정 SSL 인증서 tooa 웹 앱"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 23e83b74-614a-49a0-bc08-7542120eeec5
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6e249ceedb9e2b8872dd0bc8b0aea0d718b28dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a>사용자 지정 SSL 인증서 tooa 웹 응용 프로그램 바인딩

이 샘플 스크립트과 해당 관련된 리소스에 앱 서비스 웹 앱을 만듭니다 다음 사용자 지정 도메인 이름 tooit의 hello SSL 인증서를 바인딩합니다. 

필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview)합니다. 또한 다음 사항을 확인합니다.

- Hello를 사용 하 여 Azure와의 연결을 만들었습니다 `az login` 명령입니다.
- 액세스 tooyour 도메인 등록자의 DNS 구성 페이지를 해야합니다.
- 유효한 해야합니다. PFX 파일 및 SSL hello에 대 한 암호 인증서 tooupload 원하고 바인딩합니다.

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate tooa web app")]

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
| [Set-AzureRmWebApp](/powershell/module/azurerm.websites/set-azurermwebapp) | 웹앱의 구성을 수정합니다. |
| [New-AzureRmWebAppSSLBinding](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | 웹앱에 SSL 인증서 바인딩을 만듭니다. |

## <a name="next-steps"></a>다음 단계

Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

Azure 앱 서비스 웹 앱에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../app-service-powershell-samples.md)합니다.

---
title: "PowerShell을 사용 하 여 Azure Analysis Services 서버 aaaCreate | Microsoft Docs"
description: "자세한 방법을 toocreate Azure Analysis Services PowerShell을 사용 하 여 서버"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a>PowerShell을 사용하여 Azure Analysis Services 서버 만들기

이 퀵 스타트의 설명에서 사용 하 여 PowerShell hello 명령줄 toocreate Azure Analysis Services 서버에는 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md) Azure 구독에 있습니다.

이 작업을 수행하려면 Azure PowerShell 모듈 버전 4.0 이상이 필요합니다. toofind hello 버전을 실행 ` Get-Module -ListAvailable AzureRM`합니다. tooinstall 또는 업그레이드를 참조 하세요. [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다. 

> [!NOTE]
> 서버를 만들면 새로운 유료 서비스가 생성될 수 있습니다. toolearn 더 참조 [Analysis Services 가격](https://azure.microsoft.com/pricing/details/analysis-services/)합니다.

## <a name="prerequisites"></a>필수 조건
toocomplete 해야이 빠른 시작:

* **Azure 구독**: 방문 [Azure 무료 평가판](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate 계정.
* **Azure Active Directory**: 구독이 Azure Active Directory 테넌트와 연결되어 있고 해당 디렉터리에 계정이 있어야 합니다. toolearn 더 참조 [인증 및 사용자 권한을](analysis-services-manage-users.md)합니다.

## <a name="import-azurermanalysisservices-module"></a>AzureRm.AnalysisServices 모듈 가져오기
hello를 사용 하면 구독에 서버 toocreate [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) 모듈 구성 요소입니다. PowerShell 세션에 hello AzureRm.AnalysisServices 모듈을 로드 합니다.

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a>TooAzure에 로그인

Hello를 사용 하 여 Azure 구독 tooyour 로그인 [추가 AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) 명령입니다. 지시를 따른 hello 화면에 표시 합니다.

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a>리소스 그룹 만들기
 
[Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md)은 Azure 리소스가 그룹으로 배포되고 관리되는 논리 컨테이너입니다. 서버를 만들 때 구독에서 리소스 그룹을 지정해야 합니다. 리소스 그룹이 아직 없는 경우 hello를 사용 하 여 한 새를 만들 수 있습니다 [새로 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 명령입니다. hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello 미국 서 부 지역에 있습니다.

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a>서버 만들기

Hello를 사용 하 여 새 서버 만들기 [새로 AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) 명령입니다. hello 다음 예제에서는 hello D1 계층에서는 hello 미국 서 부 지역에서 myResourceGroup myServer 라는 서버를 만들고 지정 philipc@adventureworks.com 서버 관리자입니다.

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a>리소스 정리

Hello를 사용 하 여 hello 서버 구독에서 제거할 수 있습니다 [제거 AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) 명령입니다. 이 컬렉션의 다른 빠른 시작 및 자습서로 계속하는 경우에는 서버를 제거하지 마세요. hello 다음 예제에서는 hello 서버를 제거 hello 이전 단계에서 만든 합니다.


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a>다음 단계
[PowerShell을 사용하여 Azure Analysis Services 관리](analysis-services-powershell.md)   
[SSDT에서 모델 배포](analysis-services-deploy.md)   
[Azure Portal에서 모델 만들기](analysis-services-create-model-portal.md)
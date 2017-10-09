---
title: "웹 앱 tooa 저장소 계정을 연결 하세요. PowerShell 스크립트 샘플-aaaAzure | Microsoft Docs"
description: "Azure PowerShell 스크립트 예제-웹 응용 프로그램 tooa 저장소 계정 연결"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4831bdc-2068-4883-9474-0b34c2e3e255
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 07693366d32fbaefe92c18df67ded81661e1a2df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-storage-account"></a><span data-ttu-id="099c4-103">웹 앱 tooa 저장소 계정을 연결 하세요.</span><span class="sxs-lookup"><span data-stu-id="099c4-103">Connect a web app tooa storage account</span></span>

<span data-ttu-id="099c4-104">이 시나리오에서는 toocreate Azure 저장소 계정 및 Azure 웹 앱에 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="099c4-104">In this scenario you will learn how toocreate an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="099c4-105">그런 다음 응용 프로그램 설정을 사용 하 여 hello 저장소 계정 toohello 웹 앱을 연결할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="099c4-105">Then you will link hello storage account toohello web app using app settings.</span></span>

<span data-ttu-id="099c4-106">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="099c4-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="099c4-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="099c4-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app tooa storage account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="099c4-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="099c4-108">Clean up deployment</span></span> 

<span data-ttu-id="099c4-109">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹, 웹 앱 및 관련 된 모든 리소스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="099c4-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="099c4-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="099c4-110">Script explanation</span></span>

<span data-ttu-id="099c4-111">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="099c4-111">This script uses hello following commands.</span></span> <span data-ttu-id="099c4-112">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="099c4-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="099c4-113">명령</span><span class="sxs-lookup"><span data-stu-id="099c4-113">Command</span></span> | <span data-ttu-id="099c4-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="099c4-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="099c4-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="099c4-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="099c4-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="099c4-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="099c4-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="099c4-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="099c4-118">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="099c4-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="099c4-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="099c4-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="099c4-120">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="099c4-120">Creates a web app.</span></span> |
| [<span data-ttu-id="099c4-121">New-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="099c4-121">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="099c4-122">저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="099c4-122">Creates a Storage account.</span></span> |
| [<span data-ttu-id="099c4-123">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="099c4-123">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="099c4-124">Azure 저장소 계정에 대 한 hello 선택 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="099c4-124">Gets hello access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="099c4-125">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="099c4-125">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="099c4-126">웹앱의 구성을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="099c4-126">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="099c4-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="099c4-127">Next steps</span></span>

<span data-ttu-id="099c4-128">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="099c4-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="099c4-129">Azure 앱 서비스 웹 앱에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../app-service-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="099c4-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>

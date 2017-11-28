---
title: "Azure PowerShell 스크립트 샘플 - 저장소 계정에 웹앱 연결 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 저장소 계정에 웹앱 연결"
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
ms.openlocfilehash: 481f3efdb1cbbeba328183da7e320c7e5b819b3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-a-web-app-to-a-storage-account"></a><span data-ttu-id="1a57e-103">저장소 계정에 웹앱 연결</span><span class="sxs-lookup"><span data-stu-id="1a57e-103">Connect a web app to a storage account</span></span>

<span data-ttu-id="1a57e-104">이 시나리오에서는 Azure Storage 계정 및 Azure 웹앱을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1a57e-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="1a57e-105">그런 다음 앱 설정을 사용하여 저장소 계정을 웹앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1a57e-105">Then you will link the storage account to the web app using app settings.</span></span>

<span data-ttu-id="1a57e-106">필요한 경우 [Azure PowerShell 가이드](/powershell/azure/overview)에 있는 지침을 사용하여 Azure PowerShell을 설치한 다음, `Login-AzureRmAccount`를 실행하여 Azure에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1a57e-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="1a57e-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="1a57e-107">Sample script</span></span>

<span data-ttu-id="1a57e-108">[!code-powershell[기본](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "저장소 계정에 웹앱 연결")]</span><span class="sxs-lookup"><span data-stu-id="1a57e-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app to a storage account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="1a57e-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="1a57e-109">Clean up deployment</span></span> 

<span data-ttu-id="1a57e-110">스크립트 샘플을 실행한 후에는 다음 명령을 사용하여 리소스 그룹, 웹앱 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a57e-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="1a57e-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="1a57e-111">Script explanation</span></span>

<span data-ttu-id="1a57e-112">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1a57e-112">This script uses the following commands.</span></span> <span data-ttu-id="1a57e-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a57e-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1a57e-114">명령</span><span class="sxs-lookup"><span data-stu-id="1a57e-114">Command</span></span> | <span data-ttu-id="1a57e-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="1a57e-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1a57e-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1a57e-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1a57e-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a57e-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1a57e-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="1a57e-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="1a57e-119">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a57e-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="1a57e-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="1a57e-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="1a57e-121">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a57e-121">Creates a web app.</span></span> |
| [<span data-ttu-id="1a57e-122">New-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="1a57e-122">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="1a57e-123">저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a57e-123">Creates a Storage account.</span></span> |
| [<span data-ttu-id="1a57e-124">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="1a57e-124">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="1a57e-125">Azure Storage 계정의 선택키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1a57e-125">Gets the access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="1a57e-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="1a57e-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="1a57e-127">웹앱의 구성을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="1a57e-127">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1a57e-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1a57e-128">Next steps</span></span>

<span data-ttu-id="1a57e-129">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a57e-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1a57e-130">Azure App Service Web Apps에 대한 추가 Azure PowerShell 샘플은 [Azure PowerShell 샘플](../app-service-powershell-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a57e-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>

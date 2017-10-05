---
title: "Azure PowerShell 스크립트 샘플 - FTP를 사용하여 웹앱에 파일 업로드 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - FTP를 사용하여 웹앱에 파일 업로드"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: b7d46d6f-44fd-454c-8008-87dab6eefbc1
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 96b99110b63b037746fcc40eb15db5d718eb71a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="upload-files-to-a-web-app-using-ftp"></a><span data-ttu-id="4d220-103">FTP를 사용하여 웹앱에 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="4d220-103">Upload files to a web app using FTP</span></span>

<span data-ttu-id="4d220-104">이 샘플 스크립트는 관련된 리소스를 사용하여 App Service에서 웹앱을 만든 다음 FTP([WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)을 통해)를 사용하여 웹앱 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="4d220-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="4d220-105">필요한 경우 [Azure PowerShell 가이드](/powershell/azure/overview)에 있는 지침을 사용하여 Azure PowerShell을 설치한 다음, `Login-AzureRmAccount`을 실행하여 Azure와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4d220-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="4d220-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="4d220-106">Sample script</span></span>

<span data-ttu-id="4d220-107">[!code-powershell[기본](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "FTP를 사용하여 웹앱에 파일 업로드")]</span><span class="sxs-lookup"><span data-stu-id="4d220-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files to a web app using FTP")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4d220-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="4d220-108">Clean up deployment</span></span> 

<span data-ttu-id="4d220-109">스크립트 샘플을 실행한 후에는 다음 명령을 사용하여 리소스 그룹, 웹앱 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d220-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="4d220-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="4d220-110">Script explanation</span></span>

<span data-ttu-id="4d220-111">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d220-111">This script uses the following commands.</span></span> <span data-ttu-id="4d220-112">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d220-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4d220-113">명령</span><span class="sxs-lookup"><span data-stu-id="4d220-113">Command</span></span> | <span data-ttu-id="4d220-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="4d220-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4d220-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4d220-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4d220-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d220-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4d220-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="4d220-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="4d220-118">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d220-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="4d220-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="4d220-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="4d220-120">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d220-120">Creates a web app.</span></span> |
| [<span data-ttu-id="4d220-121">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="4d220-121">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="4d220-122">웹앱의 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4d220-122">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4d220-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d220-123">Next steps</span></span>

<span data-ttu-id="4d220-124">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d220-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4d220-125">Azure App Service Web Apps에 대한 추가 Azure PowerShell 샘플은 [Azure PowerShell 샘플](../app-service-powershell-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d220-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>

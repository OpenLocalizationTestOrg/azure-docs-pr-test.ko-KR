---
title: "PowerShell 스크립트 샘플-FTP를 사용 하 여 업로드 파일 tooa 웹 앱 aaaAzure | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플-FTP를 사용 하 여 업로드 파일 tooa 웹 앱"
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
ms.openlocfilehash: 32a0a529e94c1315cc6730faf23fca2693c50ffb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-tooa-web-app-using-ftp"></a><span data-ttu-id="271cb-103">FTP를 사용 하 여 파일 tooa 웹 앱을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="271cb-103">Upload files tooa web app using FTP</span></span>

<span data-ttu-id="271cb-104">이 샘플 스크립트는 관련된 리소스를 사용하여 App Service에서 웹앱을 만든 다음 FTP([WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)을 통해)를 사용하여 웹앱 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="271cb-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="271cb-105">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="271cb-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="271cb-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="271cb-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files tooa web app using FTP")]

## <a name="clean-up-deployment"></a><span data-ttu-id="271cb-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="271cb-107">Clean up deployment</span></span> 

<span data-ttu-id="271cb-108">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹, 웹 앱 및 관련 된 모든 리소스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="271cb-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="271cb-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="271cb-109">Script explanation</span></span>

<span data-ttu-id="271cb-110">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="271cb-110">This script uses hello following commands.</span></span> <span data-ttu-id="271cb-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="271cb-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="271cb-112">명령</span><span class="sxs-lookup"><span data-stu-id="271cb-112">Command</span></span> | <span data-ttu-id="271cb-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="271cb-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="271cb-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="271cb-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="271cb-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="271cb-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="271cb-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="271cb-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="271cb-117">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="271cb-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="271cb-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="271cb-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="271cb-119">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="271cb-119">Creates a web app.</span></span> |
| [<span data-ttu-id="271cb-120">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="271cb-120">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="271cb-121">웹앱의 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="271cb-121">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="271cb-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="271cb-122">Next steps</span></span>

<span data-ttu-id="271cb-123">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="271cb-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="271cb-124">Azure 앱 서비스 웹 앱에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../app-service-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="271cb-124">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>

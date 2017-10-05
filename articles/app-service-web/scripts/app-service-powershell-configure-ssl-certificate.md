---
title: "Azure PowerShell 스크립트 샘플 - 웹앱에 사용자 지정 SSL 인증서 바인딩 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 웹앱에 사용자 지정 SSL 인증서 바인딩"
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
ms.openlocfilehash: de8deccadcd9571be75447a117888bf2b3f571a0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="0b25d-103">웹앱에 사용자 지정 SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="0b25d-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="0b25d-104">이 샘플 스크립트는 해당 관련된 리소스를 사용하여 App Service에서 웹앱을 만든 다음 사용자 지정 도메인 이름의 SSL 인증서를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="0b25d-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> 

<span data-ttu-id="0b25d-105">필요한 경우 [Azure PowerShell 가이드](/powershell/azure/overview)에 있는 지침을 사용하여 Azure PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0b25d-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="0b25d-106">또한 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b25d-106">Also, ensure that:</span></span>

- <span data-ttu-id="0b25d-107">`az login` 명령을 사용하여 Azure와 연결했습니다.</span><span class="sxs-lookup"><span data-stu-id="0b25d-107">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="0b25d-108">도메인 등록 기관의 DNS 구성 페이지에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b25d-108">You have access to your domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="0b25d-109">업로드하고 바인딩하려는 SSL 인증서에 사용할 .PFX 파일 및 해당 암호가 유효해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b25d-109">You have a valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="0b25d-110">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="0b25d-110">Sample script</span></span>

<span data-ttu-id="0b25d-111">[!code-powershell[기본](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "웹앱에 사용자 지정 SSL 인증서 바인딩")]</span><span class="sxs-lookup"><span data-stu-id="0b25d-111">[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0b25d-112">배포 정리</span><span class="sxs-lookup"><span data-stu-id="0b25d-112">Clean up deployment</span></span> 

<span data-ttu-id="0b25d-113">스크립트 샘플을 실행한 후에는 다음 명령을 사용하여 리소스 그룹, 웹앱 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b25d-113">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="0b25d-114">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="0b25d-114">Script explanation</span></span>

<span data-ttu-id="0b25d-115">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b25d-115">This script uses the following commands.</span></span> <span data-ttu-id="0b25d-116">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b25d-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0b25d-117">명령</span><span class="sxs-lookup"><span data-stu-id="0b25d-117">Command</span></span> | <span data-ttu-id="0b25d-118">참고 사항</span><span class="sxs-lookup"><span data-stu-id="0b25d-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0b25d-119">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0b25d-119">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="0b25d-120">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b25d-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0b25d-121">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="0b25d-121">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="0b25d-122">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b25d-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="0b25d-123">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="0b25d-123">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="0b25d-124">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b25d-124">Creates a web app.</span></span> |
| [<span data-ttu-id="0b25d-125">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="0b25d-125">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="0b25d-126">App Service 계획을 수정하여 해당 가격 책정 계층을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0b25d-126">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="0b25d-127">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="0b25d-127">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="0b25d-128">웹앱의 구성을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b25d-128">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="0b25d-129">New-AzureRmWebAppSSLBinding</span><span class="sxs-lookup"><span data-stu-id="0b25d-129">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="0b25d-130">웹앱에 SSL 인증서 바인딩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b25d-130">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0b25d-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0b25d-131">Next steps</span></span>

<span data-ttu-id="0b25d-132">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b25d-132">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0b25d-133">Azure App Service Web Apps에 대한 추가 Azure PowerShell 샘플은 [Azure PowerShell 샘플](../app-service-powershell-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b25d-133">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>

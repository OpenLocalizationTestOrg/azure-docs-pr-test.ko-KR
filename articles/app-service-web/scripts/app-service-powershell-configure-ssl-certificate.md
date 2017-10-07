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
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="bff56-103">사용자 지정 SSL 인증서 tooa 웹 응용 프로그램 바인딩</span><span class="sxs-lookup"><span data-stu-id="bff56-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="bff56-104">이 샘플 스크립트과 해당 관련된 리소스에 앱 서비스 웹 앱을 만듭니다 다음 사용자 지정 도메인 이름 tooit의 hello SSL 인증서를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="bff56-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> 

<span data-ttu-id="bff56-105">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="bff56-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="bff56-106">또한 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bff56-106">Also, ensure that:</span></span>

- <span data-ttu-id="bff56-107">Hello를 사용 하 여 Azure와의 연결을 만들었습니다 `az login` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="bff56-107">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="bff56-108">액세스 tooyour 도메인 등록자의 DNS 구성 페이지를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="bff56-108">You have access tooyour domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="bff56-109">유효한 해야합니다. PFX 파일 및 SSL hello에 대 한 암호 인증서 tooupload 원하고 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="bff56-109">You have a valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="bff56-110">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="bff56-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="bff56-111">배포 정리</span><span class="sxs-lookup"><span data-stu-id="bff56-111">Clean up deployment</span></span> 

<span data-ttu-id="bff56-112">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹, 웹 앱 및 관련 된 모든 리소스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff56-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="bff56-113">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="bff56-113">Script explanation</span></span>

<span data-ttu-id="bff56-114">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff56-114">This script uses hello following commands.</span></span> <span data-ttu-id="bff56-115">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="bff56-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="bff56-116">명령</span><span class="sxs-lookup"><span data-stu-id="bff56-116">Command</span></span> | <span data-ttu-id="bff56-117">참고 사항</span><span class="sxs-lookup"><span data-stu-id="bff56-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bff56-118">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="bff56-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="bff56-119">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bff56-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bff56-120">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="bff56-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="bff56-121">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bff56-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="bff56-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="bff56-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="bff56-123">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bff56-123">Creates a web app.</span></span> |
| [<span data-ttu-id="bff56-124">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="bff56-124">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="bff56-125">앱 서비스 계획 toochange 해당 가격 책정 계층을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="bff56-125">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="bff56-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="bff56-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="bff56-127">웹앱의 구성을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="bff56-127">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="bff56-128">New-AzureRmWebAppSSLBinding</span><span class="sxs-lookup"><span data-stu-id="bff56-128">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="bff56-129">웹앱에 SSL 인증서 바인딩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bff56-129">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bff56-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bff56-130">Next steps</span></span>

<span data-ttu-id="bff56-131">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="bff56-131">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="bff56-132">Azure 앱 서비스 웹 앱에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../app-service-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bff56-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>

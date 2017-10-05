---
title: "Azure PowerShell 스크립트 샘플 - SQL Database에 웹앱 연결 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - SQL Database에 웹앱 연결"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 055440a9-fff1-49b2-b964-9c95b364e533
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 5312bf6b81d1cc48490b71c3f77323cca23e1559
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="0eb19-103">SQL Database에 웹앱 연결</span><span class="sxs-lookup"><span data-stu-id="0eb19-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="0eb19-104">이 시나리오에서는 Azure SQL Database 및 Azure 웹앱을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0eb19-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="0eb19-105">그런 다음 앱 설정을 사용하여 SQL Database를 웹앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb19-105">Then you will link the SQL database to the web app using app settings.</span></span>

<span data-ttu-id="0eb19-106">필요한 경우 [Azure PowerShell 가이드](/powershell/azure/overview)에 있는 지침을 사용하여 Azure PowerShell을 설치한 다음, `Login-AzureRmAccount`를 실행하여 Azure에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb19-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="0eb19-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="0eb19-107">Sample script</span></span>

<span data-ttu-id="0eb19-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "SQL Database에 웹앱 연결")]</span><span class="sxs-lookup"><span data-stu-id="0eb19-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app to a SQL database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0eb19-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="0eb19-109">Clean up deployment</span></span> 

<span data-ttu-id="0eb19-110">스크립트 샘플을 실행한 후에는 다음 명령을 사용하여 리소스 그룹, 웹앱 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb19-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="0eb19-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="0eb19-111">Script explanation</span></span>

<span data-ttu-id="0eb19-112">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb19-112">This script uses the following commands.</span></span> <span data-ttu-id="0eb19-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb19-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0eb19-114">명령</span><span class="sxs-lookup"><span data-stu-id="0eb19-114">Command</span></span> | <span data-ttu-id="0eb19-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="0eb19-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0eb19-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0eb19-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="0eb19-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0eb19-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0eb19-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="0eb19-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="0eb19-119">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0eb19-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="0eb19-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="0eb19-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="0eb19-121">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0eb19-121">Creates a web app.</span></span> |
| [<span data-ttu-id="0eb19-122">New-AzureRMSQLServer</span><span class="sxs-lookup"><span data-stu-id="0eb19-122">New-AzureRMSQLServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="0eb19-123">SQL Database 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0eb19-123">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="0eb19-124">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="0eb19-124">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="0eb19-125">SQL Database 서버에 대한 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0eb19-125">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="0eb19-126">New-AzureRMSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="0eb19-126">New-AzureRMSQLDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="0eb19-127">데이터베이스 또는 Elastic Database를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0eb19-127">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="0eb19-128">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="0eb19-128">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="0eb19-129">웹앱의 구성을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb19-129">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0eb19-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0eb19-130">Next steps</span></span>

<span data-ttu-id="0eb19-131">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eb19-131">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0eb19-132">Azure App Service Web Apps에 대한 추가 Azure PowerShell 샘플은 [Azure PowerShell 샘플](../app-service-powershell-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb19-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>

---
title: "Azure VM에 대한 템플릿 다운로드 | Microsoft Docs"
description: "VM에 대한 템플릿을 다운로드하면 Resource Manager 배포 모델에서 배포를 자동화할 수 있습니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 9e4c0c3cf0e233447369a24b1d5fe27495abd1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="download-the-template-for-a-vm"></a><span data-ttu-id="212f6-103">VM에 대한 템플릿 다운로드</span><span class="sxs-lookup"><span data-stu-id="212f6-103">Download the template for a VM</span></span>
<span data-ttu-id="212f6-104">포털 또는 PowerShell을 사용하여 Azure에서 VM을 만들 때 Resource Manager 템플릿은 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="212f6-104">When you create a VM in Azure using the portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="212f6-105">배포를 빠르게 복제하는 데 이 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="212f6-105">You can use this template to quickly duplicate a deployment.</span></span> <span data-ttu-id="212f6-106">템플릿은 리소스 그룹에 있는 모든 리소스에 대한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="212f6-106">The template contains information about all of the resources in a resource group.</span></span> <span data-ttu-id="212f6-107">즉 가상 컴퓨터의 경우 네트워킹 리소스를 포함하여 해당 리소스 그룹에서 VM을 지원하기 위해 만든 모든 항목이 템플릿에 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="212f6-107">For a virtual machine, this means the template contains everything that is created in support of the VM in that resource group, including the networking resources.</span></span>

## <a name="download-the-template-using-the-portal"></a><span data-ttu-id="212f6-108">포털을 사용한 템플릿 다운로드</span><span class="sxs-lookup"><span data-stu-id="212f6-108">Download the template using the portal</span></span>
1. <span data-ttu-id="212f6-109">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="212f6-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="212f6-110">허브메뉴에서 **가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="212f6-110">One the hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="212f6-111">목록에서 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="212f6-111">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="212f6-112">**Automation 스크립트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="212f6-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="212f6-113">**다운로드**를 선택하고 .zip 파일을 로컬 컴퓨터에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="212f6-113">Select **Download** and save the .zip file to your local computer.</span></span>
6. <span data-ttu-id="212f6-114">.zip 파일을 열고 파일을 폴더에 풉니다.</span><span class="sxs-lookup"><span data-stu-id="212f6-114">Open the .zip file and extract the files to a folder.</span></span> <span data-ttu-id="212f6-115">.zip 파일은 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="212f6-115">The .zip file will contain:</span></span>
   
   * <span data-ttu-id="212f6-116">deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="212f6-116">deploy.ps1</span></span>
   * <span data-ttu-id="212f6-117">deploy.sh</span><span class="sxs-lookup"><span data-stu-id="212f6-117">deploy.sh</span></span> 
   * <span data-ttu-id="212f6-118">deployer.rb</span><span class="sxs-lookup"><span data-stu-id="212f6-118">deployer.rb</span></span>
   * <span data-ttu-id="212f6-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="212f6-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="212f6-120">parameters.json</span><span class="sxs-lookup"><span data-stu-id="212f6-120">parameters.json</span></span>
   * <span data-ttu-id="212f6-121">template.json</span><span class="sxs-lookup"><span data-stu-id="212f6-121">template.json</span></span>

<span data-ttu-id="212f6-122">template.json 파일은 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="212f6-122">The template.json file is the template.</span></span>

## <a name="download-the-template-using-powershell"></a><span data-ttu-id="212f6-123">PowerShell을 사용한 템플릿 다운로드</span><span class="sxs-lookup"><span data-stu-id="212f6-123">Download the template using PowerShell</span></span>
<span data-ttu-id="212f6-124">또한 [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet을 사용하여 .json 템플릿 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="212f6-124">You can also download the .json template file using the [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="212f6-125">`-path` 매개 변수를 사용하여 .json 파일의 파일 이름 및 경로를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="212f6-125">You can use the `-path` parameter to provide the filename and path for the .json file.</span></span> <span data-ttu-id="212f6-126">이 예제에서는 로컬 컴퓨터의 **C:\users\public\downloads** 폴더에 **myResourceGroup**이라는 리소스 그룹에 대한 템플릿을 다운로드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="212f6-126">This example shows how to download the template for the resource group named **myResourceGroup** to the **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="212f6-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="212f6-127">Next steps</span></span>
<span data-ttu-id="212f6-128">템플릿을 사용하여 리소스를 배포하는 방법에 대해 알아보려면 [Resource Manager 템플릿 연습](../../azure-resource-manager/resource-manager-template-walkthrough.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="212f6-128">To learn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>


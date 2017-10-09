---
title: "Azure VM에 대 한 aaaDownload hello 템플릿을 | Microsoft Docs"
description: "Hello 만들기 hello 리소스 관리자 배포 모델에서 배포를 자동화 된 VM toohelp 다운로드"
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
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a><span data-ttu-id="a9c6a-103">VM에 대 한 hello 템플릿을 다운로드합니다</span><span class="sxs-lookup"><span data-stu-id="a9c6a-103">Download hello template for a VM</span></span>
<span data-ttu-id="a9c6a-104">Azure에서 VM을 만들 때 hello 포털 또는 PowerShell을 리소스 관리자를 사용 하 여 서식 파일은 자동으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-104">When you create a VM in Azure using hello portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="a9c6a-105">이 템플릿 tooquickly 중복 배포를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-105">You can use this template tooquickly duplicate a deployment.</span></span> <span data-ttu-id="a9c6a-106">hello 서식 파일의 모든 리소스 그룹의 hello 리소스에 대 한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-106">hello template contains information about all of hello resources in a resource group.</span></span> <span data-ttu-id="a9c6a-107">가상 컴퓨터에 대 한 hello ´ ï ´ hello 네트워킹 리소스를 포함 하 여 해당 리소스 그룹에 VM hello 지원 하기 위해 만든 모든 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-107">For a virtual machine, this means hello template contains everything that is created in support of hello VM in that resource group, including hello networking resources.</span></span>

## <a name="download-hello-template-using-hello-portal"></a><span data-ttu-id="a9c6a-108">Hello 포털을 사용 하 여 hello 템플릿을 다운로드합니다</span><span class="sxs-lookup"><span data-stu-id="a9c6a-108">Download hello template using hello portal</span></span>
1. <span data-ttu-id="a9c6a-109">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a9c6a-110">하나의 hello 허브 메뉴에서 선택 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-110">One hello hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="a9c6a-111">Hello 목록에서 hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-111">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="a9c6a-112">**Automation 스크립트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="a9c6a-113">선택 **다운로드** hello.zip 파일 tooyour 로컬 컴퓨터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-113">Select **Download** and save hello .zip file tooyour local computer.</span></span>
6. <span data-ttu-id="a9c6a-114">Hello.zip 파일을 열고 hello 파일 tooa 폴더에 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-114">Open hello .zip file and extract hello files tooa folder.</span></span> <span data-ttu-id="a9c6a-115">hello.zip 파일에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-115">hello .zip file will contain:</span></span>
   
   * <span data-ttu-id="a9c6a-116">deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="a9c6a-116">deploy.ps1</span></span>
   * <span data-ttu-id="a9c6a-117">deploy.sh</span><span class="sxs-lookup"><span data-stu-id="a9c6a-117">deploy.sh</span></span> 
   * <span data-ttu-id="a9c6a-118">deployer.rb</span><span class="sxs-lookup"><span data-stu-id="a9c6a-118">deployer.rb</span></span>
   * <span data-ttu-id="a9c6a-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="a9c6a-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="a9c6a-120">parameters.json</span><span class="sxs-lookup"><span data-stu-id="a9c6a-120">parameters.json</span></span>
   * <span data-ttu-id="a9c6a-121">template.json</span><span class="sxs-lookup"><span data-stu-id="a9c6a-121">template.json</span></span>

<span data-ttu-id="a9c6a-122">hello template.json 파일은 hello 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-122">hello template.json file is hello template.</span></span>

## <a name="download-hello-template-using-powershell"></a><span data-ttu-id="a9c6a-123">PowerShell을 사용 하 여 hello 템플릿을 다운로드합니다</span><span class="sxs-lookup"><span data-stu-id="a9c6a-123">Download hello template using PowerShell</span></span>
<span data-ttu-id="a9c6a-124">Hello를 사용 하 여 hello.json 템플릿 파일을 다운로드할 수 있습니다 [내보내기 AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-124">You can also download hello .json template file using hello [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="a9c6a-125">Hello를 사용할 수 있습니다 `-path` 매개 변수 tooprovide hello 파일 이름 및 hello.json 파일에 대 한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-125">You can use hello `-path` parameter tooprovide hello filename and path for hello .json file.</span></span> <span data-ttu-id="a9c6a-126">Hello 리소스 그룹에 대 한 toodownload hello 서식 파일 이름이 지정 하는 방법을 보여 주는이 예제 **myResourceGroup** toohello **C:\users\public\downloads** 로컬 컴퓨터의 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-126">This example shows how toodownload hello template for hello resource group named **myResourceGroup** toohello **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="a9c6a-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a9c6a-127">Next steps</span></span>
<span data-ttu-id="a9c6a-128">서식 파일을 사용 하 여 리소스를 배포에 대 한 더 toolearn 참조 [리소스 관리자 템플릿 연습](../../azure-resource-manager/resource-manager-template-walkthrough.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-128">toolearn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>


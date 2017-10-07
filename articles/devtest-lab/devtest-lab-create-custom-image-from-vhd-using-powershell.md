---
title: "PowerShell을 사용 하 여 VHD 파일의 사용자 지정 이미지를 Azure DevTest Labs aaaCreate | Microsoft Docs"
description: "PowerShell을 사용하여 VHD 파일에서 Azure DevTest Labs에 사용자 지정 이미지 만들기 자동화"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 39b4005fa46cdf86cf0800ca376128134bcfb650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a><span data-ttu-id="d2309-103">PowerShell을 사용하여 VHD 파일에서 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="d2309-103">Create a custom image from a VHD file using PowerShell</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="d2309-104">단계별 지침</span><span class="sxs-lookup"><span data-stu-id="d2309-104">Step-by-step instructions</span></span>

<span data-ttu-id="d2309-105">hello 다음 단계를 안내 PowerShell을 사용 하 여 VHD 파일에서 사용자 지정 이미지 만들기:</span><span class="sxs-lookup"><span data-stu-id="d2309-105">hello following steps walk you through creating a custom image from a VHD file using PowerShell:</span></span>

1. <span data-ttu-id="d2309-106">PowerShell 프롬프트에서 로그인 tooyour Azure 계정이 다음 호출 toohello hello로 **로그인 AzureRmAccount** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d2309-106">At a PowerShell prompt, log in tooyour Azure account with hello following call toohello **Login-AzureRmAccount** cmdlet.</span></span>  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  <span data-ttu-id="d2309-107">Select hello hello를 호출 하 여 Azure 구독을 원하는 **선택 AzureRmSubscription** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d2309-107">Select hello desired Azure subscription by calling hello **Select-AzureRmSubscription** cmdlet.</span></span> <span data-ttu-id="d2309-108">Hello에 대 한 자리 표시자 뒤 hello 대체 **$subscriptionId** 유효한 Azure 구독 id 변수</span><span class="sxs-lookup"><span data-stu-id="d2309-108">Replace hello following placeholder for hello **$subscriptionId** variable with a valid Azure subscription ID.</span></span> 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  <span data-ttu-id="d2309-109">호출 hello 여 hello 랩 개체를 가져올 **Get AzureRmResource** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d2309-109">Get hello lab object by calling hello **Get-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="d2309-110">Hello에 대 한 자리 표시자 뒤 hello 대체 **$labRg** 및 **$labName** 적절 한 사용자 환경에 대 한 값을 hello 사용 하 여 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="d2309-110">Replace hello following placeholders for hello **$labRg** and **$labName** variables with hello appropriate values for your environment.</span></span> 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  <span data-ttu-id="d2309-111">Hello 랩 저장소 계정 및 랩 저장소 계정 키에서 값을 가져올 hello 랩 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d2309-111">Get hello lab storage account and lab storage account key values from hello lab object.</span></span> 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  <span data-ttu-id="d2309-112">Hello에 대 한 자리 표시자 뒤 hello 대체 **$vhdUri** hello URI로 변수 tooyour VHD 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2309-112">Replace hello following placeholder for hello **$vhdUri** variable with hello URI tooyour uploaded VHD file.</span></span> <span data-ttu-id="d2309-113">Hello Azure 포털에에서 표시 되는 hello 저장소 계정의 blob 블레이드에서 hello VHD 파일의 URI를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2309-113">You can get hello VHD file's URI from hello storage account's blob blade in hello Azure portal.</span></span>

    ```PowerShell
    $vhdUri = '<Specify hello VHD URI here>'
    ```

1.  <span data-ttu-id="d2309-114">Hello를 사용 하 여 hello 사용자 지정 이미지 만들기 **새로 AzureRmResourceGroupDeployment** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d2309-114">Create hello custom image using hello **New-AzureRmResourceGroupDeployment** cmdlet.</span></span> <span data-ttu-id="d2309-115">Hello에 대 한 자리 표시자 뒤 hello 대체 **$customImageName** 및 **$customImageDescription** 사용자 환경에 대 한 변수 toomeaningful 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2309-115">Replace hello following placeholders for hello **$customImageName** and **$customImageDescription** variables toomeaningful names for your environment.</span></span>

    ```PowerShell
    $customImageName = '<Specify hello custom image name>'
    $customImageDescription = '<Specify hello custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-toocreate-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="d2309-116">PowerShell 스크립트 toocreate VHD 파일에서 사용자 지정 이미지</span><span class="sxs-lookup"><span data-stu-id="d2309-116">PowerShell script toocreate a custom image from a VHD file</span></span>

<span data-ttu-id="d2309-117">PowerShell 스크립트 뒤 hello 사용된 toocreate VHD 파일에서 사용자 지정 이미지 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2309-117">hello following PowerShell script can be used toocreate a custom image from a VHD file.</span></span> <span data-ttu-id="d2309-118">Hello 요구 사항에 대 한 적절 한 값으로 (부터 꺾쇠 괄호까지) hello 자리 표시자를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2309-118">Replace hello placeholders (starting and ending with angle brackets) with hello appropriate values for your needs.</span></span> 

```PowerShell
# Log in tooyour Azure account.  
Login-AzureRmAccount

# Select hello desired Azure subscription. 
$subscriptionId = '<Specify your subscription ID here>'
Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Get hello lab object.
$labRg = '<Specify your lab resource group name here>'
$labName = '<Specify your lab name here>'
$lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)

# Get hello lab storage account and lab storage account key values.
$labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
$labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value

# Set hello URI of hello VHD file.  
$vhdUri = '<Specify hello VHD URI here>'

# Set hello custom image name and description values.
$customImageName = '<Specify hello custom image name>'
$customImageDescription = '<Specify hello custom image description>'

# Set up hello parameters object.
$parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

# Create hello custom image. 
New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
```

## <a name="related-blog-posts"></a><span data-ttu-id="d2309-119">관련 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="d2309-119">Related blog posts</span></span>

- [<span data-ttu-id="d2309-120">사용자 지정 이미지 또는 수식?</span><span class="sxs-lookup"><span data-stu-id="d2309-120">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="d2309-121">Azure DevTest Labs 간의 사용자 지정 이미지 복사</span><span class="sxs-lookup"><span data-stu-id="d2309-121">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="d2309-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2309-122">Next steps</span></span>

- [<span data-ttu-id="d2309-123">추가 VM tooyour 랩</span><span class="sxs-lookup"><span data-stu-id="d2309-123">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)

---
title: "PowerShell을 사용하여 VHD 파일에서 Azure DevTest Labs 사용자 지정 이미지 만들기 | Microsoft Docs"
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
ms.openlocfilehash: a4729f70aae80a13233fbe96a5d8a56c0c9d01d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a><span data-ttu-id="0c781-103">PowerShell을 사용하여 VHD 파일에서 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="0c781-103">Create a custom image from a VHD file using PowerShell</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="0c781-104">단계별 지침</span><span class="sxs-lookup"><span data-stu-id="0c781-104">Step-by-step instructions</span></span>

<span data-ttu-id="0c781-105">다음 단계는 PowerShell을 사용하여 VHD 파일에서 사용자 지정 이미지를 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="0c781-105">The following steps walk you through creating a custom image from a VHD file using PowerShell:</span></span>

1. <span data-ttu-id="0c781-106">PowerShell 프롬프트에서, **Login-AzureRmAccount** cmdlet에 대한 다음 호출로 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0c781-106">At a PowerShell prompt, log in to your Azure account with the following call to the **Login-AzureRmAccount** cmdlet.</span></span>  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  <span data-ttu-id="0c781-107">**Select-AzureRmSubscription** cmdlet을 호출하여 원하는 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0c781-107">Select the desired Azure subscription by calling the **Select-AzureRmSubscription** cmdlet.</span></span> <span data-ttu-id="0c781-108">**$subscriptionId** 변수에 대한 다음 자리 표시자를 유효한 Azure 구독 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0c781-108">Replace the following placeholder for the **$subscriptionId** variable with a valid Azure subscription ID.</span></span> 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  <span data-ttu-id="0c781-109">**Get-AzureRmResource** cmdlet을 호출하여 랩 객체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0c781-109">Get the lab object by calling the **Get-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="0c781-110">**$labRg** 및 **$labName** 변수에 대한 다음 자리 표시자를 환경에 적합한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0c781-110">Replace the following placeholders for the **$labRg** and **$labName** variables with the appropriate values for your environment.</span></span> 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  <span data-ttu-id="0c781-111">랩 객체에서 랩 저장소 계정 및 랩 저장소 계정 키 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0c781-111">Get the lab storage account and lab storage account key values from the lab object.</span></span> 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  <span data-ttu-id="0c781-112">**$vhdUri** 변수에 대한 다음 자리 표시자를 업로드한 VHD 파일에 대한 URI로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0c781-112">Replace the following placeholder for the **$vhdUri** variable with the URI to your uploaded VHD file.</span></span> <span data-ttu-id="0c781-113">Azure Portal의 저장소 계정의 Blob 블레이드에서 VHD 파일의 URl를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c781-113">You can get the VHD file's URI from the storage account's blob blade in the Azure portal.</span></span>

    ```PowerShell
    $vhdUri = '<Specify the VHD URI here>'
    ```

1.  <span data-ttu-id="0c781-114">**New-AzureRmResourceGroupDeployment** Cmdlet을 사용자 지정 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0c781-114">Create the custom image using the **New-AzureRmResourceGroupDeployment** cmdlet.</span></span> <span data-ttu-id="0c781-115">**$customImageName** 및 **$customImageDescription** 변수에 대한 다음 자리 표시자를 환경에 의미 있는 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0c781-115">Replace the following placeholders for the **$customImageName** and **$customImageDescription** variables to meaningful names for your environment.</span></span>

    ```PowerShell
    $customImageName = '<Specify the custom image name>'
    $customImageDescription = '<Specify the custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-to-create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="0c781-116">VHD 파일에서 사용자 지정 이미지를 만들 PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="0c781-116">PowerShell script to create a custom image from a VHD file</span></span>

<span data-ttu-id="0c781-117">다음 PowerShell 스크립트를 사용하여 VHD 파일에서 사용자 지정 이미지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c781-117">The following PowerShell script can be used to create a custom image from a VHD file.</span></span> <span data-ttu-id="0c781-118">자리 표시자(각괄호)를 필요한 적합한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0c781-118">Replace the placeholders (starting and ending with angle brackets) with the appropriate values for your needs.</span></span> 

```PowerShell
# Log in to your Azure account.  
Login-AzureRmAccount

# Select the desired Azure subscription. 
$subscriptionId = '<Specify your subscription ID here>'
Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Get the lab object.
$labRg = '<Specify your lab resource group name here>'
$labName = '<Specify your lab name here>'
$lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)

# Get the lab storage account and lab storage account key values.
$labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
$labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value

# Set the URI of the VHD file.  
$vhdUri = '<Specify the VHD URI here>'

# Set the custom image name and description values.
$customImageName = '<Specify the custom image name>'
$customImageDescription = '<Specify the custom image description>'

# Set up the parameters object.
$parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

# Create the custom image. 
New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
```

## <a name="related-blog-posts"></a><span data-ttu-id="0c781-119">관련 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="0c781-119">Related blog posts</span></span>

- [<span data-ttu-id="0c781-120">사용자 지정 이미지 또는 수식?</span><span class="sxs-lookup"><span data-stu-id="0c781-120">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="0c781-121">Azure DevTest Labs 간의 사용자 지정 이미지 복사</span><span class="sxs-lookup"><span data-stu-id="0c781-121">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="0c781-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0c781-122">Next steps</span></span>

- [<span data-ttu-id="0c781-123">랩에 VM 추가</span><span class="sxs-lookup"><span data-stu-id="0c781-123">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)

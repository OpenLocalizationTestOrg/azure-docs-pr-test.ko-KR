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
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a>PowerShell을 사용하여 VHD 파일에서 사용자 지정 이미지 만들기

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>단계별 지침

hello 다음 단계를 안내 PowerShell을 사용 하 여 VHD 파일에서 사용자 지정 이미지 만들기:

1. PowerShell 프롬프트에서 로그인 tooyour Azure 계정이 다음 호출 toohello hello로 **로그인 AzureRmAccount** cmdlet.  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  Select hello hello를 호출 하 여 Azure 구독을 원하는 **선택 AzureRmSubscription** cmdlet. Hello에 대 한 자리 표시자 뒤 hello 대체 **$subscriptionId** 유효한 Azure 구독 id 변수 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  호출 hello 여 hello 랩 개체를 가져올 **Get AzureRmResource** cmdlet. Hello에 대 한 자리 표시자 뒤 hello 대체 **$labRg** 및 **$labName** 적절 한 사용자 환경에 대 한 값을 hello 사용 하 여 변수입니다. 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  Hello 랩 저장소 계정 및 랩 저장소 계정 키에서 값을 가져올 hello 랩 개체입니다. 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  Hello에 대 한 자리 표시자 뒤 hello 대체 **$vhdUri** hello URI로 변수 tooyour VHD 파일을 업로드 합니다. Hello Azure 포털에에서 표시 되는 hello 저장소 계정의 blob 블레이드에서 hello VHD 파일의 URI를 가져올 수 있습니다.

    ```PowerShell
    $vhdUri = '<Specify hello VHD URI here>'
    ```

1.  Hello를 사용 하 여 hello 사용자 지정 이미지 만들기 **새로 AzureRmResourceGroupDeployment** cmdlet. Hello에 대 한 자리 표시자 뒤 hello 대체 **$customImageName** 및 **$customImageDescription** 사용자 환경에 대 한 변수 toomeaningful 이름입니다.

    ```PowerShell
    $customImageName = '<Specify hello custom image name>'
    $customImageDescription = '<Specify hello custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-toocreate-a-custom-image-from-a-vhd-file"></a>PowerShell 스크립트 toocreate VHD 파일에서 사용자 지정 이미지

PowerShell 스크립트 뒤 hello 사용된 toocreate VHD 파일에서 사용자 지정 이미지 될 수 있습니다. Hello 요구 사항에 대 한 적절 한 값으로 (부터 꺾쇠 괄호까지) hello 자리 표시자를 대체 합니다. 

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

## <a name="related-blog-posts"></a>관련 블로그 게시물

- [사용자 지정 이미지 또는 수식?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Azure DevTest Labs 간의 사용자 지정 이미지 복사](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>다음 단계

- [추가 VM tooyour 랩](./devtest-lab-add-vm-with-artifacts.md)

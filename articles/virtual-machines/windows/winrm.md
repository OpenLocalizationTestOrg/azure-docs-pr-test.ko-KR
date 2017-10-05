---
title: "Azure VM에 대한 WinRM 액세스 설정 | Microsoft Docs"
description: "Resource Manager 배포 모델에서 만든 Azure 가상 컴퓨터에 대한 WinRM 액세스를 설정합니다."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9718e85b-d360-4621-90b8-0b0b84a21208
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/16/2016
ms.author: kasing
ms.openlocfilehash: 2d6533462400bc1d93d0d3b0227769784e2658a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="bfe50-103">Azure Resource Manager에서 가상 컴퓨터에 대한 WinRM 액세스 설정</span><span class="sxs-lookup"><span data-stu-id="bfe50-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="bfe50-104">Azure 서비스 관리 및 Azure Resource Manager의 WinRM</span><span class="sxs-lookup"><span data-stu-id="bfe50-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="bfe50-105">Azure Resource Manager의 개요를 보려면 이 [문서](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bfe50-105">For an overview of the Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="bfe50-106">Azure 서비스 관리 및 Azure Resource Manager 간의 차이점에 대해서는 이 [문서](../../resource-manager-deployment-model.md)</span><span class="sxs-lookup"><span data-stu-id="bfe50-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="bfe50-107">두 스택 간에 WinRM 구성을 설정할 때의 주요 차이점은 VM에 인증서가 설치되는 방법에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-107">The key difference in setting up WinRM configuration between the two stacks is how the certificate gets installed on the VM.</span></span> <span data-ttu-id="bfe50-108">Azure Resource Manager 스택에서 인증서는 주요 자격 증명 모음 리소스 공급자가 관리하는 리소스로 모델링됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-108">In the Azure Resource Manager stack, the certificates are modeled as resources managed by the Key Vault Resource Provider.</span></span> <span data-ttu-id="bfe50-109">따라서 사용자는 VM에서 인증서를 사용하기 위해 먼저 본인의 인증서를 제공한 후 주요 자격 증명 모음에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-109">Therefore, the user needs to provide their own certificate and upload it to a Key Vault before using it in a VM.</span></span>

<span data-ttu-id="bfe50-110">다음은 WinRM 연결을 사용하여 VM을 설정하는 데 필요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-110">Here are the steps you need to take to set up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="bfe50-111">주요 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="bfe50-111">Create a Key Vault</span></span>
2. <span data-ttu-id="bfe50-112">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="bfe50-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="bfe50-113">자체 서명된 인증서를 주요 자격 증명 모음에 업로드</span><span class="sxs-lookup"><span data-stu-id="bfe50-113">Upload your self-signed certificate to Key Vault</span></span>
4. <span data-ttu-id="bfe50-114">주요 자격 증명 모음에 자체 서명된 인증서에 대한 URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="bfe50-114">Get the URL for your self-signed certificate in the Key Vault</span></span>
5. <span data-ttu-id="bfe50-115">VM을 만드는 동안 자체 서명된 인증서 URL 참조</span><span class="sxs-lookup"><span data-stu-id="bfe50-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="bfe50-116">1단계: 주요 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="bfe50-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="bfe50-117">아래 명령을 사용하여 주요 자격 증명 모음을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-117">You can use the below command to create the Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="bfe50-118">2단계: 자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="bfe50-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="bfe50-119">이 PowerShell 스크립트를 사용하여 자체 서명된 인증서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter the certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-to-the-key-vault"></a><span data-ttu-id="bfe50-120">3단계: 주요 자격 증명 모음에 자체 서명된 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="bfe50-120">Step 3: Upload your self-signed certificate to the Key Vault</span></span>
<span data-ttu-id="bfe50-121">1단계에서 만든 주요 자격 증명 모음에 인증서를 업로드하기 전에 먼저 Microsoft.Compute 리소스 공급자가 이해할 수 있는 형식으로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-121">Before uploading the certificate to the Key Vault created in step 1, it needs to converted into a format the Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="bfe50-122">아래 PowerShell 스크립트를 사용하면 그러한 형식으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-122">The below PowerShell script will allow you do that</span></span>

```
$fileName = "<Path to the .pfx file>"
$fileContentBytes = Get-Content $fileName -Encoding Byte
$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

$jsonObject = @"
{
  "data": "$filecontentencoded",
  "dataType" :"pfx",
  "password": "<password>"
}
"@

$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText –Force
Set-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>" -SecretValue $secret
```

## <a name="step-4-get-the-url-for-your-self-signed-certificate-in-the-key-vault"></a><span data-ttu-id="bfe50-123">4단계: 주요 자격 증명 모음에 자체 서명된 인증서에 대한 URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="bfe50-123">Step 4: Get the URL for your self-signed certificate in the Key Vault</span></span>
<span data-ttu-id="bfe50-124">Microsoft.Compute 리소스 공급자는 VM을 프로비전하는 동안 주요 자격 증명 모음 내에 포함된 암호에 대한 URL이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-124">The Microsoft.Compute resource provider needs a URL to the secret inside the Key Vault while provisioning the VM.</span></span> <span data-ttu-id="bfe50-125">이룰 통해 Microsoft.Compute 리소스 공급자는 암호를 다운로드하고 VM에서 해당 인증서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-125">This enables the Microsoft.Compute resource provider to download the secret and create the equivalent certificate on the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="bfe50-126">암호의 URL에는 버전도 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-126">The URL of the secret needs to include the version as well.</span></span> <span data-ttu-id="bfe50-127">예제 URL은 아래의 https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve 같은 형태</span><span class="sxs-lookup"><span data-stu-id="bfe50-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="bfe50-128">템플릿</span><span class="sxs-lookup"><span data-stu-id="bfe50-128">Templates</span></span>
<span data-ttu-id="bfe50-129">아래 코드를 사용하여 템플릿의 URL에 대한 링크를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-129">You can get the link to the URL in the template using the below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="bfe50-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfe50-130">PowerShell</span></span>
<span data-ttu-id="bfe50-131">아래의 PowerShell 명령을 사용하여 이 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-131">You can get this URL using the below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="bfe50-132">5단계: VM을 만드는 동안 자체 서명된 인증서 URL 참조</span><span class="sxs-lookup"><span data-stu-id="bfe50-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="bfe50-133">Azure 리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="bfe50-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="bfe50-134">템플릿을 통해 VM을 만드는 동안 인증서가 아래와 같이 암호 섹션 및 winRM 섹션에서 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-134">While creating a VM through templates, the certificate gets referenced in the secrets section and the winRM section as below:</span></span>

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of the Key Vault containing the secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for the certificate you got in Step 4>",
                  "certificateStore": "<Name of the certificate store on the VM>"
                }
              ]
            }
          ],
          "windowsConfiguration": {
            ...
            "winRM": {
              "listeners": [
                {
                  "protocol": "http"
                },
                {
                  "protocol": "https",
                  "certificateUrl": "<URL for the certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

<span data-ttu-id="bfe50-135">위 항목에 대한 샘플 템플릿은 [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="bfe50-135">A sample template for the above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="bfe50-136">이 템플릿의 소스 코드는 [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="bfe50-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="bfe50-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfe50-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-to-the-vm"></a><span data-ttu-id="bfe50-138">6단계: VM에 연결</span><span class="sxs-lookup"><span data-stu-id="bfe50-138">Step 6: Connecting to the VM</span></span>
<span data-ttu-id="bfe50-139">VM에 연결하려면 먼저 컴퓨터가 WinRM 원격 관리에 맞게 구성되어 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-139">Before you can connect to the VM you'll need to make sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="bfe50-140">관리자 권한으로 PowerShell을 시작하고 아래 명령을 실행하여 제대로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-140">Start PowerShell as an administrator and execute the below command to make sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="bfe50-141">위 작업이 제대로 수행되지 않으면 WinRM 서비스가 실행되고 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-141">You might need to make sure the WinRM service is running if the above does not work.</span></span> <span data-ttu-id="bfe50-142">이 작업은 `Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="bfe50-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="bfe50-143">설정이 끝나면 아래 명령을 사용하여 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfe50-143">Once the setup is done, you can connect to the VM using the below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate

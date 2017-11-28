---
title: "Azure VM에 대 한 WinRM 액세스를 aaaSet | Microsoft Docs"
description: "Hello 리소스 관리자 배포 모델에서 만든 Azure 가상 컴퓨터와 사용에 대 한 WinRM 액세스를 설정 합니다."
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
ms.openlocfilehash: 23d1d3a3065cbd8e4036be085c6d835cae36caae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="33a38-103">Azure Resource Manager에서 가상 컴퓨터에 대한 WinRM 액세스 설정</span><span class="sxs-lookup"><span data-stu-id="33a38-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="33a38-104">Azure 서비스 관리 및 Azure Resource Manager의 WinRM</span><span class="sxs-lookup"><span data-stu-id="33a38-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="33a38-105">Hello Azure 리소스 관리자의 개요를 참조 하십시오이 [문서](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="33a38-105">For an overview of hello Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="33a38-106">Azure 서비스 관리 및 Azure Resource Manager 간의 차이점에 대해서는 이 [문서](../../resource-manager-deployment-model.md)</span><span class="sxs-lookup"><span data-stu-id="33a38-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="33a38-107">hello hello 두 스택 간에 WinRM 구성 설정의 주요 차이점은 hello 인증서 hello VM에 설치 되는 방법을 합니다.</span><span class="sxs-lookup"><span data-stu-id="33a38-107">hello key difference in setting up WinRM configuration between hello two stacks is how hello certificate gets installed on hello VM.</span></span> <span data-ttu-id="33a38-108">Hello Azure 리소스 관리자 스택의 hello 인증서 hello 키 자격 증명 모음 리소스 공급자에서 관리 하는 리소스 그룹으로 모델링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33a38-108">In hello Azure Resource Manager stack, hello certificates are modeled as resources managed by hello Key Vault Resource Provider.</span></span> <span data-ttu-id="33a38-109">따라서 hello 사용자 tooprovide 자신의 인증서가 필요 하 고 VM에서 사용 하기 전에 tooa 주요 자격 증명 모음에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="33a38-109">Therefore, hello user needs tooprovide their own certificate and upload it tooa Key Vault before using it in a VM.</span></span>

<span data-ttu-id="33a38-110">다음은 WinRM 연결에 VM tootake tooset 필요한 hello 단계</span><span class="sxs-lookup"><span data-stu-id="33a38-110">Here are hello steps you need tootake tooset up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="33a38-111">주요 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="33a38-111">Create a Key Vault</span></span>
2. <span data-ttu-id="33a38-112">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="33a38-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="33a38-113">자체 서명 된 인증서 tooKey 자격 증명 모음에 업로드</span><span class="sxs-lookup"><span data-stu-id="33a38-113">Upload your self-signed certificate tooKey Vault</span></span>
4. <span data-ttu-id="33a38-114">Hello 키 자격 증명 모음에에서 자체 서명 된 인증서에 대 한 hello URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="33a38-114">Get hello URL for your self-signed certificate in hello Key Vault</span></span>
5. <span data-ttu-id="33a38-115">VM을 만드는 동안 자체 서명된 인증서 URL 참조</span><span class="sxs-lookup"><span data-stu-id="33a38-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="33a38-116">1단계: 주요 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="33a38-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="33a38-117">명령 toocreate hello 주요 자격 증명 모음 아래 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33a38-117">You can use hello below command toocreate hello Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="33a38-118">2단계: 자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="33a38-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="33a38-119">이 PowerShell 스크립트를 사용하여 자체 서명된 인증서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33a38-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a><span data-ttu-id="33a38-120">3 단계: 키 자격 증명 모음에 자체 서명 된 인증서 toohello 업로드</span><span class="sxs-lookup"><span data-stu-id="33a38-120">Step 3: Upload your self-signed certificate toohello Key Vault</span></span>
<span data-ttu-id="33a38-121">1 단계에서 만든 hello 인증서 toohello 주요 자격 증명 모음 업로드, 전에 tooconverted 형식 hello Microsoft.Compute 리소스 공급자는 이해 하는에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="33a38-121">Before uploading hello certificate toohello Key Vault created in step 1, it needs tooconverted into a format hello Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="33a38-122">이렇게 하면 아래 PowerShell 스크립트는 hello 사용 하면</span><span class="sxs-lookup"><span data-stu-id="33a38-122">hello below PowerShell script will allow you do that</span></span>

```
$fileName = "<Path toohello .pfx file>"
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

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a><span data-ttu-id="33a38-123">4 단계: 키 자격 증명 모음 hello에 자체 서명 된 인증서에 대 한 hello URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="33a38-123">Step 4: Get hello URL for your self-signed certificate in hello Key Vault</span></span>
<span data-ttu-id="33a38-124">hello Microsoft.Compute 리소스 공급자는 hello 키 자격 증명 모음 내 URL toohello 비밀 hello VM을 프로 비전 할 때 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="33a38-124">hello Microsoft.Compute resource provider needs a URL toohello secret inside hello Key Vault while provisioning hello VM.</span></span> <span data-ttu-id="33a38-125">이 hello Microsoft.Compute 리소스 공급자 toodownload hello 암호를 사용 하도록 설정 하 고 hello VM에 hello 해당 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33a38-125">This enables hello Microsoft.Compute resource provider toodownload hello secret and create hello equivalent certificate on hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="33a38-126">hello 암호의 hello URL tooinclude hello 버전도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="33a38-126">hello URL of hello secret needs tooinclude hello version as well.</span></span> <span data-ttu-id="33a38-127">예제 URL은 아래의 https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve 같은 형태</span><span class="sxs-lookup"><span data-stu-id="33a38-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="33a38-128">템플릿</span><span class="sxs-lookup"><span data-stu-id="33a38-128">Templates</span></span>
<span data-ttu-id="33a38-129">아래 코드는 hello를 사용 하 여 hello 템플릿을에서 hello 링크 toohello URL을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33a38-129">You can get hello link toohello URL in hello template using hello below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="33a38-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="33a38-130">PowerShell</span></span>
<span data-ttu-id="33a38-131">아래의 PowerShell 명령 hello를 사용 하 여이 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33a38-131">You can get this URL using hello below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="33a38-132">5단계: VM을 만드는 동안 자체 서명된 인증서 URL 참조</span><span class="sxs-lookup"><span data-stu-id="33a38-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="33a38-133">Azure 리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="33a38-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="33a38-134">템플릿을 통해 VM을 만드는 동안 hello 비밀 섹션과 hello winRM 섹션 아래와 같이 hello 인증서 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="33a38-134">While creating a VM through templates, hello certificate gets referenced in hello secrets section and hello winRM section as below:</span></span>

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of hello Key Vault containing hello secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for hello certificate you got in Step 4>",
                  "certificateStore": "<Name of hello certificate store on hello VM>"
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
                  "certificateUrl": "<URL for hello certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

<span data-ttu-id="33a38-135">위의 hello에 대 한 샘플 템플릿을 확인할 수 있습니다에 [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="33a38-135">A sample template for hello above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="33a38-136">이 템플릿의 소스 코드는 [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="33a38-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="33a38-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="33a38-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a><span data-ttu-id="33a38-138">6 단계: toohello VM 연결</span><span class="sxs-lookup"><span data-stu-id="33a38-138">Step 6: Connecting toohello VM</span></span>
<span data-ttu-id="33a38-139">Toohello VM을 연결 하려면 먼저 toomake WinRM 원격 관리에 대 한 시스템 구성 되어 있는지 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="33a38-139">Before you can connect toohello VM you'll need toomake sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="33a38-140">관리자 권한으로 PowerShell을 시작 하 고 설정 되어 있는지 명령 toomake 아래 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="33a38-140">Start PowerShell as an administrator and execute hello below command toomake sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="33a38-141">Toomake hello 위의 작동 하지 않을 경우 hello WinRM 서비스가 실행 되 고 있는지를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33a38-141">You might need toomake sure hello WinRM service is running if hello above does not work.</span></span> <span data-ttu-id="33a38-142">이 작업은 `Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="33a38-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="33a38-143">Hello 설치가 완료 되 면 VM toohello 연결할 수 있습니다 명령 아래의 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="33a38-143">Once hello setup is done, you can connect toohello VM using hello below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate

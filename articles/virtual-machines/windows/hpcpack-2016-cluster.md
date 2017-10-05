---
title: "Azure에서 HPC 팩 2016 클러스터 | Microsoft Docs"
description: "Azure에서 HPC 팩 2016 클러스터를 배포하는 방법에 대해 알아봅니다"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 88d1f4e29f38ba1a6bef57c2da43bee205575eee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="405c0-103">Azure에서 HPC 팩 2016 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="405c0-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="405c0-104">이 문서의 단계에 따라 Azure 가상 컴퓨터에서 [Microsoft HPC 팩 2016](https://technet.microsoft.com/library/cc514029) 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-104">Follow the steps in this article to deploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="405c0-105">HPC Pack은 Microsoft Azure 및 Windows Server 기술로 구축된 Microsoft의 무료 HPC 솔루션으로, 광범위한 HPC 워크로드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="405c0-106">[Azure Resource Manager 템플릿](https://github.com/MsHpcPack/HPCPack2016) 중 하나를 사용하여 HPC 팩 2016 클러스터를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-106">Use one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span></span> <span data-ttu-id="405c0-107">클러스터 헤드 노드의 숫자가 다른 클러스터 토폴로지를 선택하고 Linux 또는 Windows 계산 노드를 사용할지 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="405c0-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="405c0-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="405c0-109">PFX 인증서</span><span class="sxs-lookup"><span data-stu-id="405c0-109">PFX certificate</span></span>

<span data-ttu-id="405c0-110">Microsoft HPC 팩 2016 클러스터에는 HPC 노드 간 통신을 보호하기 위해 PFX(개인 정보 교환) 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate to secure the communication between the HPC nodes.</span></span> <span data-ttu-id="405c0-111">인증서는 다음 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-111">The certificate must meet the following requirements:</span></span>

* <span data-ttu-id="405c0-112">키 교환이 가능한 개인 키가 있어야 함</span><span class="sxs-lookup"><span data-stu-id="405c0-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="405c0-113">디지털 서명 및 키 암호화를 포함하는 키 사용</span><span class="sxs-lookup"><span data-stu-id="405c0-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="405c0-114">클라이언트 인증 및 서버 인증을 포함하는 강화된 키 사용</span><span class="sxs-lookup"><span data-stu-id="405c0-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="405c0-115">이러한 요구 사항을 충족하는 인정서가 아직 없는 경우 인증 기관에서 인증서를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-115">If you don’t already have a certificate that meets these requirements, you can request the certificate from a certification authority.</span></span> <span data-ttu-id="405c0-116">또는 다음 명령을 사용하여 명령을 실행하는 운영 체제에 따라 자체 서명된 인증서를 생성하고 개인 키가 있는 PFX 형식 인증서를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-116">Alternatively, you can use the following commands to generate the self-signed certificate based on the operating system on which you run the command, and export the PFX format certificate with private key.</span></span>

* <span data-ttu-id="405c0-117">**Windows 10 또는 Windows Server 2016의 경우**, 다음과 같이 기본 제공 **New-SelfSignedCertificate** PowerShell cmdlet를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-117">**For Windows 10 or Windows Server 2016**, run the built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="405c0-118">**Windows 10 또는 Windows Server 2016 이전의 운영 체제의 경우** Microsoft Script Center에서 [자체 서명 인증서 생성기](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download the [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from the Microsoft Script Center.</span></span> <span data-ttu-id="405c0-119">그 내용을 추출하고 PowerShell 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-119">Extract its contents and run the following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-to-an-azure-key-vault"></a><span data-ttu-id="405c0-120">Azure Key Vault에 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="405c0-120">Upload certificate to an Azure key vault</span></span>

<span data-ttu-id="405c0-121">HPC 클러스터를 배포하기 전에 인증서를 [Azure Key Vault](../../key-vault/index.md)에 암호로 업로드하고 배포하는 동안 사용할 **자격 증명 모음 이름**, **자격 증명 모음 리소스 그룹**, **인증서 URL** 및 **인증서 지문** 정보를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-121">Before deploying the HPC cluster, upload the certificate to an [Azure key vault](../../key-vault/index.md) as a secret, and record the following information for use during the deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="405c0-122">인증서를 업로드하는 샘플 PowerShell 스크립트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-122">A sample PowerShell script to upload the certificate follows.</span></span> <span data-ttu-id="405c0-123">Azure Key Vault에 인증서를 업로드하는 방법에 대한 자세한 내용은 [Azure Key Vault 시작](../../key-vault/key-vault-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="405c0-123">For more information about uploading a certificate to an Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give the following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate the pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode the JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload the certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"The following Information will be used in the deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="405c0-124">지원되는 토폴로지</span><span class="sxs-lookup"><span data-stu-id="405c0-124">Supported topologies</span></span>

<span data-ttu-id="405c0-125">[Azure Resource Manager 템플릿](https://github.com/MsHpcPack/HPCPack2016) 중 하나를 선택하여 HPC 팩 2016 클러스터를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-125">Choose one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span></span> <span data-ttu-id="405c0-126">다음은 지원되는 세 가지 클러스터 토폴로지의 상위 수준 아키텍처입니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="405c0-127">고가용성 토폴로지는 여러 클러스터 헤드 노드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="405c0-128">Active Directory 도메인을 사용하는 고가용성 클러스터</span><span class="sxs-lookup"><span data-stu-id="405c0-128">High-availability cluster with Active Directory domain</span></span>

    ![AD 도메인의 HA 클러스터](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="405c0-130">Active Directory 도메인을 사용하지 않는 고가용성 클러스터</span><span class="sxs-lookup"><span data-stu-id="405c0-130">High-availability cluster without Active Directory domain</span></span>

    ![AD 도메인이 없는 HA 클러스터](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="405c0-132">단일 헤드 노드를 포함한 클러스터</span><span class="sxs-lookup"><span data-stu-id="405c0-132">Cluster with a single head node</span></span>

   ![단일 헤드 노드를 포함한 클러스터](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="405c0-134">클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="405c0-134">Deploy a cluster</span></span>

<span data-ttu-id="405c0-135">클러스터를 만들려면 템플릿을 선택하고 **Azure에 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-135">To create the cluster, choose a template and click **Deploy to Azure**.</span></span> <span data-ttu-id="405c0-136">[Azure Portal](https://portal.azure.com)에서 다음 단계에 설명된 대로 템플릿에 대한 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-136">In the [Azure portal](https://portal.azure.com), specify parameters for the template as described in the following steps.</span></span> <span data-ttu-id="405c0-137">각 템플릿은 HPC 클러스터 인프라에 필요한 모든 Azure 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-137">Each template creates all Azure resources required for the HPC cluster infrastructure.</span></span> <span data-ttu-id="405c0-138">리소스는 Azure 가상 네트워크, 공용 IP 주소, 부하 분산 장치(고가용성 클러스터만 해당), 네트워크 인터페이스, 가용성 집합, 저장소 계정 및 가상 컴퓨터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-the-subscription-location-and-resource-group"></a><span data-ttu-id="405c0-139">1단계: 구독, 위치 및 리소스 그룹 선택</span><span class="sxs-lookup"><span data-stu-id="405c0-139">Step 1: Select the subscription, location, and resource group</span></span>

<span data-ttu-id="405c0-140">**구독** 및 **위치**는 PFX 인증서를 업로드하는 경우 지정한 것과 동일해야 합니다(필수 구성 요소 참조).</span><span class="sxs-lookup"><span data-stu-id="405c0-140">The **Subscription** and the **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="405c0-141">이 배포에 대해 **리소스 그룹**을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-141">We recommend that you create a **Resource group** for the deployment.</span></span>

### <a name="step-2-specify-the-parameter-settings"></a><span data-ttu-id="405c0-142">2단계: 매개 변수 설정 지정</span><span class="sxs-lookup"><span data-stu-id="405c0-142">Step 2: Specify the parameter settings</span></span>

<span data-ttu-id="405c0-143">템플릿 매개 변수의 값을 입력하거나 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-143">Enter or modify values for the template parameters.</span></span> <span data-ttu-id="405c0-144">도움말 정보를 보려면 각 매개 변수 옆에 있는 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-144">Click the icon next to each parameter for help information.</span></span> <span data-ttu-id="405c0-145">또한 [사용 가능한 VM 크기](sizes.md)에 대한 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="405c0-145">Also see the guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="405c0-146">**자격 증명 모음 이름**, **자격 증명 모음 리소스 그룹**, **인증서 URL** 및 **인증서 지문** 매개 변수의 필수 구성 요소에 기록한 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-146">Specify the values you recorded in the Prerequisites for the following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="405c0-147">3단계.</span><span class="sxs-lookup"><span data-stu-id="405c0-147">Step 3.</span></span> <span data-ttu-id="405c0-148">약관 검토 및 만들기</span><span class="sxs-lookup"><span data-stu-id="405c0-148">Review legal terms and create</span></span>
<span data-ttu-id="405c0-149">**약관 검토**를 클릭하고 약관을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-149">Click **Review legal terms** to review the terms.</span></span> <span data-ttu-id="405c0-150">동의하면 **구매**를 클릭한 다음 **만들기**를 클릭하여 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-150">If you agree, click **Purchase**, and then click **Create** to start the deployment.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="405c0-151">클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="405c0-151">Connect to the cluster</span></span>
1. <span data-ttu-id="405c0-152">HPC 팩 클러스터를 배포한 후 [Azure Portal](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-152">After the HPC Pack cluster is deployed, go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="405c0-153">**리소스 그룹**을 클릭하고 클러스터가 배포된 리소스 그룹을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-153">Click **Resource groups**, and find the resource group in which the cluster was deployed.</span></span> <span data-ttu-id="405c0-154">헤드 노드 가상 컴퓨터를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-154">You can find the head node virtual machines.</span></span>

    ![포털의 클러스터 헤드 노드](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="405c0-156">하나의 헤드 노드를 클릭합니다. 고가용성 클러스터에서 헤드 노드 중 하나를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-156">Click one head node (in a high-availability cluster, click any of the head nodes).</span></span> <span data-ttu-id="405c0-157">**Essentials**에서 클러스터의 공용 IP 주소 또는 전체 DNS 이름을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-157">In **Essentials**, you can find the public IP address or full DNS name of the cluster.</span></span>

    ![클러스터 연결 설정](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="405c0-159">**연결**을 클릭하여 지정된 관리자 사용자 이름으로 원격 데스크톱을 사용하여 헤드 노드 중 하나에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-159">Click **Connect** to log on to any of the head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="405c0-160">배포한 클러스터가 Active Directory 도메인에 있으면 사용자 이름은 <privateDomainName>\<adminUsername >(예: hpc.local\hpcadmin)와 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-160">If the cluster you deployed is in an Active Directory Domain, the user name is of the form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="405c0-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="405c0-161">Next steps</span></span>
* <span data-ttu-id="405c0-162">클러스터에 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="405c0-162">Submit jobs to your cluster.</span></span> <span data-ttu-id="405c0-163">[Azure에서 HPC 팩 클러스터에 작업 제출](hpcpack-cluster-submit-jobs.md) 및 [Azure에서 Azure Active Directory를 사용하여 HPC 팩 2016 클러스터 관리](hpcpack-cluster-active-directory.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="405c0-163">See [Submit jobs to HPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>


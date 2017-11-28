---
title: "Azure에서 클러스터를 aaaHPC 팩 2016 | Microsoft Docs"
description: "Azure에서 HPC 팩 2016 toodeploy 클러스터링 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="26dbb-103">Azure에서 HPC 팩 2016 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="26dbb-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="26dbb-104">이 문서 toodeploy에 hello 단계를 따라는 [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) Azure 가상 컴퓨터의 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-104">Follow hello steps in this article toodeploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="26dbb-105">HPC Pack은 Microsoft Azure 및 Windows Server 기술로 구축된 Microsoft의 무료 HPC 솔루션으로, 광범위한 HPC 워크로드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="26dbb-106">Hello 중 하나를 사용 하 여 [Azure 리소스 관리자 템플릿을](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC 팩 2016 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-106">Use one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="26dbb-107">클러스터 헤드 노드의 숫자가 다른 클러스터 토폴로지를 선택하고 Linux 또는 Windows 계산 노드를 사용할지 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26dbb-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="26dbb-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="26dbb-109">PFX 인증서</span><span class="sxs-lookup"><span data-stu-id="26dbb-109">PFX certificate</span></span>

<span data-ttu-id="26dbb-110">Microsoft HPC Pack 2016 클러스터 hello HPC 노드 간의 정보 교환 PFX (개인) 인증서 toosecure hello 통신이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate toosecure hello communication between hello HPC nodes.</span></span> <span data-ttu-id="26dbb-111">hello 인증서 요구 사항을 준수 하는 hello를 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-111">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="26dbb-112">키 교환이 가능한 개인 키가 있어야 함</span><span class="sxs-lookup"><span data-stu-id="26dbb-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="26dbb-113">디지털 서명 및 키 암호화를 포함하는 키 사용</span><span class="sxs-lookup"><span data-stu-id="26dbb-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="26dbb-114">클라이언트 인증 및 서버 인증을 포함하는 강화된 키 사용</span><span class="sxs-lookup"><span data-stu-id="26dbb-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="26dbb-115">이러한 요구 사항을 충족 하는 인증서를 아직 없는 경우에 인증 기관에서 hello 인증서를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-115">If you don’t already have a certificate that meets these requirements, you can request hello certificate from a certification authority.</span></span> <span data-ttu-id="26dbb-116">또는 hello 명령을 toogenerate hello 자체 서명 된 인증서를 hello 명령을 실행 하 고이 hello PFX 형식 인증서 개인 키를 포함 하 여 내보낼 hello 운영 체제에 따라 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-116">Alternatively, you can use hello following commands toogenerate hello self-signed certificate based on hello operating system on which you run hello command, and export hello PFX format certificate with private key.</span></span>

* <span data-ttu-id="26dbb-117">**Windows 10 또는 Windows Server 2016에 대 한**, 기본 제공 hello 실행 **New-selfsignedcertificate** 다음과 같이 PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="26dbb-117">**For Windows 10 or Windows Server 2016**, run hello built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="26dbb-118">**운영 체제의 Windows 10 또는 Windows Server 2016 이전**, hello 다운로드 [자체 서명 된 인증서 생성기](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) hello Microsoft 스크립트 센터에서에서.</span><span class="sxs-lookup"><span data-stu-id="26dbb-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download hello [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from hello Microsoft Script Center.</span></span> <span data-ttu-id="26dbb-119">콘텐츠를 추출 하 고 다음 PowerShell 프롬프트에서 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-119">Extract its contents and run hello following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a><span data-ttu-id="26dbb-120">인증서 tooan Azure 키 자격 증명 모음 업로드</span><span class="sxs-lookup"><span data-stu-id="26dbb-120">Upload certificate tooan Azure key vault</span></span>

<span data-ttu-id="26dbb-121">Hello HPC 클러스터를 배포 하기 전에 hello 인증서 tooan 업로드 [Azure 키 자격 증명 모음](../../key-vault/index.md) 비밀을 및 레코드 hello hello 배포 중에 사용 하기 위해 정보를 다음으로: **자격 증명 모음 이름**, ** 자격 증명 모음 리소스 그룹**, **인증서 URL**, 및 **인증서 지문을**합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-121">Before deploying hello HPC cluster, upload hello certificate tooan [Azure key vault](../../key-vault/index.md) as a secret, and record hello following information for use during hello deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="26dbb-122">샘플 PowerShell 스크립트 tooupload hello 인증서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-122">A sample PowerShell script tooupload hello certificate follows.</span></span> <span data-ttu-id="26dbb-123">인증서 tooan Azure 키 자격 증명 모음에 업로드 하는 방법에 대 한 자세한 내용은 참조 [Azure 키 자격 증명 모음 시작](../../key-vault/key-vault-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-123">For more information about uploading a certificate tooan Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
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
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="26dbb-124">지원되는 토폴로지</span><span class="sxs-lookup"><span data-stu-id="26dbb-124">Supported topologies</span></span>

<span data-ttu-id="26dbb-125">Hello 중 하나를 선택 [Azure 리소스 관리자 템플릿을](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC 팩 2016 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-125">Choose one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="26dbb-126">다음은 지원되는 세 가지 클러스터 토폴로지의 상위 수준 아키텍처입니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="26dbb-127">고가용성 토폴로지는 여러 클러스터 헤드 노드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="26dbb-128">Active Directory 도메인을 사용하는 고가용성 클러스터</span><span class="sxs-lookup"><span data-stu-id="26dbb-128">High-availability cluster with Active Directory domain</span></span>

    ![AD 도메인의 HA 클러스터](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="26dbb-130">Active Directory 도메인을 사용하지 않는 고가용성 클러스터</span><span class="sxs-lookup"><span data-stu-id="26dbb-130">High-availability cluster without Active Directory domain</span></span>

    ![AD 도메인이 없는 HA 클러스터](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="26dbb-132">단일 헤드 노드를 포함한 클러스터</span><span class="sxs-lookup"><span data-stu-id="26dbb-132">Cluster with a single head node</span></span>

   ![단일 헤드 노드를 포함한 클러스터](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="26dbb-134">클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="26dbb-134">Deploy a cluster</span></span>

<span data-ttu-id="26dbb-135">toocreate hello 클러스터 서식 파일을 선택 하 고 클릭 **tooAzure 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-135">toocreate hello cluster, choose a template and click **Deploy tooAzure**.</span></span> <span data-ttu-id="26dbb-136">Hello에 [Azure 포털](https://portal.azure.com), 단계를 수행 하는 hello에 설명 된 대로 hello 서식 파일에 대 한 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-136">In hello [Azure portal](https://portal.azure.com), specify parameters for hello template as described in hello following steps.</span></span> <span data-ttu-id="26dbb-137">각 템플릿은 hello HPC 클러스터 인프라에 필요한 모든 Azure 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-137">Each template creates all Azure resources required for hello HPC cluster infrastructure.</span></span> <span data-ttu-id="26dbb-138">리소스는 Azure 가상 네트워크, 공용 IP 주소, 부하 분산 장치(고가용성 클러스터만 해당), 네트워크 인터페이스, 가용성 집합, 저장소 계정 및 가상 컴퓨터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a><span data-ttu-id="26dbb-139">1 단계: hello 구독, 위치 및 리소스 그룹 선택</span><span class="sxs-lookup"><span data-stu-id="26dbb-139">Step 1: Select hello subscription, location, and resource group</span></span>

<span data-ttu-id="26dbb-140">hello **구독** 및 hello **위치** PFX 인증서를 업로드 하는 경우 지정 된 동일 해야 합니다 (필수 구성 요소 참조).</span><span class="sxs-lookup"><span data-stu-id="26dbb-140">hello **Subscription** and hello **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="26dbb-141">만들어야 하는 것이 좋습니다는 **리소스 그룹** hello 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-141">We recommend that you create a **Resource group** for hello deployment.</span></span>

### <a name="step-2-specify-hello-parameter-settings"></a><span data-ttu-id="26dbb-142">2 단계: hello 매개 변수 설정 지정</span><span class="sxs-lookup"><span data-stu-id="26dbb-142">Step 2: Specify hello parameter settings</span></span>

<span data-ttu-id="26dbb-143">입력 하거나 hello 템플릿 매개 변수 값을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-143">Enter or modify values for hello template parameters.</span></span> <span data-ttu-id="26dbb-144">Hello 아이콘 다음 tooeach 매개 변수 도움말 정보에 대 한를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-144">Click hello icon next tooeach parameter for help information.</span></span> <span data-ttu-id="26dbb-145">또한 hello 지침을 참조 [사용 가능한 VM 크기](sizes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-145">Also see hello guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="26dbb-146">Hello 매개 변수 뒤에 대 한 hello 필수 구성 요소에 기록 하는 hello 값을 지정: **자격 증명 모음 이름**, **자격 증명 모음 리소스 그룹**, **인증서 URL**, 및 **인증서 지문을**합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-146">Specify hello values you recorded in hello Prerequisites for hello following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="26dbb-147">3단계.</span><span class="sxs-lookup"><span data-stu-id="26dbb-147">Step 3.</span></span> <span data-ttu-id="26dbb-148">약관 검토 및 만들기</span><span class="sxs-lookup"><span data-stu-id="26dbb-148">Review legal terms and create</span></span>
<span data-ttu-id="26dbb-149">클릭 **약관을 검토** tooreview hello 용어입니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-149">Click **Review legal terms** tooreview hello terms.</span></span> <span data-ttu-id="26dbb-150">동의 하면 클릭 **구매**, 클릭 하 고 **만들기** toostart hello 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-150">If you agree, click **Purchase**, and then click **Create** toostart hello deployment.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="26dbb-151">Toohello 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="26dbb-151">Connect toohello cluster</span></span>
1. <span data-ttu-id="26dbb-152">Hello HPC Pack 클러스터를 배포한 후 이동 toohello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-152">After hello HPC Pack cluster is deployed, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="26dbb-153">클릭 **리소스 그룹**, 및 찾기 hello 리소스 그룹은 hello 클러스터 배포 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-153">Click **Resource groups**, and find hello resource group in which hello cluster was deployed.</span></span> <span data-ttu-id="26dbb-154">Hello 헤드 노드 가상 컴퓨터를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-154">You can find hello head node virtual machines.</span></span>

    ![Hello 포털에서 클러스터 헤드 노드](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="26dbb-156">헤드 노드를 하나 클릭 (고가용성 클러스터)를 클릭 hello 헤드 노드 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-156">Click one head node (in a high-availability cluster, click any of hello head nodes).</span></span> <span data-ttu-id="26dbb-157">**Essentials**, hello 공용 IP 주소 또는 hello 클러스터의 전체 DNS 이름을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-157">In **Essentials**, you can find hello public IP address or full DNS name of hello cluster.</span></span>

    ![클러스터 연결 설정](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="26dbb-159">클릭 **연결** 에 원격 데스크톱을 사용 하 여 지정 된 관리자 사용자 이름으로는 hello 헤드 노드의 tooany toolog 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-159">Click **Connect** toolog on tooany of hello head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="26dbb-160">Active Directory 도메인에 배포 된 hello 클러스터 있으면 hello 사용자 이름이 hello 폼의 <privateDomainName> \<adminUsername > (예를 들어 hpc.local\hpcadmin).</span><span class="sxs-lookup"><span data-stu-id="26dbb-160">If hello cluster you deployed is in an Active Directory Domain, hello user name is of hello form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="26dbb-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="26dbb-161">Next steps</span></span>
* <span data-ttu-id="26dbb-162">Tooyour 클러스터 작업을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-162">Submit jobs tooyour cluster.</span></span> <span data-ttu-id="26dbb-163">참조 [작업 tooHPC Azure의 HPC Pack 클러스터 제출](hpcpack-cluster-submit-jobs.md) 및 [Azure Active Directory를 사용 하 여 Azure의 HPC 팩 2016 클러스터는 관리](hpcpack-cluster-active-directory.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26dbb-163">See [Submit jobs tooHPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>


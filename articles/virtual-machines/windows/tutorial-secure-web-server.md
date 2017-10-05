---
title: "Azure에서 SSL 인증서로 IIS 보호 | Microsoft Docs"
description: "Azure의 Windows VM에서 SSL 인증서로 IIS 웹 서버를 보호하는 방법을 알아봅니다."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/14/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 6567853e9ef3cad63595dc0afe7a793bdc5d972c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="decce-103">Azure의 Windows 가상 컴퓨터에서 SSL 인증서로 IIS 웹 서버 보호</span><span class="sxs-lookup"><span data-stu-id="decce-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="decce-104">웹 서버를 보호하기 위해 웹 트래픽을 암호화하는 데 SSL(Secure Sockets Later) 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="decce-104">To secure web servers, a Secure Sockets Later (SSL) certificate can be used to encrypt web traffic.</span></span> <span data-ttu-id="decce-105">이러한 SSL 인증서는 Azure Key Vault에 저장될 수 있으며 Azure에서 Windows VM(가상 컴퓨터)에 인증서의 보안 배포를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="decce-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates to Windows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="decce-106">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="decce-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="decce-107">Azure Key Vault 만들기</span><span class="sxs-lookup"><span data-stu-id="decce-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="decce-108">Key Vault에 인증서 생성 또는 업로드</span><span class="sxs-lookup"><span data-stu-id="decce-108">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="decce-109">VM 만들기 및 IIS 웹 서버 설치</span><span class="sxs-lookup"><span data-stu-id="decce-109">Create a VM and install the IIS web server</span></span>
> * <span data-ttu-id="decce-110">VM에 인증서 삽입 및 SSL 바인딩으로 IIS 구성</span><span class="sxs-lookup"><span data-stu-id="decce-110">Inject the certificate into the VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="decce-111">이 자습서에는 Azure PowerShell 모듈 버전 3.6 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="decce-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="decce-112">` Get-Module -ListAvailable AzureRM`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="decce-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="decce-113">업그레이드해야 하는 경우 [Azure PowerShell 모듈 설치](/powershell/azure/install-azurerm-ps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="decce-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="decce-114">개요</span><span class="sxs-lookup"><span data-stu-id="decce-114">Overview</span></span>
<span data-ttu-id="decce-115">Azure Key Vault는 암호화 키 및 비밀 정보(인증서 또는 암호)를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="decce-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="decce-116">Key Vault를 사용하면 인증서 관리 프로세스를 간소화하고 해당 인증서에 액세스하는 키의 제어를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="decce-116">Key Vault helps streamline the certificate management process and enables you to maintain control of keys that access those certificates.</span></span> <span data-ttu-id="decce-117">Key Vault 내에 자체 서명된 인증서를 만들거나 이미 소유하고 있는 기존의 신뢰할 수 있는 인증서를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="decce-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="decce-118">내재된 인증서를 포함하는 사용자 지정 VM 이미지를 사용하는 대신 실행 중인 VM에 인증서를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="decce-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="decce-119">이 프로세스를 통해 배포하는 동안 가장 최신 인증서가 웹 서버에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="decce-119">This process ensures that the most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="decce-120">인증서를 갱신하거나 바꾸는 경우 새 사용자 지정 VM 이미지를 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="decce-120">If you renew or replace a certificate, you don't also have to create a new custom VM image.</span></span> <span data-ttu-id="decce-121">최신 인증서는 추가 VM을 만들 때 자동으로 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="decce-121">The latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="decce-122">전체 프로세스 동안 인증서는 Azure 플랫폼에서 벗어나거나 스크립트, 명령줄 기록 또는 템플릿에 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="decce-122">During the whole process, the certificates never leave the Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="decce-123">Azure Key Vault 만들기</span><span class="sxs-lookup"><span data-stu-id="decce-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="decce-124">Key Vault 및 인증서를 만들려면 먼저 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="decce-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="decce-125">다음 예제에서는 *미국 동부* 위치에 *myResourceGroupSecureWeb*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="decce-125">The following example creates a resource group named *myResourceGroupSecureWeb* in the *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="decce-126">다음으로 [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault)를 사용하여 Key Vault를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="decce-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="decce-127">각 Key Vault에는 고유한 이름이 필요하며 모두 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="decce-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="decce-128">다음 예제에서 `<mykeyvault>`를 사용자 고유의 Key Vault 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="decce-128">Replace `<mykeyvault>` in the following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="decce-129">인증서 생성 및 Key Vault에 저장</span><span class="sxs-lookup"><span data-stu-id="decce-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="decce-130">프로덕션 사용을 위해 [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate)를 사용하여 신뢰할 수 있는 공급자가 서명한 유효한 인증서를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="decce-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="decce-131">이 자습서의 다음 예제는 [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy)에서 기본 인증서 정책을 사용하는 자체 서명된 인증서를 [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate)를 사용하여 생성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="decce-131">For this tutorial, the following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses the default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

```powershell
$policy = New-AzureKeyVaultCertificatePolicy `
    -SubjectName "CN=www.contoso.com" `
    -SecretContentType "application/x-pkcs12" `
    -IssuerName Self `
    -ValidityInMonths 12

Add-AzureKeyVaultCertificate `
    -VaultName $keyvaultName `
    -Name "mycert" `
    -CertificatePolicy $policy 
```


## <a name="create-a-virtual-machine"></a><span data-ttu-id="decce-132">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="decce-132">Create a virtual machine</span></span>
<span data-ttu-id="decce-133">[Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential)을 사용하여 VM의 관리자 사용자 이름과 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="decce-133">Set an administrator username and password for the VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="decce-134">이제 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)을 사용하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="decce-134">Now you can create the VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="decce-135">다음 예제에서는 필요한 가상 네트워크 구성 요소, OS 구성을 만든 다음 *myVM*이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="decce-135">The following example creates the required virtual network components, the OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myVnet" `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleRDP"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 443
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleWWW"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name "myNic" `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS2" | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName "myVM" -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName "MicrosoftWindowsServer" `
    -Offer "WindowsServer" -Skus "2016-Datacenter" -Version "latest" | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Create virtual machine
New-AzureRmVM -ResourceGroupName $resourceGroup -Location $location -VM $vmConfig

# Use the Custom Script Extension to install IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

<span data-ttu-id="decce-136">VM을 만드는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="decce-136">It takes a few minutes for the VM to be created.</span></span> <span data-ttu-id="decce-137">마지막 단계는 [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension)을 통해 Azure 사용자 지정 스크립트 확장을 사용하여 IIS 웹 서버를 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="decce-137">The last step uses the Azure Custom Script Extension to install the IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-to-vm-from-key-vault"></a><span data-ttu-id="decce-138">Key Vault에서 VM에 인증서 추가</span><span class="sxs-lookup"><span data-stu-id="decce-138">Add a certificate to VM from Key Vault</span></span>
<span data-ttu-id="decce-139">Key Vault에서 VM으로 인증서를 추가하려면 [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret)을 사용하여 인증서의 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="decce-139">To add the certificate from Key Vault to a VM, obtain the ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="decce-140">[Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret)을 사용하여 VM에 인증서를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="decce-140">Add the certificate to the VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-to-use-the-certificate"></a><span data-ttu-id="decce-141">인증서를 사용하도록 IIS 구성</span><span class="sxs-lookup"><span data-stu-id="decce-141">Configure IIS to use the certificate</span></span>
<span data-ttu-id="decce-142">다시 [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension)을 통해 사용자 지정 스크립트 확장을 사용하여 IIS 구성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="decce-142">Use the Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to update the IIS configuration.</span></span> <span data-ttu-id="decce-143">이 업데이트는 Key Vault에서 가져온 인증서를 IIS에 적용하고 웹 바인딩을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="decce-143">This update applies the certificate injected from Key Vault to IIS and configures the web binding:</span></span>

```powershell
$PublicSettings = '{
    "fileUris":["https://raw.githubusercontent.com/iainfoulds/azure-samples/master/secure-iis.ps1"],
    "commandToExecute":"powershell -ExecutionPolicy Unrestricted -File secure-iis.ps1"
}'

Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString $publicSettings
```


### <a name="test-the-secure-web-app"></a><span data-ttu-id="decce-144">보안 웹앱 테스트</span><span class="sxs-lookup"><span data-stu-id="decce-144">Test the secure web app</span></span>
<span data-ttu-id="decce-145">[Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress)를 사용하여 VM의 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="decce-145">Obtain the public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="decce-146">다음 예제에서는 앞서 만든 `myPublicIP`의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="decce-146">The following example obtains the IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="decce-147">이제 웹 브라우저를 열고 주소 표시줄에 `https://<myPublicIP>`를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="decce-147">Now you can open a web browser and enter `https://<myPublicIP>` in the address bar.</span></span> <span data-ttu-id="decce-148">자체 서명된 인증서를 사용하는 경우 보안 경고를 받으려면 **세부 정보**, **웹 페이지로 이동**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="decce-148">To accept the security warning if you used a self-signed certificate, select **Details** and then **Go on to the webpage**:</span></span>

![웹 브라우저 보안 경고 허용](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="decce-150">그러면 보안 IIS 웹 사이트가 다음 예제와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="decce-150">Your secured IIS website is then displayed as in the following example:</span></span>

![실행 중인 보안 IIS 사이트 보기](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="decce-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="decce-152">Next steps</span></span>

<span data-ttu-id="decce-153">이 자습서에서는 Azure Key Vault에 저장된 SSL 인증서를 사용하여 IIS 웹 서버를 보호했습니다.</span><span class="sxs-lookup"><span data-stu-id="decce-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="decce-154">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="decce-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="decce-155">Azure Key Vault 만들기</span><span class="sxs-lookup"><span data-stu-id="decce-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="decce-156">Key Vault에 인증서 생성 또는 업로드</span><span class="sxs-lookup"><span data-stu-id="decce-156">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="decce-157">VM 만들기 및 IIS 웹 서버 설치</span><span class="sxs-lookup"><span data-stu-id="decce-157">Create a VM and install the IIS web server</span></span>
> * <span data-ttu-id="decce-158">VM에 인증서 삽입 및 SSL 바인딩으로 IIS 구성</span><span class="sxs-lookup"><span data-stu-id="decce-158">Inject the certificate into the VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="decce-159">미리 빌드된 가상 컴퓨터 스크립트 샘플을 보려면 이 링크를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="decce-159">Follow this link to see pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="decce-160">Windows 가상 컴퓨터 스크립트 샘플 </span><span class="sxs-lookup"><span data-stu-id="decce-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)
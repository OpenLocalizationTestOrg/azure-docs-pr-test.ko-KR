---
title: "Azure의 Windows VM에서 Key Vault를 SQL Server에 통합(클래식) | Microsoft Docs"
description: "Azure 키 자격 증명 모음과 함께 사용하도록 SQL Server 암호화 구성을 자동화하는 방법에 대해 알아보세요. 이 항목에서는 Azure 주요 자격 증명 모음 통합을 클래식 배포 모델에서 만든 SQL Server 가상 컴퓨터와 함께 사용하는 방법에 대해 설명합니다."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: ab8d41a7-1971-4032-ab71-eb435c455dc1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 02/17/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2a9ac5763bb934bd0646e47c3936f7bdd0d603b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-classic"></a><span data-ttu-id="4d4ac-104">Azure Virtual Machines에서 SQL Server에 대한 Azure Key Vault 통합 구성(클래식)</span><span class="sxs-lookup"><span data-stu-id="4d4ac-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d4ac-105">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="4d4ac-105">Resource Manager</span></span>](../sql/virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="4d4ac-106">클래식</span><span class="sxs-lookup"><span data-stu-id="4d4ac-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="4d4ac-107">개요</span><span class="sxs-lookup"><span data-stu-id="4d4ac-107">Overview</span></span>
<span data-ttu-id="4d4ac-108">[TDE(투명한 데이터 암호화)](https://msdn.microsoft.com/library/bb934049.aspx), [CLE(열 수준 암호화)](https://msdn.microsoft.com/library/ms173744.aspx) [백업 암호화](https://msdn.microsoft.com/library/dn449489.aspx) 등 여러 SQL Server 암호화 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="4d4ac-109">이러한 형태의 암호화는 암호화에 사용되는 암호화 키를 관리 및 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-109">These forms of encryption require you to manage and store the cryptographic keys you use for encryption.</span></span> <span data-ttu-id="4d4ac-110">AKV(Azure 키 자격 증명 모음) 서비스는 안전하고 가용성이 높은 위치에서 이러한 키의 보안 및 관리를 개선하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-110">The Azure Key Vault (AKV) service is designed to improve the security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="4d4ac-111">[SQL Server 커넥터](http://www.microsoft.com/download/details.aspx?id=45344) 는 SQL Server가 Azure 주요 자격 증명 모음의 주요 항목을 사용할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-111">The [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server to use these keys from Azure Key Vault.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="4d4ac-112">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-112">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4d4ac-113">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-113">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="4d4ac-114">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-114">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="4d4ac-115">온-프레미스 컴퓨터로 SQL Server를 실행하는 경우 [온-프레미스 SQL Server 컴퓨터에서 Azure 키 자격 증명 모음에 액세스할 수 있는 단계](https://msdn.microsoft.com/library/dn198405.aspx)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-115">If you are running SQL Server with on-premises machines, there are [steps you can follow to access Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="4d4ac-116">하지만 Azure VM의 SQL Server에서는 *Azure 주요 자격 증명 모음 통합* 기능을 사용하여 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-116">But for SQL Server in Azure VMs, you can save time by using the *Azure Key Vault Integration* feature.</span></span> <span data-ttu-id="4d4ac-117">이 기능을 지원하는 Azure PowerShell cmdlet 몇 개만 있으면 SQL VM이 키 자격 증명 모음에 액세스하는 데 필요한 구성을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-117">With a few Azure PowerShell cmdlets to enable this feature, you can automate the configuration necessary for a SQL VM to access your key vault.</span></span>

<span data-ttu-id="4d4ac-118">이 기능은 활성화되면 자동으로 SQL Server 커넥터를 설치하고, Azure 키 자격 증명 모음에 액세스하도록 EKM 공급자를 구성하고, 사용자가 자격 증명 모음에 액세스할 수 있도록 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-118">When this feature is enabled, it automatically installs the SQL Server Connector, configures the EKM provider to access Azure Key Vault, and creates the credential to allow you to access your vault.</span></span> <span data-ttu-id="4d4ac-119">앞에서 언급한 온-프레미스 설명서의 단계를 살펴보셨다면 이 기능이 2 및 3단계를 자동화한다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-119">If you looked at the steps in the previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="4d4ac-120">사용자가 수동으로 해야 하는 유일한 일은 키 자격 증명 모음 및 키를 만드는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-120">The only thing you would still need to do manually is to create the key vault and keys.</span></span> <span data-ttu-id="4d4ac-121">그 이후에 SQL VM을 설정하는 전체 과정이 자동화됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-121">From there, the entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="4d4ac-122">이 기능이 설정을 완료하면 사용자는 T-SQL 문을 실행하여 평소와 같이 데이터베이스 암호화 또는 백업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-122">Once this feature has completed this setup, you can execute T-SQL statements to begin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="configure-akv-integration"></a><span data-ttu-id="4d4ac-123">AKV 통합 구성</span><span class="sxs-lookup"><span data-stu-id="4d4ac-123">Configure AKV Integration</span></span>
<span data-ttu-id="4d4ac-124">PowerShell을 사용하여 Azure 키 자격 증명 모음 통합을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-124">Use PowerShell to configure Azure Key Vault Integration.</span></span> <span data-ttu-id="4d4ac-125">다음 섹션에서는 필수 매개 변수 및 샘플 PowerShell 스크립트의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-125">The following sections provide an overview of the required parameters and then a sample PowerShell script.</span></span>

### <a name="install-the-sql-server-iaas-extension"></a><span data-ttu-id="4d4ac-126">SQL Server IaaS 확장 설치</span><span class="sxs-lookup"><span data-stu-id="4d4ac-126">Install the SQL Server IaaS Extension</span></span>
<span data-ttu-id="4d4ac-127">먼저 [SQL Server IaaS 확장을 설치](../classic/sql-server-agent-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-127">First, [install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

### <a name="understand-the-input-parameters"></a><span data-ttu-id="4d4ac-128">입력 매개 변수 이해</span><span class="sxs-lookup"><span data-stu-id="4d4ac-128">Understand the input parameters</span></span>
<span data-ttu-id="4d4ac-129">다음 표에는 다음 섹션에는 PowerShell 스크립트를 실행하는 데 필요한 매개 변수가 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-129">The following table lists the parameters required to run the PowerShell script in the next section.</span></span>

| <span data-ttu-id="4d4ac-130">매개 변수</span><span class="sxs-lookup"><span data-stu-id="4d4ac-130">Parameter</span></span> | <span data-ttu-id="4d4ac-131">설명</span><span class="sxs-lookup"><span data-stu-id="4d4ac-131">Description</span></span> | <span data-ttu-id="4d4ac-132">예</span><span class="sxs-lookup"><span data-stu-id="4d4ac-132">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4d4ac-133">**$akvURL**</span><span class="sxs-lookup"><span data-stu-id="4d4ac-133">**$akvURL**</span></span> |<span data-ttu-id="4d4ac-134">**키 자격 증명 모음 URL**</span><span class="sxs-lookup"><span data-stu-id="4d4ac-134">**The key vault URL**</span></span> |<span data-ttu-id="4d4ac-135">"https://contosokeyvault.vault.azure.net/"</span><span class="sxs-lookup"><span data-stu-id="4d4ac-135">"https://contosokeyvault.vault.azure.net/"</span></span> |
| <span data-ttu-id="4d4ac-136">**$spName**</span><span class="sxs-lookup"><span data-stu-id="4d4ac-136">**$spName**</span></span> |<span data-ttu-id="4d4ac-137">**서비스 주체 이름**</span><span class="sxs-lookup"><span data-stu-id="4d4ac-137">**Service Principal name**</span></span> |<span data-ttu-id="4d4ac-138">"fde2b411-33d5-4e11-af04eb07b669ccf2"</span><span class="sxs-lookup"><span data-stu-id="4d4ac-138">"fde2b411-33d5-4e11-af04eb07b669ccf2"</span></span> |
| <span data-ttu-id="4d4ac-139">**$spSecret**</span><span class="sxs-lookup"><span data-stu-id="4d4ac-139">**$spSecret**</span></span> |<span data-ttu-id="4d4ac-140">**서비스 주체 암호**</span><span class="sxs-lookup"><span data-stu-id="4d4ac-140">**Service Principal secret**</span></span> |<span data-ttu-id="4d4ac-141">"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="</span><span class="sxs-lookup"><span data-stu-id="4d4ac-141">"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="</span></span> |
| <span data-ttu-id="4d4ac-142">**$credName**</span><span class="sxs-lookup"><span data-stu-id="4d4ac-142">**$credName**</span></span> |<span data-ttu-id="4d4ac-143">**자격 증명 이름**: AKV 통합은 VM이 주요 자격 증명 모음에 액세스할 수 있도록 SQL Server 내에 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-143">**Credential name**: AKV Integration creates a credential within SQL Server, allowing the VM to have access to the key vault.</span></span> <span data-ttu-id="4d4ac-144">이 자격 증명의 이름을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-144">Choose a name for this credential.</span></span> |<span data-ttu-id="4d4ac-145">"mycred1"</span><span class="sxs-lookup"><span data-stu-id="4d4ac-145">"mycred1"</span></span> |
| <span data-ttu-id="4d4ac-146">**$vmName**</span><span class="sxs-lookup"><span data-stu-id="4d4ac-146">**$vmName**</span></span> |<span data-ttu-id="4d4ac-147">**가상 컴퓨터 이름**: 이전에 만든 SQL VM의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-147">**Virtual machine name**: The name of a previously created SQL VM.</span></span> |<span data-ttu-id="4d4ac-148">"myvmname"</span><span class="sxs-lookup"><span data-stu-id="4d4ac-148">"myvmname"</span></span> |
| <span data-ttu-id="4d4ac-149">**$serviceName**</span><span class="sxs-lookup"><span data-stu-id="4d4ac-149">**$serviceName**</span></span> |<span data-ttu-id="4d4ac-150">**서비스 이름**: SQL VM과 연결된 클라우드 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-150">**Service name**: The Cloud Service name that is associated with the SQL VM.</span></span> |<span data-ttu-id="4d4ac-151">"mycloudservicename"</span><span class="sxs-lookup"><span data-stu-id="4d4ac-151">"mycloudservicename"</span></span> |

### <a name="enable-akv-integration-with-powershell"></a><span data-ttu-id="4d4ac-152">PowerShell과 AKV 통합 설정</span><span class="sxs-lookup"><span data-stu-id="4d4ac-152">Enable AKV Integration with PowerShell</span></span>
<span data-ttu-id="4d4ac-153">**New-AzureVMSqlServerKeyVaultCredentialConfig** cmdlet은 Azure Key Vault Integration 기능에 대한 구성 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-153">The **New-AzureVMSqlServerKeyVaultCredentialConfig** cmdlet creates a configuration object for the Azure Key Vault Integration feature.</span></span> <span data-ttu-id="4d4ac-154">**Set-AzureVMSqlServerExtension**은 **KeyVaultCredentialSettings** 매개 변수와의 통합을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-154">The **Set-AzureVMSqlServerExtension** configures this integration with the **KeyVaultCredentialSettings** parameter.</span></span> <span data-ttu-id="4d4ac-155">다음 단계에서는 이러한 명령을 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-155">The following steps show how to use these commands.</span></span>

1. <span data-ttu-id="4d4ac-156">이 항목의 이전 섹션에서 설명한 대로, 먼저 Azure PowerShell에서 특정 값을 사용하여 입력 매개 변수를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-156">In Azure PowerShell, first configure the input parameters with your specific values as described in the previous sections of this topic.</span></span> <span data-ttu-id="4d4ac-157">다음은 스크립트 예입니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-157">The following script is an example.</span></span>
   
        $akvURL = "https://contosokeyvault.vault.azure.net/"
        $spName = "fde2b411-33d5-4e11-af04eb07b669ccf2"
        $spSecret = "9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="
        $credName = "mycred1"
        $vmName = "myvmname"
        $serviceName = "mycloudservicename"
2. <span data-ttu-id="4d4ac-158">그런 후 다음 스크립트를 사용하여 AKV 통합을 구성 및 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-158">Then use the following script to configure and enable AKV Integration.</span></span>
   
        $secureakv =  $spSecret | ConvertTo-SecureString -AsPlainText -Force
        $akvs = New-AzureVMSqlServerKeyVaultCredentialConfig -Enable -CredentialName $credname -AzureKeyVaultUrl $akvURL -ServicePrincipalName $spName -ServicePrincipalSecret $secureakv
        Get-AzureVM -ServiceName $serviceName -Name $vmName | Set-AzureVMSqlServerExtension -KeyVaultCredentialSettings $akvs | Update-AzureVM

<span data-ttu-id="4d4ac-159">SQL IaaS 에이전트 확장에서 이 새로운 구성을 사용하여 SQL VM을 업데이트할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4d4ac-159">The SQL IaaS Agent Extension will update the SQL VM with this new configuration.</span></span>

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]


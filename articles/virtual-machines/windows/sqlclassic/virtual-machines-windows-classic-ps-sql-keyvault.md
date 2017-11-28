---
title: "Azure (클래식)에서 Windows Vm에서 SQL Server 자격 증명 모음 키 aaaIntegrate | Microsoft Docs"
description: "어떻게 tooautomate hello Azure 키 자격 증명 사용 하기 위해 SQL Server 암호화 구성에 알아봅니다. 이 항목에서는 SQL Server 가상 컴퓨터와 Azure 키 자격 증명 모음 통합 toouse hello 클래식 배포 모델에서 만드는 방법을 설명 합니다."
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
ms.openlocfilehash: 54664875b76dac7271d5a9f00b3f41fdc9c08491
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-classic"></a><span data-ttu-id="44c06-104">Azure Virtual Machines에서 SQL Server에 대한 Azure Key Vault 통합 구성(클래식)</span><span class="sxs-lookup"><span data-stu-id="44c06-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="44c06-105">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="44c06-105">Resource Manager</span></span>](../sql/virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="44c06-106">클래식</span><span class="sxs-lookup"><span data-stu-id="44c06-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="44c06-107">개요</span><span class="sxs-lookup"><span data-stu-id="44c06-107">Overview</span></span>
<span data-ttu-id="44c06-108">[TDE(투명한 데이터 암호화)](https://msdn.microsoft.com/library/bb934049.aspx), [CLE(열 수준 암호화)](https://msdn.microsoft.com/library/ms173744.aspx) [백업 암호화](https://msdn.microsoft.com/library/dn449489.aspx) 등 여러 SQL Server 암호화 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="44c06-109">이러한 형태의 암호화 toomanage 요구 하 고 암호화에 사용 하는 hello 암호화 키를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-109">These forms of encryption require you toomanage and store hello cryptographic keys you use for encryption.</span></span> <span data-ttu-id="44c06-110">hello Azure 키 자격 증명 모음 (AKV) 서비스 안전 하 고 항상 사용 가능한 위치에 이러한 키의 디자인 된 tooimprove hello 보안 및 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-110">hello Azure Key Vault (AKV) service is designed tooimprove hello security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="44c06-111">hello [SQL Server 커넥터](http://www.microsoft.com/download/details.aspx?id=45344) 사용 하면 SQL Server toouse Azure 키 자격 증명 모음에서 이러한 키입니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-111">hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server toouse these keys from Azure Key Vault.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="44c06-112">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-112">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="44c06-113">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-113">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="44c06-114">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-114">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="44c06-115">온-프레미스 컴퓨터와 SQL Server를 실행 하는 경우 없는 [온-프레미스 SQL Server 컴퓨터에서 tooaccess Azure 키 자격 증명 모음을 수행할 수 있는 단계](https://msdn.microsoft.com/library/dn198405.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-115">If you are running SQL Server with on-premises machines, there are [steps you can follow tooaccess Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="44c06-116">Azure Vm에서 SQL Server에 대 한 hello를 사용 하 여 시간을 절약할 수 있습니다 하지만 *Azure 키 자격 증명 모음 통합* 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-116">But for SQL Server in Azure VMs, you can save time by using hello *Azure Key Vault Integration* feature.</span></span> <span data-ttu-id="44c06-117">몇 가지 Azure PowerShell cmdlet tooenable와이 기능을 자동화할 수 있습니다 hello 구성에 대 한 SQL VM tooaccess 필요한 주요 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-117">With a few Azure PowerShell cmdlets tooenable this feature, you can automate hello configuration necessary for a SQL VM tooaccess your key vault.</span></span>

<span data-ttu-id="44c06-118">이 기능을 사용할 때 자동으로 설치 hello SQL Server 커넥터, hello EKM 공급자 tooaccess Azure 키 자격 증명 모음을 구성 하 고 hello 자격 증명 tooallow 만듭니다 있습니다 tooaccess 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-118">When this feature is enabled, it automatically installs hello SQL Server Connector, configures hello EKM provider tooaccess Azure Key Vault, and creates hello credential tooallow you tooaccess your vault.</span></span> <span data-ttu-id="44c06-119">살펴본 hello의 hello 단계는 온-프레미스 설명서에 앞에서 언급 한 면이 기능은 단계 2와 3 단계를 자동화를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-119">If you looked at hello steps in hello previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="44c06-120">hello 여전히 필요할 toodo 수동으로만 toocreate hello 주요 자격 증명 모음 및 키.</span><span class="sxs-lookup"><span data-stu-id="44c06-120">hello only thing you would still need toodo manually is toocreate hello key vault and keys.</span></span> <span data-ttu-id="44c06-121">여기에서 hello SQL VM의 전체 설치 자동화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-121">From there, hello entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="44c06-122">이 기능은이 설치 프로그램이 완료 되 면 평소와 같이 데이터베이스 또는 백업을 암호화 하는 T-SQL 문을 toobegin를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-122">Once this feature has completed this setup, you can execute T-SQL statements toobegin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="configure-akv-integration"></a><span data-ttu-id="44c06-123">AKV 통합 구성</span><span class="sxs-lookup"><span data-stu-id="44c06-123">Configure AKV Integration</span></span>
<span data-ttu-id="44c06-124">PowerShell tooconfigure Azure 키 자격 증명 모음 통합을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-124">Use PowerShell tooconfigure Azure Key Vault Integration.</span></span> <span data-ttu-id="44c06-125">다음 섹션 hello hello 필수 매개 변수에 대 한 개요 및 샘플 PowerShell 스크립트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-125">hello following sections provide an overview of hello required parameters and then a sample PowerShell script.</span></span>

### <a name="install-hello-sql-server-iaas-extension"></a><span data-ttu-id="44c06-126">SQL Server IaaS 확장 hello를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-126">Install hello SQL Server IaaS Extension</span></span>
<span data-ttu-id="44c06-127">첫째, [hello SQL Server IaaS 확장 설치](../classic/sql-server-agent-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-127">First, [install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

### <a name="understand-hello-input-parameters"></a><span data-ttu-id="44c06-128">Hello 입력된 매개 변수 이해</span><span class="sxs-lookup"><span data-stu-id="44c06-128">Understand hello input parameters</span></span>
<span data-ttu-id="44c06-129">hello 다음 테이블 목록 hello 매개 변수 필수 hello 다음 섹션에서 toorun hello PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-129">hello following table lists hello parameters required toorun hello PowerShell script in hello next section.</span></span>

| <span data-ttu-id="44c06-130">매개 변수</span><span class="sxs-lookup"><span data-stu-id="44c06-130">Parameter</span></span> | <span data-ttu-id="44c06-131">설명</span><span class="sxs-lookup"><span data-stu-id="44c06-131">Description</span></span> | <span data-ttu-id="44c06-132">예</span><span class="sxs-lookup"><span data-stu-id="44c06-132">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44c06-133">**$akvURL**</span><span class="sxs-lookup"><span data-stu-id="44c06-133">**$akvURL**</span></span> |<span data-ttu-id="44c06-134">**hello 주요 자격 증명 모음 URL**</span><span class="sxs-lookup"><span data-stu-id="44c06-134">**hello key vault URL**</span></span> |<span data-ttu-id="44c06-135">"https://contosokeyvault.vault.azure.net/"</span><span class="sxs-lookup"><span data-stu-id="44c06-135">"https://contosokeyvault.vault.azure.net/"</span></span> |
| <span data-ttu-id="44c06-136">**$spName**</span><span class="sxs-lookup"><span data-stu-id="44c06-136">**$spName**</span></span> |<span data-ttu-id="44c06-137">**서비스 주체 이름**</span><span class="sxs-lookup"><span data-stu-id="44c06-137">**Service Principal name**</span></span> |<span data-ttu-id="44c06-138">"fde2b411-33d5-4e11-af04eb07b669ccf2"</span><span class="sxs-lookup"><span data-stu-id="44c06-138">"fde2b411-33d5-4e11-af04eb07b669ccf2"</span></span> |
| <span data-ttu-id="44c06-139">**$spSecret**</span><span class="sxs-lookup"><span data-stu-id="44c06-139">**$spSecret**</span></span> |<span data-ttu-id="44c06-140">**서비스 주체 암호**</span><span class="sxs-lookup"><span data-stu-id="44c06-140">**Service Principal secret**</span></span> |<span data-ttu-id="44c06-141">"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="</span><span class="sxs-lookup"><span data-stu-id="44c06-141">"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="</span></span> |
| <span data-ttu-id="44c06-142">**$credName**</span><span class="sxs-lookup"><span data-stu-id="44c06-142">**$credName**</span></span> |<span data-ttu-id="44c06-143">**자격 증명 이름**: AKV 통합 hello VM toohave 액세스 toohello 주요 자격 증명 모음을 허용 하는 SQL Server 내에서 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-143">**Credential name**: AKV Integration creates a credential within SQL Server, allowing hello VM toohave access toohello key vault.</span></span> <span data-ttu-id="44c06-144">이 자격 증명의 이름을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="44c06-144">Choose a name for this credential.</span></span> |<span data-ttu-id="44c06-145">"mycred1"</span><span class="sxs-lookup"><span data-stu-id="44c06-145">"mycred1"</span></span> |
| <span data-ttu-id="44c06-146">**$vmName**</span><span class="sxs-lookup"><span data-stu-id="44c06-146">**$vmName**</span></span> |<span data-ttu-id="44c06-147">**가상 컴퓨터 이름**: 이전에 만든된 SQL VM의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-147">**Virtual machine name**: hello name of a previously created SQL VM.</span></span> |<span data-ttu-id="44c06-148">"myvmname"</span><span class="sxs-lookup"><span data-stu-id="44c06-148">"myvmname"</span></span> |
| <span data-ttu-id="44c06-149">**$serviceName**</span><span class="sxs-lookup"><span data-stu-id="44c06-149">**$serviceName**</span></span> |<span data-ttu-id="44c06-150">**서비스 이름**: hello SQL VM과 연관 된 hello 클라우드 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-150">**Service name**: hello Cloud Service name that is associated with hello SQL VM.</span></span> |<span data-ttu-id="44c06-151">"mycloudservicename"</span><span class="sxs-lookup"><span data-stu-id="44c06-151">"mycloudservicename"</span></span> |

### <a name="enable-akv-integration-with-powershell"></a><span data-ttu-id="44c06-152">PowerShell과 AKV 통합 설정</span><span class="sxs-lookup"><span data-stu-id="44c06-152">Enable AKV Integration with PowerShell</span></span>
<span data-ttu-id="44c06-153">hello **새로 AzureVMSqlServerKeyVaultCredentialConfig** cmdlet hello Azure 키 자격 증명 모음 통합 기능에 대 한 구성 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-153">hello **New-AzureVMSqlServerKeyVaultCredentialConfig** cmdlet creates a configuration object for hello Azure Key Vault Integration feature.</span></span> <span data-ttu-id="44c06-154">hello **집합 AzureVMSqlServerExtension** hello와이 통합이 구성 **KeyVaultCredentialSettings** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-154">hello **Set-AzureVMSqlServerExtension** configures this integration with hello **KeyVaultCredentialSettings** parameter.</span></span> <span data-ttu-id="44c06-155">단계 표시 방법을 따르는 hello toouse 이러한 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-155">hello following steps show how toouse these commands.</span></span>

1. <span data-ttu-id="44c06-156">Azure PowerShell에서 먼저 구성 hello 입력된 매개 변수가 특정 값으로이 항목의 hello 이전 섹션에 설명 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-156">In Azure PowerShell, first configure hello input parameters with your specific values as described in hello previous sections of this topic.</span></span> <span data-ttu-id="44c06-157">다음 스크립트는 hello 예입니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-157">hello following script is an example.</span></span>
   
        $akvURL = "https://contosokeyvault.vault.azure.net/"
        $spName = "fde2b411-33d5-4e11-af04eb07b669ccf2"
        $spSecret = "9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="
        $credName = "mycred1"
        $vmName = "myvmname"
        $serviceName = "mycloudservicename"
2. <span data-ttu-id="44c06-158">그런 다음 사용 하 여 hello 다음 tooconfigure 및 스크립트 AKV 통합을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-158">Then use hello following script tooconfigure and enable AKV Integration.</span></span>
   
        $secureakv =  $spSecret | ConvertTo-SecureString -AsPlainText -Force
        $akvs = New-AzureVMSqlServerKeyVaultCredentialConfig -Enable -CredentialName $credname -AzureKeyVaultUrl $akvURL -ServicePrincipalName $spName -ServicePrincipalSecret $secureakv
        Get-AzureVM -ServiceName $serviceName -Name $vmName | Set-AzureVMSqlServerExtension -KeyVaultCredentialSettings $akvs | Update-AzureVM

<span data-ttu-id="44c06-159">SQL IaaS 에이전트 확장 hello이 새 구성을 사용 하 여 hello SQL VM을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="44c06-159">hello SQL IaaS Agent Extension will update hello SQL VM with this new configuration.</span></span>

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]


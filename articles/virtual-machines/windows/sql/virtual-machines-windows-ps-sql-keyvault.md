---
title: "키 자격 증명 모음 (리소스 관리자) Azure에서 Windows Vm에서 SQL Server와 함께 aaaIntegrate | Microsoft Docs"
description: "어떻게 tooautomate hello Azure 키 자격 증명 사용 하기 위해 SQL Server 암호화 구성에 알아봅니다. 이 항목에서는 SQL Server 가상 컴퓨터와 Azure 키 자격 증명 모음 통합 toouse 리소스 관리자를 사용 하 여 생성 하는 방법을 설명 합니다."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: cd66dfb1-0e9b-4fb0-a471-9deaf4ab4ab8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: jroth
ms.openlocfilehash: 0d36d3d075d6538c18cd5ecb43c19a4b000a99e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a><span data-ttu-id="4f03b-104">Azure Virtual Machines에서 SQL Server에 대한 Azure Key Vault 통합 구성(Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="4f03b-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f03b-105">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="4f03b-105">Resource Manager</span></span>](virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="4f03b-106">클래식</span><span class="sxs-lookup"><span data-stu-id="4f03b-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="4f03b-107">개요</span><span class="sxs-lookup"><span data-stu-id="4f03b-107">Overview</span></span>
<span data-ttu-id="4f03b-108">[TDE(투명한 데이터 암호화)](https://msdn.microsoft.com/library/bb934049.aspx), [CLE(열 수준 암호화)](https://msdn.microsoft.com/library/ms173744.aspx) [백업 암호화](https://msdn.microsoft.com/library/dn449489.aspx) 등 여러 SQL Server 암호화 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="4f03b-109">이러한 형태의 암호화 toomanage 요구 하 고 암호화에 사용 하는 hello 암호화 키를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-109">These forms of encryption require you toomanage and store hello cryptographic keys you use for encryption.</span></span> <span data-ttu-id="4f03b-110">hello Azure 키 자격 증명 모음 (AKV) 서비스 안전 하 고 항상 사용 가능한 위치에 이러한 키의 디자인 된 tooimprove hello 보안 및 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-110">hello Azure Key Vault (AKV) service is designed tooimprove hello security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="4f03b-111">hello [SQL Server 커넥터](http://www.microsoft.com/download/details.aspx?id=45344) 사용 하면 SQL Server toouse Azure 키 자격 증명 모음에서 이러한 키입니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-111">hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server toouse these keys from Azure Key Vault.</span></span>

<span data-ttu-id="4f03b-112">하는 경우 온-프레미스 SQL Server를 실행 하면 컴퓨터의 경우 있습니다는 [온-프레미스 SQL Server 컴퓨터에서 tooaccess Azure 키 자격 증명 모음을 수행할 수 있는 단계](https://msdn.microsoft.com/library/dn198405.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-112">If you running SQL Server with on-premises machines, there are [steps you can follow tooaccess Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="4f03b-113">Azure Vm에서 SQL Server에 대 한 hello를 사용 하 여 시간을 절약할 수 있습니다 하지만 *Azure 키 자격 증명 모음 통합* 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-113">But for SQL Server in Azure VMs, you can save time by using hello *Azure Key Vault Integration* feature.</span></span>

<span data-ttu-id="4f03b-114">이 기능을 사용할 때 자동으로 설치 hello SQL Server 커넥터, hello EKM 공급자 tooaccess Azure 키 자격 증명 모음을 구성 하 고 hello 자격 증명 tooallow 만듭니다 있습니다 tooaccess 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-114">When this feature is enabled, it automatically installs hello SQL Server Connector, configures hello EKM provider tooaccess Azure Key Vault, and creates hello credential tooallow you tooaccess your vault.</span></span> <span data-ttu-id="4f03b-115">살펴본 hello의 hello 단계는 온-프레미스 설명서에 앞에서 언급 한 면이 기능은 단계 2와 3 단계를 자동화를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-115">If you looked at hello steps in hello previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="4f03b-116">hello 여전히 필요할 toodo 수동으로만 toocreate hello 주요 자격 증명 모음 및 키.</span><span class="sxs-lookup"><span data-stu-id="4f03b-116">hello only thing you would still need toodo manually is toocreate hello key vault and keys.</span></span> <span data-ttu-id="4f03b-117">여기에서 hello SQL VM의 전체 설치 자동화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-117">From there, hello entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="4f03b-118">이 기능은이 설치 프로그램이 완료 되 면 평소와 같이 데이터베이스 또는 백업을 암호화 하는 T-SQL 문을 toobegin를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-118">Once this feature has completed this setup, you can execute T-SQL statements toobegin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a><span data-ttu-id="4f03b-119">AKV 통합 설정 및 구성</span><span class="sxs-lookup"><span data-stu-id="4f03b-119">Enabling and configuring AKV integration</span></span>
<span data-ttu-id="4f03b-120">기존 VM에 대해 프로비전닝 또는 구성하는 동안 AKV 통합을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="4f03b-121">새 VM</span><span class="sxs-lookup"><span data-stu-id="4f03b-121">New VMs</span></span>
<span data-ttu-id="4f03b-122">리소스 관리자를 사용 하 여 새 SQL Server 가상 컴퓨터 프로 비전 하는 경우 Azure 포털 hello 단계 tooenable Azure 키 자격 증명 모음 통합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, hello Azure portal provides a step tooenable Azure Key Vault integration.</span></span> <span data-ttu-id="4f03b-123">hello Azure 키 자격 증명 모음 기능은 hello Enterprise, Developer 및 Evaluation SQL Server 버전에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-123">hello Azure Key Vault feature is available only for hello Enterprise, Developer and Evaluation Editions of SQL Server.</span></span>

![SQL Azure Key Vault 통합](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

<span data-ttu-id="4f03b-125">프로 비전의 자세한 연습을 참조 하십시오. [hello Azure 포털에서에서 SQL Server 가상 컴퓨터를 프로 비전](virtual-machines-windows-portal-sql-server-provision.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in hello Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="4f03b-126">기존 VM</span><span class="sxs-lookup"><span data-stu-id="4f03b-126">Existing VMs</span></span>
<span data-ttu-id="4f03b-127">기존 SQL Server 가상 컴퓨터에 대한 해당 SQL Server 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="4f03b-128">다음 hello 선택 **SQL Server 구성** hello 섹션 **설정** 블레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-128">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![기존 VM에 대한 SQL AKV 통합](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

<span data-ttu-id="4f03b-130">Hello에 **SQL Server 구성** 블레이드에서 hello 클릭 **편집** hello 자동화 된 키 자격 증명 모음 통합 섹션에에서는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-130">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated Key Vault integration section.</span></span>

![기존 VM에 대한 SQL AKV 통합 구성](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

<span data-ttu-id="4f03b-132">완료 되 면 hello 클릭 **확인** hello hello 하단에서 단추 **SQL Server 구성** 블레이드 toosave 변경 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-132">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

> [!NOTE]
> <span data-ttu-id="4f03b-133">또한 템플릿을 사용하여 AKV 통합을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f03b-133">You can also configure AKV integration using a template.</span></span> <span data-ttu-id="4f03b-134">자세한 내용은 [Azure 주요 자격 증명 모음 통합을 위한 Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f03b-134">For more information, see [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span></span>
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]


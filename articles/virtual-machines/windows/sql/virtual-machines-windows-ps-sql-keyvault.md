---
title: "Azure의 Windows VM에서 Key Vault를 SQL Server에 통합(Resource Manager) | Microsoft Docs"
description: "Azure 키 자격 증명 모음과 함께 사용하도록 SQL Server 암호화 구성을 자동화하는 방법에 대해 알아보세요. 이 항목에서는 Azure 주요 자격 증명 모음 통합을 리소스 관리자로 만든 SQL Server 가상 컴퓨터와 함께 사용하는 방법에 대해 설명합니다."
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
ms.openlocfilehash: 32b9564fa5c9ca6864ade343fda309b2c3edf123
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a><span data-ttu-id="a9881-104">Azure Virtual Machines에서 SQL Server에 대한 Azure Key Vault 통합 구성(Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="a9881-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a9881-105">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="a9881-105">Resource Manager</span></span>](virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="a9881-106">클래식</span><span class="sxs-lookup"><span data-stu-id="a9881-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="a9881-107">개요</span><span class="sxs-lookup"><span data-stu-id="a9881-107">Overview</span></span>
<span data-ttu-id="a9881-108">[TDE(투명한 데이터 암호화)](https://msdn.microsoft.com/library/bb934049.aspx), [CLE(열 수준 암호화)](https://msdn.microsoft.com/library/ms173744.aspx) [백업 암호화](https://msdn.microsoft.com/library/dn449489.aspx) 등 여러 SQL Server 암호화 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="a9881-109">이러한 형태의 암호화는 암호화에 사용되는 암호화 키를 관리 및 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-109">These forms of encryption require you to manage and store the cryptographic keys you use for encryption.</span></span> <span data-ttu-id="a9881-110">AKV(Azure 키 자격 증명 모음) 서비스는 안전하고 가용성이 높은 위치에서 이러한 키의 보안 및 관리를 개선하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-110">The Azure Key Vault (AKV) service is designed to improve the security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="a9881-111">[SQL Server 커넥터](http://www.microsoft.com/download/details.aspx?id=45344) 는 SQL Server가 Azure 키 자격 증명 모음의 키를 사용할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-111">The [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server to use these keys from Azure Key Vault.</span></span>

<span data-ttu-id="a9881-112">온-프레미스 컴퓨터로 SQL Server를 실행하는 경우 [온-프레미스 SQL Server 컴퓨터에서 Azure 키 자격 증명 모음에 액세스할 수 있는 단계](https://msdn.microsoft.com/library/dn198405.aspx)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-112">If you running SQL Server with on-premises machines, there are [steps you can follow to access Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="a9881-113">하지만 Azure VM의 SQL Server에서는 *Azure 주요 자격 증명 모음 통합* 기능을 사용하여 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-113">But for SQL Server in Azure VMs, you can save time by using the *Azure Key Vault Integration* feature.</span></span>

<span data-ttu-id="a9881-114">이 기능은 활성화되면 자동으로 SQL Server 커넥터를 설치하고, Azure 키 자격 증명 모음에 액세스하도록 EKM 공급자를 구성하고, 사용자가 자격 증명 모음에 액세스할 수 있도록 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-114">When this feature is enabled, it automatically installs the SQL Server Connector, configures the EKM provider to access Azure Key Vault, and creates the credential to allow you to access your vault.</span></span> <span data-ttu-id="a9881-115">앞에서 언급한 온-프레미스 설명서의 단계를 살펴보셨다면 이 기능이 2 및 3단계를 자동화한다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-115">If you looked at the steps in the previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="a9881-116">사용자가 수동으로 해야 하는 유일한 일은 키 자격 증명 모음 및 키를 만드는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-116">The only thing you would still need to do manually is to create the key vault and keys.</span></span> <span data-ttu-id="a9881-117">그 이후에 SQL VM을 설정하는 전체 과정이 자동화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-117">From there, the entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="a9881-118">이 기능이 설정을 완료하면 사용자는 T-SQL 문을 실행하여 평소와 같이 데이터베이스 암호화 또는 백업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-118">Once this feature has completed this setup, you can execute T-SQL statements to begin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a><span data-ttu-id="a9881-119">AKV 통합 설정 및 구성</span><span class="sxs-lookup"><span data-stu-id="a9881-119">Enabling and configuring AKV integration</span></span>
<span data-ttu-id="a9881-120">기존 VM에 대해 프로비전닝 또는 구성하는 동안 AKV 통합을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="a9881-121">새 VM</span><span class="sxs-lookup"><span data-stu-id="a9881-121">New VMs</span></span>
<span data-ttu-id="a9881-122">리소스 관리자와 함께 새 SQL Server 가상 컴퓨터를 프로비전하는 경우 Azure 포털은 Azure 키 자격 증명 모음 통합을 사용하도록 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, the Azure portal provides a step to enable Azure Key Vault integration.</span></span> <span data-ttu-id="a9881-123">Azure Key Vault 기능은 SQL Server Enterprise, Developer 및 평가판 버전에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-123">The Azure Key Vault feature is available only for the Enterprise, Developer and Evaluation Editions of SQL Server.</span></span>

![SQL Azure 주요 자격 증명 모음 통합](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

<span data-ttu-id="a9881-125">프로비전의 자세한 연습은 [Azure 포털에서 SQL Server 가상 컴퓨터 프로비전](virtual-machines-windows-portal-sql-server-provision.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9881-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in the Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="a9881-126">기존 VM</span><span class="sxs-lookup"><span data-stu-id="a9881-126">Existing VMs</span></span>
<span data-ttu-id="a9881-127">기존 SQL Server 가상 컴퓨터에 대한 해당 SQL Server 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="a9881-128">그런 다음 **설정** 블레이드의 **SQL Server 구성** 섹션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-128">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![기존 VM에 대한 SQL AKV 통합](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

<span data-ttu-id="a9881-130">**SQL Server 구성** 블레이드에서 자동화된 Key Vault 통합 섹션의 **편집** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-130">In the **SQL Server configuration** blade, click the **Edit** button in the Automated Key Vault integration section.</span></span>

![기존 VM에 대한 SQL AKV 통합 구성](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

<span data-ttu-id="a9881-132">완료되면 **SQL Server 구성** 블레이드 아래쪽의 **확인** 단추를 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-132">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

> [!NOTE]
> <span data-ttu-id="a9881-133">또한 템플릿을 사용하여 AKV 통합을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9881-133">You can also configure AKV integration using a template.</span></span> <span data-ttu-id="a9881-134">자세한 내용은 [Azure 주요 자격 증명 모음 통합을 위한 Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9881-134">For more information, see [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span></span>
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]


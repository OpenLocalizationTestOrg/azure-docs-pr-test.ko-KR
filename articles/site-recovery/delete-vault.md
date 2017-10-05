---
title: "Site Recovery 자격 증명 모음 삭제"
description: "Site Recovery 시나리오에 따라 Azure Site Recovery 자격 증명 모음을 삭제하는 방법에 대해 알아봅니다."
service: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: b95b9defa0a037f7d7d3ef36b99bc7c53c751050
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="7e914-103">Site Recovery 자격 증명 모음 삭제</span><span class="sxs-lookup"><span data-stu-id="7e914-103">Delete a Site Recovery vault</span></span>
<span data-ttu-id="7e914-104">종속성으로 인해 Azure Site Recovery 자격 증명 모음을 삭제하지 못할 수 있으며,</span><span class="sxs-lookup"><span data-stu-id="7e914-104">Dependencies can prevent you from deleting an Azure Site Recovery vault.</span></span> <span data-ttu-id="7e914-105">VMWare에서 Azure로, Hyper-V(System Center Virtual Machine Manager 있음 및 없음)에서 Azure로 및 Azure Backup과 같은 Site Recovery 시나리오에 따라 수행해야 하는 작업이 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-105">The actions you need to take vary based on the Site Recovery scenario: VMware to Azure, Hyper-V (with and without System Center Virtual Machine Manager) to Azure, and Azure Backup.</span></span> <span data-ttu-id="7e914-106">Azure Backup에서 사용되는 자격 증명 모음을 삭제하려면 [Azure에서 백업 자격 증명 모음 삭제](../backup/backup-azure-delete-vault.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7e914-106">To delete a vault used in Azure Backup, see [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md).</span></span>

>[!Important]
><span data-ttu-id="7e914-107">제품을 테스트하고 데이터 손실을 우려하지 않는다면 강제 삭제 방법을 사용하여 자격 증명 모음 및 모든 해당 종속성을 빠르게 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-107">If you're testing the product and aren't concerned about data loss, use the force delete method to rapidly remove the vault and all its dependencies.</span></span>

> <span data-ttu-id="7e914-108">PowerShell 명령은 자격 증명 모음의 모든 내용을 삭제하며 되돌릴 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-108">The PowerShell command deletes all the contents of the vault and is not reversible.</span></span>

## <a name="use-powershell-to-force-delete-the-vault"></a><span data-ttu-id="7e914-109">PowerShell을 사용하여 자격 증명 모음 강제 삭제</span><span class="sxs-lookup"><span data-stu-id="7e914-109">Use PowerShell to force delete the vault</span></span> 

<span data-ttu-id="7e914-110">보호된 항목이 있더라도 Site Recovery 자격 증명 모음을 삭제하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-110">To delete the Site Recovery vault even if there are protected items, use these commands:</span></span>

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="7e914-111">Site Recovery 자격 증명 모음 삭제</span><span class="sxs-lookup"><span data-stu-id="7e914-111">Delete a Site Recovery vault</span></span> 
<span data-ttu-id="7e914-112">자격 증명 모음을 삭제하려면 시나리오에 맞는 권장 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-112">To delete the vault, follow the recommended steps for your scenario.</span></span>

### <a name="vmware-vms-to-azure"></a><span data-ttu-id="7e914-113">VMware VM에서 Azure로</span><span class="sxs-lookup"><span data-stu-id="7e914-113">VMware VMs to Azure</span></span>

1. <span data-ttu-id="7e914-114">[VMware에 대한 보호 사용 안 함](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)의 단계에 따라 보호되는 VM을 모두 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-114">Delete all protected VMs by following the steps in [Disable protection for a VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="7e914-115">[복제 정책 삭제](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)의 단계에 따라 모든 복제 정책을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-115">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="7e914-116">[vCenter 삭제](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery)의 단계에 따라 vCenter에 대한 참조를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-116">Delete references to vCenter by following the steps in [Delete a vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span></span>

4. <span data-ttu-id="7e914-117">[구성 서버 서비스 해제](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server)의 단계에 따라 구성 서버를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-117">Delete the configuration server by following the steps in [Decommission a configuration server](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span></span>

5. <span data-ttu-id="7e914-118">자격 증명 모음을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-118">Delete the vault.</span></span>


### <a name="hyper-v-vms-with-virtual-machine-manager-to-azure"></a><span data-ttu-id="7e914-119">Hyper-V VM(Virtual Machine Manager 있음)에서 Azure로</span><span class="sxs-lookup"><span data-stu-id="7e914-119">Hyper-V VMs (with Virtual Machine Manager) to Azure</span></span>
1. <span data-ttu-id="7e914-120">[VMware VM 또는 물리적 서버에 대한 보호 사용 안 함](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)의 단계에 따라 보호되는 VM을 모두 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-120">Delete all protected VMs by following the steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="7e914-121">[복제 정책 삭제](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)의 단계에 따라 모든 복제 정책을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-121">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3.  <span data-ttu-id="7e914-122">[연결된 VMM 서버 등록 취소](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server)의 단계에 따라 Virtual Machine Manager 서버에 대한 참조를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-122">Delete references to Virtual Machine Manager servers by following the steps in [Unregister a connected VMM server](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span></span>

4.  <span data-ttu-id="7e914-123">자격 증명 모음을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-123">Delete the vault.</span></span>

### <a name="hyper-v-vms-without-virtual-machine-manager-to-azure"></a><span data-ttu-id="7e914-124">Hyper-V VM(Virtual Machine Manager 없음)에서 Azure로</span><span class="sxs-lookup"><span data-stu-id="7e914-124">Hyper-V VMs (without Virtual Machine Manager) to Azure</span></span>
1. <span data-ttu-id="7e914-125">[VMware VM 또는 물리적 서버에 대한 보호 사용 안 함](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)의 단계에 따라 보호되는 VM을 모두 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-125">Delete all protected VMs by following the steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="7e914-126">[복제 정책 삭제](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)의 단계에 따라 모든 복제 정책을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-126">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="7e914-127">[Hyper-V 호스트 등록 취소](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site)의 단계에 따라 Hyper-V 서버에 대한 참조를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-127">Delete references to Hyper-V servers by following the steps in [Unregister a Hyper-V host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span></span>

4. <span data-ttu-id="7e914-128">Hyper-V 사이트를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-128">Delete the Hyper-V site.</span></span>

5. <span data-ttu-id="7e914-129">자격 증명 모음을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e914-129">Delete the vault.</span></span>

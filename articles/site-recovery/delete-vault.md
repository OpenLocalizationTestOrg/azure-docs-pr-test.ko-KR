---
title: "사이트 복구 자격 증명 모음 aaaDelete"
description: "Toodelete는 Azure Site Recovery 자격 증명 모음에 따라 방법 hello Site Recovery 시나리오에 알아봅니다."
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
ms.openlocfilehash: 36db202d8b790bb5d31d1348fb72f51acb5d559c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="60c58-103">Site Recovery 자격 증명 모음 삭제</span><span class="sxs-lookup"><span data-stu-id="60c58-103">Delete a Site Recovery vault</span></span>
<span data-ttu-id="60c58-104">종속성으로 인해 Azure Site Recovery 자격 증명 모음을 삭제하지 못할 수 있으며,</span><span class="sxs-lookup"><span data-stu-id="60c58-104">Dependencies can prevent you from deleting an Azure Site Recovery vault.</span></span> <span data-ttu-id="60c58-105">hello tootake 해야 하는 작업에 따라 달라 집니다 hello Site Recovery 시나리오: VMware tooAzure (또는 System Center Virtual Machine Manager 없이) Hyper-v tooAzure 및 Azure 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-105">hello actions you need tootake vary based on hello Site Recovery scenario: VMware tooAzure, Hyper-V (with and without System Center Virtual Machine Manager) tooAzure, and Azure Backup.</span></span> <span data-ttu-id="60c58-106">Azure 백업에 사용 되는 자격 증명 모음 toodelete 참조 [Azure에서 백업 자격 증명 모음 삭제](../backup/backup-azure-delete-vault.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-106">toodelete a vault used in Azure Backup, see [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md).</span></span>

>[!Important]
><span data-ttu-id="60c58-107">Hello 제품을 테스트 하는 데이터 손실에 대해 고려 하지 않는 경우 사용 하 여 hello force delete 메서드 toorapidly hello 자격 증명 모음 및 모든 해당 종속성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-107">If you're testing hello product and aren't concerned about data loss, use hello force delete method toorapidly remove hello vault and all its dependencies.</span></span>

> <span data-ttu-id="60c58-108">PowerShell 명령 hello hello 자격 증명 모음의 hello 내용이 모두 삭제 되며 되돌릴 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-108">hello PowerShell command deletes all hello contents of hello vault and is not reversible.</span></span>

## <a name="use-powershell-tooforce-delete-hello-vault"></a><span data-ttu-id="60c58-109">사용 하 여 PowerShell tooforce hello 자격 증명 모음 삭제</span><span class="sxs-lookup"><span data-stu-id="60c58-109">Use PowerShell tooforce delete hello vault</span></span> 

<span data-ttu-id="60c58-110">경우에 사이트 복구 자격 증명 모음 toodelete hello 보호 되는 항목, 이러한 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-110">toodelete hello Site Recovery vault even if there are protected items, use these commands:</span></span>

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="60c58-111">Site Recovery 자격 증명 모음 삭제</span><span class="sxs-lookup"><span data-stu-id="60c58-111">Delete a Site Recovery vault</span></span> 
<span data-ttu-id="60c58-112">toodelete hello 자격 증명 모음에 따라 hello 권장 되는 시나리오에 대 한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-112">toodelete hello vault, follow hello recommended steps for your scenario.</span></span>

### <a name="vmware-vms-tooazure"></a><span data-ttu-id="60c58-113">VMware Vm tooAzure</span><span class="sxs-lookup"><span data-stu-id="60c58-113">VMware VMs tooAzure</span></span>

1. <span data-ttu-id="60c58-114">Hello 단계를 수행 하 여 보호 된 Vm을 삭제 모든 [VMware에 대 한 보호 사용 안 함](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-114">Delete all protected VMs by following hello steps in [Disable protection for a VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="60c58-115">Hello 단계를 수행 하 여 모든 복제 정책을 삭제 [복제 정책 삭제](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-115">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="60c58-116">단계를 다음 hello 여 toovCenter 참조 삭제 [vCenter 삭제](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery)합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-116">Delete references toovCenter by following hello steps in [Delete a vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span></span>

4. <span data-ttu-id="60c58-117">Hello 단계를 수행 하 여 hello 구성 서버를 삭제 [구성 서버의 중지](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server)합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-117">Delete hello configuration server by following hello steps in [Decommission a configuration server](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span></span>

5. <span data-ttu-id="60c58-118">Hello 자격 증명 모음을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-118">Delete hello vault.</span></span>


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a><span data-ttu-id="60c58-119">Hyper-v Vm (Virtual Machine Manager) tooAzure</span><span class="sxs-lookup"><span data-stu-id="60c58-119">Hyper-V VMs (with Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="60c58-120">Hello 단계를 수행 하 여 보호 된 Vm을 삭제 모든 [VMware VM 또는 실제 서버에 대 한 보호 사용 안 함](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-120">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="60c58-121">Hello 단계를 수행 하 여 모든 복제 정책을 삭제 [복제 정책 삭제](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-121">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3.  <span data-ttu-id="60c58-122">Hello 단계를 수행 하 여 tooVirtual Machine Manager 서버를 참조 하는 delete [VMM 서버 연결된의 등록을 취소](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server)합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-122">Delete references tooVirtual Machine Manager servers by following hello steps in [Unregister a connected VMM server](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span></span>

4.  <span data-ttu-id="60c58-123">Hello 자격 증명 모음을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-123">Delete hello vault.</span></span>

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a><span data-ttu-id="60c58-124">Hyper-v Vm (없이 가상 컴퓨터 관리자) tooAzure</span><span class="sxs-lookup"><span data-stu-id="60c58-124">Hyper-V VMs (without Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="60c58-125">Hello 단계를 수행 하 여 보호 된 Vm을 삭제 모든 [VMware VM 또는 실제 서버에 대 한 보호 사용 안 함](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-125">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="60c58-126">Hello 단계를 수행 하 여 모든 복제 정책을 삭제 [복제 정책 삭제](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-126">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="60c58-127">Hello 단계를 수행 하 여 tooHyper-V 서버를 참조 하는 delete [Hyper-v 호스트를 등록 취소](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site)합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-127">Delete references tooHyper-V servers by following hello steps in [Unregister a Hyper-V host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span></span>

4. <span data-ttu-id="60c58-128">Hello 하이퍼-V 사이트를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-128">Delete hello Hyper-V site.</span></span>

5. <span data-ttu-id="60c58-129">Hello 자격 증명 모음을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="60c58-129">Delete hello vault.</span></span>

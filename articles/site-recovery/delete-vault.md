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
# <a name="delete-a-site-recovery-vault"></a>Site Recovery 자격 증명 모음 삭제
종속성으로 인해 Azure Site Recovery 자격 증명 모음을 삭제하지 못할 수 있으며, hello tootake 해야 하는 작업에 따라 달라 집니다 hello Site Recovery 시나리오: VMware tooAzure (또는 System Center Virtual Machine Manager 없이) Hyper-v tooAzure 및 Azure 백업 합니다. Azure 백업에 사용 되는 자격 증명 모음 toodelete 참조 [Azure에서 백업 자격 증명 모음 삭제](../backup/backup-azure-delete-vault.md)합니다.

>[!Important]
>Hello 제품을 테스트 하는 데이터 손실에 대해 고려 하지 않는 경우 사용 하 여 hello force delete 메서드 toorapidly hello 자격 증명 모음 및 모든 해당 종속성을 제거 합니다.

> PowerShell 명령 hello hello 자격 증명 모음의 hello 내용이 모두 삭제 되며 되돌릴 수 없습니다.

## <a name="use-powershell-tooforce-delete-hello-vault"></a>사용 하 여 PowerShell tooforce hello 자격 증명 모음 삭제 

경우에 사이트 복구 자격 증명 모음 toodelete hello 보호 되는 항목, 이러한 명령을 사용 합니다.

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a>Site Recovery 자격 증명 모음 삭제 
toodelete hello 자격 증명 모음에 따라 hello 권장 되는 시나리오에 대 한 단계입니다.

### <a name="vmware-vms-tooazure"></a>VMware Vm tooAzure

1. Hello 단계를 수행 하 여 보호 된 Vm을 삭제 모든 [VMware에 대 한 보호 사용 안 함](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)합니다.

2. Hello 단계를 수행 하 여 모든 복제 정책을 삭제 [복제 정책 삭제](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)합니다.

3. 단계를 다음 hello 여 toovCenter 참조 삭제 [vCenter 삭제](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery)합니다.

4. Hello 단계를 수행 하 여 hello 구성 서버를 삭제 [구성 서버의 중지](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server)합니다.

5. Hello 자격 증명 모음을 삭제 합니다.


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a>Hyper-v Vm (Virtual Machine Manager) tooAzure
1. Hello 단계를 수행 하 여 보호 된 Vm을 삭제 모든 [VMware VM 또는 실제 서버에 대 한 보호 사용 안 함](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)합니다.

2. Hello 단계를 수행 하 여 모든 복제 정책을 삭제 [복제 정책 삭제](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)합니다.

3.  Hello 단계를 수행 하 여 tooVirtual Machine Manager 서버를 참조 하는 delete [VMM 서버 연결된의 등록을 취소](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server)합니다.

4.  Hello 자격 증명 모음을 삭제 합니다.

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a>Hyper-v Vm (없이 가상 컴퓨터 관리자) tooAzure
1. Hello 단계를 수행 하 여 보호 된 Vm을 삭제 모든 [VMware VM 또는 실제 서버에 대 한 보호 사용 안 함](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)합니다.

2. Hello 단계를 수행 하 여 모든 복제 정책을 삭제 [복제 정책 삭제](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)합니다.

3. Hello 단계를 수행 하 여 tooHyper-V 서버를 참조 하는 delete [Hyper-v 호스트를 등록 취소](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site)합니다.

4. Hello 하이퍼-V 사이트를 삭제 합니다.

5. Hello 자격 증명 모음을 삭제 합니다.

---
title: "Azure Backup으로 암호화된 VM 백업 및 복원"
description: "이 문서에서는 Azure Disk Encryption을 사용하여 암호화된 VM의 백업 및 복원 환경에 대해 설명합니다."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 8387f186-7d7b-400a-8fc3-88a85403ea63
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/27/2017
ms.author: pajosh;markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 89492cda8eff23509bee7693bb5f7e6ab5eb10d1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-back-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a>Azure Backup으로 암호화된 가상 컴퓨터를 백업 및 복원하는 방법
이 문서에서는 Azure Backup을 사용하여 가상 컴퓨터를 백업하고 복원하는 단계에 대해 설명합니다. 또한 지원되는 시나리오, 필수 조건 및 오류 사례에 대한 문제 해결 조치에 대한 자세한 정보도 제공합니다.

## <a name="supported-scenarios"></a>지원되는 시나리오
> [!NOTE]
> * 암호화된 VM의 백업 및 복원은 Resource Manager에서 배포한 가상 컴퓨터에 대해서만 지원됩니다. 클래식 가상 컴퓨터에서는 지원되지 않습니다. <br>
> * Azure Disk Encryption을 사용하는 Windows 및 Linux Virtual Machines 둘 다에 대해 지원됩니다. 이 암호화 방식은 Windows의 업계 표준 BitLocker 기능과 Linux의 DM 암호화 기능을 활용하여 디스크 암호화 기능을 제공합니다. <br>
> * BitLocker 암호화 키와 키 암호화 키를 모두 사용하여 암호화된 가상 컴퓨터에서만 지원됩니다. BitLocker 암호화 키만 사용하여 암호화된 가상 컴퓨터에서는 지원되지 않습니다. <br>
>
>

## <a name="prerequisites"></a>필수 조건
1. 가상 컴퓨터가 [Azure Disk Encryption](../security/azure-security-disk-encryption.md)을 사용하여 암호화되었습니다. 이 경우 BitLocker 암호화 키와 키 암호화 키를 모두 사용하여 암호화해야 합니다.
2. [백업 환경 준비](backup-azure-arm-vms-prepare.md)에서 언급한 단계를 사용하여 복구 서비스 자격 증명 모음이 만들어졌으며 저장소 복제가 설정되었습니다.
3. Azure Backup에는 암호화된 VM에 대한 키, 비밀을 포함한 [키 자격 증명 모음에 액세스할 수 있는 사용 권한](#provide-permissions-to-azure-backup)이 지정되었습니다.

## <a name="backup-encrypted-vm"></a>암호화된 VM 백업
다음 단계를 사용하여 백업 목표를 설정하고, 정책을 정의하며, 항목을 구성하고, 백업을 트리거합니다.

### <a name="configure-backup"></a>백업 구성
1. 이미 Recovery Services 자격 증명 모음이 열려 있으면 다음 단계로 진행합니다. 복구 서비스 자격 증명 모음이 열려 있지 않지만 Azure 포털에 있는 경우 허브 메뉴에서 **찾아보기**를 클릭합니다.

   * 리소스 목록에서 **복구 서비스**를 입력합니다.
   * 입력을 시작하면 입력한 내용을 바탕으로 목록이 필터링됩니다. **복구 서비스 자격 증명 모음**이 표시되면 클릭합니다.

      ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     복구 서비스 자격 증명 모음의 목록이 표시됩니다. 복구 서비스 자격 증명 모음의 목록에서 자격 증명 모음을 선택합니다.

     선택한 자격 증명 모음 대시보드가 열립니다.
2. 자격 증명 모음 아래쪽에 나타나는 항목 목록에서 **백업**을 클릭하여 [백업] 블레이드를 엽니다.

      ![백업 블레이드 열기](./media/backup-azure-vms-encryption/select-backup.png)
3. 백업 블레이드에서 **백업 목표** 를 클릭하여 백업 목표 블레이드를 엽니다.

      ![시나리오 블레이드 열기](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
4. [백업 목표] 블레이드에서 **워크로드 실행 위치**를 Azure로 설정하고 **백업할 항목**을 가상 컴퓨터로 설정한 다음 **확인**을 클릭합니다.

   백업 목표 블레이드가 닫히고 백업 정책 블레이드가 열립니다.

   ![시나리오 블레이드 열기](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
5. 백업 정책 블레이드에서 자격 증명 모음에 적용할 백업 정책을 선택하고 **확인**을 클릭합니다.

      ![백업 정책 선택](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    상세 정보에 기본 정책에 대한 자세한 내용이 나열됩니다. 정책을 만들려는 경우 드롭다운 메뉴에서 **새로 만들기** 를 선택합니다. **확인**을 클릭하면 백업 정책이 자격 증명 모음과 연결됩니다.

    다음으로 자격 증명 모음과 연결할 VM을 선택합니다.
6. 지정된 정책과 연결할 암호화된 가상 컴퓨터를 선택하고 **확인**을 클릭합니다.

      ![암호화된 VM 선택](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
7. 이 페이지에서는 선택한 암호화된 VM에 연결된 키 자격 증명 모음에 대한 메시지를 보여 줍니다. 백업 서비스를 사용하려면 키 자격 증명 모음의 키와 비밀에 대한 읽기 전용 액세스 권한이 있어야 합니다. 이 권한을 사용하여 연결된 VM과 함께 키와 암호를 백업합니다. **백업 서비스에 백업이 작동하도록 키 자격 증명 모음에 액세스하는 권한을 부여해야 합니다**. [아래 섹션에 설명된 단계](#provide-permissions-to-azure-backup)를 사용하여 이러한 사용 권한을 제공할 수 있습니다.

      ![암호화된 VM 메시지](./media/backup-azure-vms-encryption/encrypted-vm-warning-message.png)

      이제 자격 증명 모음의 모든 설정을 정의했으므로 [백업] 블레이드에서 페이지 아래쪽의 [백업 사용]을 클릭합니다. [백업 사용]은 정책을 자격 증명 모음 및 VM에 배포합니다.
8. 다음 준비 단계는 VM 에이전트를 설치하거나 VM 에이전트가 설치되었는지 확인하는 단계입니다. 이 작업을 수행하려면 [백업 환경 준비](backup-azure-arm-vms-prepare.md)에서 언급한 단계를 사용합니다.

### <a name="triggering-backup-job"></a>백업 작업 트리거
백업 작업을 트리거하려면 [복구 서비스 자격 증명 모음에 Azure VM 백업](backup-azure-arm-vms.md) 문서에서 언급한 단계를 사용합니다.

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a>암호화를 설정한 상태로 이미 백업한 VM의 백업 계속  
복구 서비스 자격 증명 모음에서 VM이 이미 백업되었으며 나중에 암호화가 설정된 경우 백업이 계속될 수 있게 백업 서비스에 Key Vault에 액세스할 수 있는 권한을 부여해야 합니다. [아래 섹션의 단계](#provide-permissions-to-azure-backup) 또는 [PowerShell 설명서](backup-azure-vms-automation.md)의 **백업 사용** 섹션에서 설명한 PowerShell 단계를 사용하여 이러한 사용 권한을 제공할 수 있습니다. 

## <a name="provide-permissions-to-azure-backup"></a>Azure Backup에 사용 권한 제공
키 자격 증명 모음에 액세스하고 암호화된 VM의 백업을 수행하기 위해 다음 단계를 사용하여 Azure Backup에 관련 사용 권한을 제공합니다.
1. **추가 서비스**를 선택하고 **키 자격 증명 모음**을 검색합니다.

    ![키 자격 증명 모음 검색](./media/backup-azure-vms-encryption/search-key-vault.png)
    
2. 키 자격 증명 모음 목록에서 백업해야 하는 암호화된 VM에 관련된 키 자격 증명 모음을 선택합니다.

     ![키 자격 증명 모음 선택](./media/backup-azure-vms-encryption/select-key-vault.png)
     
3. **액세스 정책** 및 **새로 추가**를 차례로 클릭합니다.

    ![액세스 정책 추가](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)
    
4. **보안 주체 선택**을 클릭하고 검색 창에서 **백업 관리 서비스**를 입력합니다. 

    ![백업 서비스 검색](./media/backup-azure-vms-encryption/search-backup-service.png)
    
5. **백업 관리 서비스**를 선택하고 선택 단추를 클릭합니다.

    ![백업 서비스 선택](./media/backup-azure-vms-encryption/select-backup-service.png)
    
6. 템플릿 드롭다운의 구성에서 **Azure Backup**을 선택합니다. 키 사용 권한 및 비밀 사용 권한 드롭다운에서 필요한 권한을 미리 채웁니다. 

    ![Azure Backup 선택](./media/backup-azure-vms-encryption/select-backup-template.png)
    
7. **확인**을 클릭합니다. Backup Management Service를 액세스 정책 블레이드에서 추가했는지 확인합니다. 

    ![서비스 액세스 정책 백업](./media/backup-azure-vms-encryption/backup-service-access-policy.png)
    
8. **Save**를 클릭합니다. 이렇게 하면 Azure Backup에 필요한 사용 권한이 제공됩니다.

    ![서비스 액세스 정책 백업](./media/backup-azure-vms-encryption/save-access-policy.png)

사용 권한이 성공적으로 주어지면 암호화된 VM에 백업을 사용하도록 진행할 수 있습니다.

## <a name="restore-encrypted-vm"></a>암호화된 VM 복원
암호화된 VM을 복원하려면 먼저 [VM 복원 구성 선택](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration)의 **백업된 디스크 복원** 섹션에 제공된 단계에 따라 디스크를 복원합니다. 그런 후에 다음 옵션 중 하나를 사용할 수 있습니다.
* [복원된 디스크에서 VM 만들기](backup-azure-vms-automation.md#create-a-vm-from-restored-disks)에 설명된 PowerShell 단계를 사용하여 복원된 디스크에서 전체 VM을 만듭니다.
* 또는 [디스크 복원의 일부로 생성된 템플릿을 사용](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm)하여 복원된 디스크에서 VM을 만듭니다. 템플릿은 2017년 4월 26일 이후에 만들어진 복원 지점에 대해서만 사용할 수 있습니다.

## <a name="troubleshooting-errors"></a>문제 해결 오류
| 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| 백업 |가상 컴퓨터가 BEK만으로 암호화되었기 때문에 유효성 검사에 실패했습니다. BEK와 KEK 모두로 암호화된 가상 컴퓨터에서만 백업을 사용할 수 있습니다. |가상 컴퓨터는 BEK와 KEK를 사용하여 암호화해야 합니다. 먼저 VM의 암호를 해독하고 BEK와 KEK를 사용하여 암호화합니다. VM이 BEK와 KEK를 사용하여 암호화되면 백업을 사용하도록 설정합니다. [VM 암호 해독 및 암호화](../security/azure-security-disk-encryption.md)에 대한 자세한 정보  |
| 복원 |이 VM과 연결된 키 자격 증명 모음이 없기 때문에 이 암호화된 VM을 복원할 수 없습니다. |키 자격 증명 모음을 만들려면 [Azure Key Vault 시작](../key-vault/key-vault-get-started.md)을 사용합니다. 키와 비밀이 없는 경우 이를 복원하려면 [Azure Backup으로 키 자격 증명 모음 키 및 비밀 복원](backup-azure-restore-key-secret.md)(영문) 문서를 사용합니다. |
| 복원 |이 VM과 연결된 키와 비밀이 없기 때문에 이 암호화된 VM을 복원할 수 없습니다. |키와 비밀이 없는 경우 이를 복원하려면 [Azure Backup으로 키 자격 증명 모음 키 및 비밀 복원](backup-azure-restore-key-secret.md)(영문) 문서를 사용합니다. |
| 복원 |백업 서비스는 구독의 리소스에 액세스할 수 있는 권한이 없습니다. |위에서 설명된 것처럼 먼저 [VM 복원 구성 선택](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration)의 **백업된 디스크 복원** 섹션에 제공된 단계에 따라 디스크를 복원합니다. 그런 후에 PowerShell을 사용하여 [복원된 디스크에서 VM을 만듭니다](backup-azure-vms-automation.md#create-a-vm-from-restored-disks). |
|백업 | Azure Backup 서비스에는 암호화된 가상 컴퓨터의 백업을 위한 Key Vault에 대해 충분한 권한이 없습니다. | 이 경우 가상 시스템을 BitLocker 암호화 키와 키 암호화 키를 모두 사용하여 암호화해야 합니다. 그런 후에 백업을 사용하도록 설정해야 합니다.  백업 서비스는 [위의 섹션에서 언급한 단계](#provide-permissions-to-azure-backup) 또는 [AzureRM.RecoveryServices.Backup cmdlet을 사용하여 가상 컴퓨터 백업](backup-azure-vms-automation.md#back-up-azure-vms)에서 PowerShell 설명서의 **보호 사용** 섹션에서 언급한 PowerShell 단계를 사용하여 이러한 사용 권한을 제공받아야 합니다. |  

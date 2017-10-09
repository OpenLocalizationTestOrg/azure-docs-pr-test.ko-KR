---
title: "디스크 암호화 문제 해결 aaaAzure | Microsoft Docs"
description: "이 문서에서는 Windows 및 Linux IaaS VM용 Microsoft Azure Disk Encryption에 대한 문제 해결 팁을 제공합니다."
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: ce0e23bd-07eb-43af-a56c-aa1a73bdb747
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: devtiw
ms.openlocfilehash: 2ecb8df1fb869e3bf8f3be4be4494e6485e75695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-troubleshooting-guide"></a>Azure Disk Encryption 문제 해결

이 가이드는 정보 정보 기술 (IT) 전문가 위한 보안 분석가 및 관련 문제를 클라우드 관리자 인 Azure 디스크 암호화를 사용 하는 조직과 지침 tootroubleshoot 디스크 암호화가 필요 합니다.

## <a name="troubleshooting-linux-os-disk-encryption"></a>Linux OS 디스크 암호화 문제 해결

Linux 운영 체제 디스크 암호화 hello 운영 체제 드라이브 이전 toorunning 탑재 해제 해야 hello 전체 디스크 암호화 프로세스를 통해 합니다.   불가능 한 경우, 오류 메시지의 "실패 후 toounmount..." 오류 메시지는 가능성이 toooccur입니다.

이는 지원되는 재고 갤러리 이미지에서 수정되거나 변경된 대상 VM 환경에서 OS 디스크 암호화를 시도할 때 발생합니다.  Hello 확장의 기능 toounmount hello 운영 체제 드라이브와 충돌할 수 있는 지원 되는 hello 이미지에서 편차의 예입니다.
- 지원되는 파일 시스템 및/또는 파티션 구성표와 더 이상 일치하지 않는 사용자 지정 이미지
- 예: 바이러스 백신 응용 프로그램, Docker, SAP, MongoDB, 또는 Apache Cassandra hello OS 이전 tooencryption에서 실행을 사용 하 여 사용자 지정 된 이미지입니다.  이러한 응용 프로그램은 어려운 tooterminate 하 고 열려 있는 파일 핸들 toohello 운영 체제 드라이브, 유지 hello 드라이브를 탑재 되지 않은 오류를 발생 시키는 일 수 없습니다.
- 실행 되는 사용자 지정 스크립트 근접 toohello 암호화 단계 충돌할 수 있으며이 오류가 발생 하는 시간을 닫습니다. 이 사용자 지정 스크립트 확장 또는 기타 작업이 실행 될 때 동시에 toodisk 암호화 또는 리소스 관리자 템플릿 동시에 여러 확장 tooexecute를 정의 하는 경우에 발생할 수 있습니다.   직렬화 하는 작업 및 이러한 단계를 분리 hello 문제를 해결할 수 있습니다.
- SELinux 사용할 수 없는 이전 tooenabling 암호화 되지 않았으면 hello 단계 실패를 분리 합니다.  암호화가 완료되면 SELinux를 다시 활성화할 수 있습니다.
- Hello OS 디스크 LVM 체계 사용 하는 경우 (제한 된 LVM 데이터 디스크 지원을 사용할 수 있는 경우에 LVM OS 디스크는 아님)
- 최소 메모리 요구 사항이 충족되지 않는 경우 - OS 디스크 암호화에 권장되는 메모리 크기는 7GB입니다.
- 데이터 드라이브가 /mnt/ 디렉터리 또는 다른 디렉터리(예: /mnt/data1, /mnt/data2, /data3 + /data3/data4 등) 아래에 재귀적으로 탑재된 경우
- Linux에 대한 다른 Azure Disk Encryption [필수 구성 요소](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)가 충족되지 않은 경우

## <a name="unable-tooencrypt"></a>Tooencrypt 수 없습니다.

경우에 따라 hello Linux 디스크 암호화 toobe "OS 디스크 암호화 시작"에서 중단 하 고 SSH를 비활성화 나타납니다. 이 프로세스는 주식 갤러리 이미지에 3-16 시간 toocomplete 간의 걸릴 수 있습니다.  다중 TB 크기 데이터 디스크 추가 되 면 hello 프로세스 일 걸릴 수 있습니다. hello Linux 운영 체제 디스크 암호화 시퀀스 일시적으로 hello 운영 체제 드라이브를 탑재 해제 하 고 암호화 된 상태에서 다시 탑재 하기 전에 hello 전체 운영 체제 디스크의 블록 단위로 암호화를 수행 합니다.   Windows Azure 디스크 암호화를와 달리 Linux 디스크 암호화 허용 하지 않습니다 hello VM의 동시 사용 hello 암호화가 진행 중인 동안.  hello hello 디스크와 표준 또는 프리미엄 (SSD) 저장소 hello 저장소 계정 기반한 여부의 hello 크기를 포함 한 VM의 성능 특성 hello hello 필요한 시간 toocomplete 암호화 하는 데 상당한 영향을 수 있습니다.

toocheck 상태 hello에서 반환 된 hello ProgressMessage 필드 [Get AzureRmVmDiskEncryptionStatus](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) 명령을 폴링할 수 있습니다.   Hello 운영 체제 드라이브를 암호화 하는 hello VM 서비스 상태가 하 고 SSH 비활성화 tooprevent 이기도 모든 중단 toohello 지속적인 프로세스입니다.  진행 중, 아래에 몇 시간이 나중 toorestart hello VM는 VMRestartPending 메시지가 암호화 하는 동안 EncryptionInProgress hello 시간의 hello 대부분에 대 한 보고 됩니다.  예:


```
PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : EncryptionInProgress
DataVolumesEncrypted       : EncryptionInProgress
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk encryption started

PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : VMRestartPending
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk successfully encrypted, please reboot hello VM
```

한 번 tooreboot hello VM을 묻는 메시지가 표시 하 고 hello VM을 다시 시작 하 고 2-3 분 hello 다시 부팅 하 고 hello 대상에서 수행 하는 마지막 단계는 toobe 제공, 후 hello 상태 메시지가 암호화는 완료 된 마지막으로 표시 됩니다.   이 메시지를 사용할 수 있는 암호화 된 hello 운영 체제 드라이브가 사용 하기 위해 수행 하 고 사용 가능한 hello VM toobe에 대 한 예상된 toobe 다시 있습니다.

경우에이 시퀀스를 찾을 수 없습니다 또는 부팅 정보, 진행률 메시지 또는 기타 오류 지표 보고서 (예:이 가이드에 설명 된 hello "toounmount 실패 했습니다." 오류가 표시 되는 경우)이이 프로세스의 hello 가운데에 운영 체제 암호화에 실패 했음을 toorestore hello VM 백 toohello 스냅숏 또는 즉시 이전 tooencryption 수행 된 백업 것이 좋습니다.  이전 toohello 다음 시도 제안 된 toore-hello VM의 hello 특징을 평가 하 고 모든 필수 조건이 충족 확인 합니다.

## <a name="troubleshooting-azure-disk-encryption-behind-a-firewall"></a>방화벽 뒤에 있는 Azure Disk Encryption 문제 해결
때 연결이 필요한 작업 중단 수 hello 확장 tooperform의 방화벽, 프록시 요구 사항 또는 네트워크 보안 그룹 (NSG) 설정 hello 능력에 의해 제한 됩니다.   상태 메시지 "hello VM에서 사용할 수 없는 확장 상태" 등이 될 수 있습니다 및 예상된 시나리오가 toofinish 실패 합니다.  이어지는 hello 섹션에 몇 가지 일반적인 방화벽 문제를 조사할 수 있습니다.

### <a name="network-security-groups"></a>네트워크 보안 그룹
적용 된 모든 네트워크 보안 그룹 설정은 hello 끝점 toomeet 문서화 hello 네트워크 구성 허용 여전히 해야 [필수 구성 요소](https://docs.microsoft.com/azure/security/azure-security-disk-encryption#prerequisites) 디스크 암호화에 대 한 합니다.

### <a name="azure-keyvault-behind-firewall"></a>방화벽 뒤에 있는 Azure Key Vault
hello VM 수 tooaccess 키 자격 증명 모음 이어야 합니다. Hello로 유지 관리 되는 방화벽 뒤에서 액세스 tookey 오류에서 tooguidance 참조 [키 자격 증명 모음](https://docs.microsoft.com/azure/key-vault/key-vault-access-behind-firewall) 팀입니다.

### <a name="linux-package-management-behind-firewall"></a>방화벽 뒤에 있는 Linux 패키지 관리
Linux 용 Azure 디스크 암호화는 런타임 시 hello 대상 배포 패키지 관리 시스템 tooinstall 필요한 필수 구성 요소 이전 tooenabling 암호화에 의존합니다.  Hello VM toodownload 수 없도록 방지 하 고 이러한 구성 요소를 설치 하는 방화벽 설정, 다른 연결이 실패 예상 됩니다.    hello 단계 tooconfigure 분배 하 여 다를 수 있습니다.  Red Hat에서 프록시가 필요한 경우에는 subscription-manager와 yum이 올바르게 설정되었는지 확인해야 합니다.  이 항목은 [여기](https://access.redhat.com/solutions/189533)에 있는 Red Hat 지원 문서를 참조하세요.  

## <a name="troubleshooting-windows-server-2016-server-core"></a>Windows Server 2016 Server Core 문제 해결

Windows Server 2016 Server Core에서 hello bdehdcfg 구성 요소가 기본적으로 사용할 수 없습니다. 이 구성 요소는 Azure Disk Encryption에 필요합니다.

tooworkaround이 문제점, hello Server Core 이미지의 Windows Server 2016 데이터 센터 VM toohello c:\windows\system32 폴더에서 다음 4 파일이 복사 hello:

```
bdehdcfg.exe
bdehdcfglib.dll
bdehdcfglib.dll.mui
bdehdcfg.exe.mui
```

Hello 다음 명령을 실행 합니다.

```
bdehdcfg.exe -target default
```

550MB 시스템 파티션을 만들어집니다 고 다시 부팅 한 후 수 있습니다 Diskpart toocheck hello 볼륨을 사용 하 여 계속 합니다.  

예:

```
DISKPART> list vol

  Volume ###  Ltr  Label        Fs     Type        Size     Status     Info
  ----------  ---  -----------  -----  ----------  -------  ---------  --------
  Volume 0     C                NTFS   Partition    126 GB  Healthy    Boot
  Volume 1                      NTFS   Partition    550 MB  Healthy    System
  Volume 2     D   Temporary S  NTFS   Partition     13 GB  Healthy    Pagefile
```
## <a name="see-also"></a>참고 항목
이 문서에서 배운 Azure 디스크 암호화에서는 몇 가지 일반적인 문제에 대 한 자세한 방법과 tootroubleshoot 합니다. 이 서비스 및 기능에 대한 자세한 내용은 다음을 참조하세요.

- [Azure Security Center에서 디스크 암호화 적용](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Azure 가상 컴퓨터 암호화](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Azure 미사용 데이터 암호화](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)

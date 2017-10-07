---
title: "Windows 및 Linux IaaS Vm에 대 한 디스크 암호화 aaaAzure | Microsoft Docs"
description: "이 문서에서는 Windows 및 Linux IaaS VM용 Microsoft Azure Disk Encryption에 대한 개요를 제공합니다."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a>Windows 및 Linux IaaS VM용 Azure 디스크 암호화
Microsoft Azure는 강력 하 게 커밋된 tooensuring 데이터 개인 정보를 데이터 sovereignty 및 toocontrol Azure 호스트를 사용 하면 다양 한 고급 기술 tooencrypt 통해 데이터를 제어 하 고 암호화 키를 관리할 데이터의 액세스 제어 및 감사 합니다. 이 Azure 고객 hello 유연성 toochoose hello 솔루션을 제공 비즈니스 요구에 가장 적합 합니다. 이 문서에 소개 tooa 새로운 기술 솔루션 "Windows 및 Linux IaaS VM에 대 한 Azure 디스크 암호화" toohelp 보호 하 고 데이터 toomeet 조직 보안 및 규정 준수 행 결과 보호 합니다. hello 용지 hello를 비롯 한 toouse hello Azure 디스크 암호화 기능 시나리오 및 hello 사용자 환경을 원하는 하는 방법에 자세한 지침을 제공 합니다.

> [!NOTE]
> 특정 권장 사항으로 인해 데이터, 네트워크 또는 계산 리소스 사용량이 증가할 수 있으며 이로 인해 라이선스 또는 구독 비용이 발생합니다.

## <a name="overview"></a>개요
Azure Disk Encryption은 Windows 및 Linux IaaS 가상 컴퓨터 디스크를 암호화할 수 있도록 하는 새로운 기능입니다. Azure 디스크 암호화 활용 hello 업계 표준 [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) 창과 hello의 기능 [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) hello OS 및 hello 데이터 디스크에 대 한 Linux tooprovide 볼륨 암호화의 기능입니다. 와 통합 된 hello 솔루션 [Azure 키 자격 증명 모음](https://azure.microsoft.com/documentation/services/key-vault/) toohelp 제어 및 주요 자격 증명 모음 구독에서 hello 디스크 암호화 키 및 암호를 관리 합니다. hello 솔루션 하면 hello 가상 컴퓨터 디스크에 있는 모든 데이터가 Azure 저장소에 저장 된 상태의 암호화 됩니다.

Windows 및 Linux IaaS VM용 Azure Disk Encryption은 이제 Standard VM 및 Premium Storage를 사용하는 VM을 위한 모든 Azure 공용 지역 및 AzureGov 지역에서 **일반 공급**으로 제공됩니다.

### <a name="encryption-scenarios"></a>암호화 시나리오
hello Azure 디스크 암호화 솔루션에서는 hello 다음 고객 시나리오를 지원 합니다.

* 미리 암호화된 VHD 및 암호화 키에서 만든 새 IaaS VM에서 암호화 사용
* 지원 되는 hello Azure 갤러리 이미지에서 만든 새 IaaS Vm에 대 한 암호화를 사용 하도록 설정
* Azure에서 실행 중인 기존 IaaS VM에 대해 암호화 사용
* Windows IaaS VM에서 암호화 사용 안 함
* Linux IaaS VM에 대한 데이터 드라이브에서 암호화 사용 안 함
* 관리 디스크 VM의 암호화 사용
* 기존의 암호화된 Premium Storage 이외 VM의 암호화 설정 업데이트
* 키 암호화 키를 사용하여 암호화된 VM의 백업 및 복원

hello 솔루션 hello Microsoft Azure에서 설정 된 경우 IaaS Vm에 대 한 다음 시나리오를 지원 합니다.

* Azure Key Vault와 통합
* 표준 계층 VM: [A, D, DS, G, GS, F 등 시리즈 IaaS VM](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Windows 및 Linux IaaS Vm 및 hello에서 관리 되는 디스크 Vm에서 사용 암호화 Azure 갤러리 이미지를 지원합니다.
* Windows IaaS VM 및 관리 디스크 VM에 대한 OS 및 데이터 드라이브에서 암호화 사용 안 함
* Linux IaaS VM 및 관리 디스크 VM에 대한 데이터 드라이브에서 암호화 사용 안 함
* Windows 클라이언트 OS를 실행하는 IaaS VM에서 암호화 사용
* 탑재 경로가 있는 볼륨에서 암호화 사용
* mdadm을 사용하여 디스크 스트라이프(RAID)로 구성된 Linux VM에서 암호화 사용
* 데이터 디스크에 대해 LVM을 사용하여 Linux VM에서 암호화 사용
* Storage 공간으로 구성된 Windows VM에서 암호화 사용
* 기존의 암호화된 Premium Storage 이외 VM의 암호화 설정 업데이트
* 모든 Azure 공용 지역 및 AzureGov 지역 지원됨

hello 솔루션 시나리오, 기능 및 기술에 따라 hello를 지원 하지 않습니다.

* 기본 계층 IaaS VM
* Linux IaaS VM에 대한 OS 드라이브에서 암호화 사용 안 함
* 운영 체제 드라이브 hello Linux Iaas Vm에 대 한 암호화 된 경우 데이터 드라이브에 대 한 암호화를 사용 하지 않도록 설정
* Hello 클래식 VM 만들기 방법을 사용 하 여 만들어진 IaaS Vm
* Windows 및 Linux IaaS VM 고객 사용자 지정 이미지에 암호화를 사용하는 기능은 지원되지 않습니다. Linux LVM OS 디스크에 암호화를 사용하는 기능은 현재 지원되지 않습니다. 이 지원은 곧 제공될 예정입니다.
* 온-프레미스 키 관리 서비스와의 통합
* Azure 파일(공유 파일 시스템), NFS(네트워크 파일 시스템), 동적 볼륨, 소프트웨어 기반 RAID 시스템으로 구성된 Windows VM
* 키 암호화 키를 사용하지 않고 암호화된 VM의 백업 및 복원입니다.
* 기존의 암호화된 Premium Storage VM의 암호화 설정을 업데이트합니다.

> [!NOTE]
> 암호화 된 Vm의 백업 및 복원 hello KEK 구성을 사용 하 여 암호화 된 Vm에 대해서만 지원 됩니다. KEK 없이 암호화된 VM에서는 지원되지 않습니다. KEK는 VM 암호화를 사용하도록 설정하는 선택적 매개 변수입니다. 곧 지원될 예정입니다.
> 기존의 암호화된 Premium Storage VM의 암호화 설정 업데이트는 지원되지 않습니다. 곧 지원될 예정입니다.

### <a name="encryption-features"></a>암호화 기능
를 사용 하도록 설정 및 Azure IaaS Vm에 대 한 Azure 디스크 암호화 배포 hello 다음과 같은 기능이 활성화 되어 제공 하는 hello 구성에 따라:

* 저장소에 저장 된 상태의 hello OS 볼륨 tooprotect hello 부팅 볼륨의 암호화
* 저장소에 있는 미사용 데이터 볼륨 tooprotect hello 데이터 볼륨 암호화
* Windows IaaS Vm에 대 한 드라이브 hello OS 및 데이터에 대 한 암호화를 사용 하지 않도록 설정
* (경우에 운영 체제 드라이브 IS NOT 암호화) Linux IaaS Vm에 대 한 드라이브 hello 데이터에 암호화를 사용 하지 않도록 설정
* Hello 암호화 키 및 키 자격 증명 모음 구독에 암호 보호
* 암호화 된 IaaS VM의 hello hello 암호화 상태를 보고 합니다.
* Hello IaaS 가상 컴퓨터에서 디스크 암호화 구성 설정 제거
* Hello Azure 백업 서비스를 사용 하 여 암호화 된 Vm의 백업 및 복원

> [!NOTE]
> 암호화 된 Vm의 백업 및 복원 hello KEK 구성을 사용 하 여 암호화 된 Vm에 대해서만 지원 됩니다. KEK 없이 암호화된 VM에서는 지원되지 않습니다. KEK는 VM 암호화를 사용하도록 설정하는 선택적 매개 변수입니다.

Windows 및 Linux 솔루션용 IaaS VM에 대한 Azure Disk Encryption에는 다음 내용이 포함됩니다.

* Windows 용 hello 디스크 암호화 확장입니다.
* Linux 용 hello 디스크 암호화 확장 합니다.
* hello 디스크 암호화 PowerShell cmdlet입니다.
* 디스크 암호화 Azure CLI (명령줄 인터페이스) cmdlet hello 합니다.
* hello 디스크 암호화 Azure 리소스 관리자 템플릿을 합니다.

hello Azure 디스크 암호화 솔루션은 Windows 또는 Linux 운영 체제를 실행 중인 IaaS Vm에서 지원 됩니다. Hello 지원 운영 체제에 대 한 자세한 내용은 참조 hello "전제 조건" 섹션.

> [!NOTE]
> Azure Disk Encryption으로 VM 디스크를 암호화하는 작업에 대한 추가 요금은 없습니다.

### <a name="value-proposition"></a>가치 제안
Hello Azure 디스크 암호화 관리 솔루션에 적용할 때는 hello 다음 비즈니스 요구를 충족 시킬 수 있습니다.

* 업계 표준 암호화 기술을 tooaddress 조직 보안 및 규정 준수 요구 사항을 사용할 수 있으므로 IaaS Vm은 미사용 보안이 유지 됩니다.
* IaaS VM은 고객이 제어하는 키 및 정책에 따라 부팅되며 Key Vault에서 이러한 사용을 감사할 수 있습니다.

### <a name="encryption-workflow"></a>암호화 워크플로
Windows 및 Linux Vm에 대 한 디스크 암호화 tooenable 다음 hello지 않습니다.

1. 암호화 시나리오 hello 앞에 암호화 시나리오 중에서 선택 합니다.
2. Hello Azure 디스크 암호화 리소스 관리자 템플릿, PowerShell cmdlet 또는 CLI 명령을 통해 tooenabling 디스크 암호화에서 선택한 hello 암호화 구성을 지정 합니다.

   * Hello 고객 암호화 VHD 시나리오에 대 한 암호화 hello VHD tooyour 저장소 계정 및 hello 암호화 키 재료 tooyour 키 자격 증명 모음을 업로드 합니다. 그런 다음 새 IaaS VM에 hello 암호화 구성 tooenable 암호화를 제공 합니다.
   * Hello 시장에서에서 생성 된 새 Vm 및 Azure에서 이미 실행 중인 기존 Vm에 대 한 hello IaaS VM에 hello 암호화 구성 tooenable 암호화를 제공 합니다.

3. 권한 부여 액세스 toohello Azure 플랫폼 tooread hello 암호화 키 (Windows 시스템에 대 한 BitLocker 암호화 키) 및 Linux에 대 한 암호의에서 자료 hello IaaS VM에 키 자격 증명 모음 tooenable 암호화 합니다.

4. Hello Azure Active Directory (Azure AD) 응용 프로그램 identity toowrite hello 암호화 키 재료 tooyour 키 자격 증명 모음을 제공 합니다. 이렇게 하면 특정 2 단계에서 언급 한 hello 시나리오에 대 한 hello IaaS VM에 대 한 암호화 합니다.

5. Azure는 암호화와 hello 주요 자격 증명 모음 구성을 hello VM 서비스 모델을 업데이트 하 고 암호화 된 VM을 설정 합니다.

 ![Azure의 Microsoft 맬웨어 방지](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a>암호 해독 워크플로
IaaS vm의 경우 높은 수준의 단계를 수행 하는 전체 hello toodisable 디스크 암호화:

1. Hello Azure 디스크 암호화 리소스 관리자 템플릿 또는 PowerShell cmdlet을 통해 Azure에서 실행 중인 IaaS VM에 toodisable 암호화 (해독)를 선택 하 고 hello 암호 해독 구성을 지정 합니다.

 이 단계는 hello OS 또는 hello 데이터 볼륨에 또는 둘 다 Windows IaaS VM을 실행 하는 hello의 암호화를 해제 합니다. 그러나 hello 이전 섹션에서 설명 했 듯이 Linux에 대 한 OS 디스크 암호화를 해제 하면 지원 되지 않습니다. hello 암호 해독 단계 hello OS 디스크 암호화 되지 않은 상태로 Linux Vm에서 데이터 드라이브에만 허용 됩니다.
2. Azure 업데이트 hello VM 서비스 모델 및 hello IaaS VM을 암호 해독 된 표시 됩니다. hello VM의 hello 콘텐츠는 더 이상 휴지 암호화 됩니다.

> [!NOTE]
> hello 암호화 사용 안 함 작업이 경우 키 자격 증명 모음 및 hello 암호화 키 자료 (Windows 시스템에 대 한 BitLocker 암호화 키) 또는 Linux에 대 한 암호를 삭제 하지 않습니다.
 > Linux OS 디스크 암호화는 사용하지 않도록 설정할 수 없습니다. hello 암호 해독 단계 Linux Vm에서 데이터 드라이브에만 허용 됩니다.
Linux 용 데이터 디스크 암호화를 해제 하면 hello 운영 체제 드라이브를 암호화 하는 경우 지원 되지 않습니다.

## <a name="prerequisites"></a>필수 조건
Hello "개요" 섹션에서에서 설명한 hello 지원 시나리오에 대 한 Azure IaaS Vm에 Azure 디스크 암호화를 사용 하기 전에 hello 다음 필수 구성 요소를 참조 하세요.

* 유효한 활성 Azure 구독 toocreate 리소스 hello 지원 영역에 Azure에 있어야 합니다.
* Azure 디스크 암호화는 hello 다음 Windows Server 버전에서 지원: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 및 Windows Server 2016 합니다.
* Azure 디스크 암호화는 hello 다음 Windows 클라이언트 버전에서 지원: Windows 8 클라이언트 및 Windows 10 클라이언트입니다.

> [!NOTE]
> Windows Server 2008 R2의 경우 Azure에서 암호화를 사용하도록 설정하기 전에 .NET Framework 4.5를 설치해야 합니다. Windows Server 2008 R2 x64 기반 시스템에 대 한 Microsoft.NET Framework 4.5.2 hello 선택적 업데이트를 설치 하 여 Windows 업데이트에서 설치할 수 있습니다 ([KB2901983](https://support.microsoft.com/kb/2901983)).

* Azure 디스크 암호화가 지원 hello Azure 갤러리의 다음 기반으로 Linux 서버 배포 및 버전:

| Linux 배포 | 버전 | 암호화에 지원되는 볼륨 유형|
| --- | --- |--- |
| Ubuntu | 16.04-DAILY-LTS | OS 및 데이터 디스크 |
| Ubuntu | 14.04.5-DAILY-LTS | OS 및 데이터 디스크 |
| Ubuntu | 12.10 | 데이터 디스크  |
| Ubuntu | 12.04 | 데이터 디스크  |
| RHEL | 7.3 | OS 및 데이터 디스크 |
| RHEL | 7.2 | OS 및 데이터 디스크 |
| RHEL | 6.8 | OS 및 데이터 디스크 |
| RHEL | 6.7 | 데이터 디스크  |
| CentOS | 7.3 | OS 및 데이터 디스크 |
| CentOS | 7.2n | OS 및 데이터 디스크 |
| CentOS | 6.8 | OS 및 데이터 디스크 |
| CentOS | 7.1 | 데이터 디스크  |
| CentOS | 7.0 | 데이터 디스크  |
| CentOS | 6.7 | 데이터 디스크  |
| CentOS | 6.6 | 데이터 디스크  |
| CentOS | 6.5 | 데이터 디스크  |
| openSUSE | 13.2 | 데이터 디스크  |
| SLES | 12 SP1 | 데이터 디스크  |
| SLES | 12-SP1(Premium) | 데이터 디스크  |
| SLES | HPC 12 | 데이터 디스크  |
| SLES | 11-SP4(Premium) | 데이터 디스크  |
| SLES | 11 SP4 | 데이터 디스크  |

* Azure 디스크 암호화를 사용 하려면 키 자격 증명 모음 및 Vm에에서 상주 하는 hello 동일한 Azure 지역 및 구독 합니다.

> [!NOTE]
> 개별 영역에서 hello 리소스 구성 hello Azure 디스크 암호화 기능을 사용 하면 오류가 발생 합니다.

* tooset 위로 및 Azure 디스크 암호화에 대 한 주요 자격 증명 모음 구성 섹션을 참조 하십시오 **설정 및 Azure 디스크 암호화에 대 한 주요 자격 증명 모음 구성** hello에 *필수 구성 요소* 이 문서의 섹션.
* tooset 및 Azure 디스크 암호화에 대 한 Azure Active directory에서 Azure AD 응용 프로그램을 구성 하십시오 섹션을 참조 **hello Azure AD 응용 프로그램을 Azure Active Directory에서** hello에 *필수 구성 요소* 이 문서의 섹션입니다.
* tooset hello Azure AD 응용 프로그램에 대 한 hello 주요 자격 증명 모음 액세스 정책 구성 및 하십시오 섹션을 참조 **hello Azure AD 응용 프로그램에 대 한 hello 주요 자격 증명 모음 액세스 정책을 설정** hello에 *필수 구성 요소* 의 섹션 이 문서입니다.
* 미리 암호화 된 Windows VHD tooprepare 섹션을 참조 하세요. **미리 암호화 된 Windows VHD를 준비** hello에 *부록*합니다.
* 미리 암호화 된 Linux VHD tooprepare 섹션을 참조 하세요. **미리 암호화 된 Linux VHD 준비** hello에 *부록*합니다.
* hello Azure 플랫폼 있어야 액세스 toohello 암호화 키 또는 키 자격 증명 모음 toomake의 암호에 사용할 수 있는 toohello 가상 컴퓨터를 부팅 하 고 hello 가상 컴퓨터 운영 체제 볼륨 암호를 해독 합니다. toogrant 권한 tooAzure 플랫폼 집합 hello **EnabledForDiskEncryption** hello 키 자격 증명 모음에는 속성입니다. 자세한 내용은 참조 **설정 및 Azure 디스크 암호화에 대 한 주요 자격 증명 모음 구성** hello 부록에에서 있습니다.
* Key Vault 비밀 및 KEK URL 버전을 지정해야 합니다. Azure에서 이 버전 관리 제한을 적용합니다. 유효한 암호 및 KEK Url에 대 한 예제 따르는 hello를 참조 하세요.

  * 올바른 비밀 URL 예제: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * 올바른 KEK URL 예제: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* Azure Disk Encryption은 Key Vault 비밀 및 KEK URL의 일부로 포트 번호 지정을 지원하지 않습니다. 지원 되지 않는 및 지원 되는 키 자격 증명 모음 Url의 예를 보려면 hello 다음을 참조 하세요.

  * 허용되지 않는 Key Vault URL *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * 허용되는 Key Vault URL: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* tooenable hello Azure 디스크 암호화 기능을 hello IaaS Vm 네트워크 끝점 구성 요구 사항을 준수 하는 hello를 충족 해야 합니다.
  * tooget 토큰 tooconnect tooyour 키 자격 증명 모음을 hello IaaS VM 수 tooconnect tooan Azure Active Directory 끝점 있어야 \[login.microsoftonline.com\]합니다.
  * toowrite hello 암호화 키 tooyour 키 자격 증명 모음 hello IaaS VM 수 tooconnect toohello 주요 자격 증명 모음 끝점 이어야 합니다.
  * hello IaaS VM에는 호스트 hello Azure 확장 리포지토리 및 호스트 hello VHD 파일을 Azure 저장소 계정이 있는지 수 tooconnect tooan Azure 저장소 끝점 이어야 합니다.

  > [!NOTE]
  > 보안 정책에 Azure Vm toohello 인터넷에서에서 액세스를 제한 하는 경우 hello 앞에 URI를 확인할 수 있으며 특정 규칙 tooallow 아웃 바운드 연결 toohello Ip를 구성할 수 있습니다.
  >
  >tooconfigure 및 (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall) 방화벽 뒤에 있는 Azure 키 자격 증명 모음 액세스

* Hello 최신 버전의 Azure PowerShell SDK 버전 tooconfigure Azure 디스크 암호화를 사용 합니다. 최신 버전의 hello 다운로드 [Azure PowerShell 릴리스](https://github.com/Azure/azure-powershell/releases)

 > [!NOTE]
  > Azure Disk Encryption은 [Azure PowerShell SDK 버전 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016)에서 지원되지 않습니다. 오류가 발생 하는 경우 Azure PowerShell 1.1.0, toousing 관련 참조 [Azure 디스크 암호화 관련 오류 tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx)합니다.

* toorun Azure CLI 명령을 Azure 구독에 연결 하 고, 먼저 Azure CLI를 설치 해야 합니다.
  * Azure CLI tooinstall Azure 구독과 연결을 참조 하세요 [어떻게 tooinstall Azure CLI를 구성 하 고](../cli-install-nodejs.md)합니다.
  * Mac, Linux 및 Windows Azure 리소스 관리자와 Azure CLI toouse 참조 [리소스 관리자 모드에서 Azure CLI 명령을](../virtual-machines/azure-cli-arm-commands.md)합니다.

* 관리 되는 디스크를 암호화 하는 경우, 때는 필수 필수 tootake hello 관리 되는 디스크의 스냅숏을 또는 Azure 디스크 암호화 이전 tooenabling 암호화 외부 hello 디스크의 백업입니다.  위치에 백업 하지 않으면 암호화 하는 동안 예기치 않은 모든 오류 해석할 수 있습니다 hello 디스크 및 VM 복구 옵션 없이 액세스할 수 없습니다.  집합 AzureRmVMDiskEncryptionExtension 않습니다 하지 현재 관리 되는 디스크를 백업 하 고 hello-skipVmBackup 매개 변수를 지정 하지 않은 경우 관리 되는 디스크에 대해 사용 하는 경우 오류가 발생 합니다.  이 매개 변수 표시 되지 않으면 toouse 안전 하지 않은 백업을 Azure 디스크 암호화 외부에서 작성 되었습니다.   Hello-skipVmBackup 매개 변수를 지정 하는 경우 hello cmdlet hello 관리 되는 디스크에 대 한 이전 tooencryption의 백업을 만들지 않습니다.  이러한 이유로 hello 경우 복구는 나중에 VM이 Azure 디스크 암호화 tooenabling을 이전 하는 위치에는 관리 되는 디스크의 백업이 필요 있는지 필수 필수 toomake를 간주 됩니다.  
> [!NOTE]
 > 스냅숏 또는 백업 이미 이루어졌을 외부 Azure 디스크 암호화 하지 않는 한 hello-skipVmBackup 매개 변수 사용 하지 말아야 합니다. 

* Azure 디스크 암호화 솔루션 hello Windows IaaS Vm에 대 한 hello BitLocker 외부 키 보호기를 사용합니다. 도메인 가입 VM의 경우 TPM 보호기를 적용하는 그룹 정책을 푸시하지 마십시오. Hello 그룹 정책에 대 한 "호환 되는 TPM 없이 BitLocker 허용"에 대 한 정보를 참조 하십시오. [BitLocker 그룹 정책 참조](https://technet.microsoft.com/library/ee706521)합니다.
* 사용자 지정 그룹 정책 사용 하 여 도메인에 가입 된 가상 컴퓨터에서 Bitlocker 정책 설정에 따라 hello를 포함 해야 합니다: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` Azure 디스크 암호화는 Bitlocker에 대 한 사용자 지정 그룹 정책 설정을 호환 되지 않을 때 실패 합니다. Hello 되어 있지 않은 컴퓨터에서 올바른 정책 설정, hello 새 정책을 적용 hello 새 정책 tooupdate (gpupdate.exe /force)를 강제 적용 한 다음 다시 시작이 필요할 수 있습니다.  
* toocreate Azure AD 응용 프로그램 키 자격 증명 모음 만들기 또는 기존 키 자격 증명 모음 설정 및 암호화를 사용 하도록 설정, hello 참조 [필수 PowerShell 스크립트를 Azure 디스크 암호화](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1)합니다.
* hello Azure CLI를 사용 하 여 tooconfigure 디스크 암호화 필수 구성 요소 참조 [이 Bash 스크립트](https://github.com/ejarvi/ade-cli-getting-started)합니다.
* toouse hello Azure 백업 서비스 tooback 및 암호화가 설정 하 여 Azure 디스크 암호화 된 경우 암호화 복원 Vm hello Azure 디스크 암호화 키 구성을 사용 하 여 Vm을 암호화 합니다. 백업 서비스 hello KEK 구성만을 사용 하 여 암호화 된 Vm을 지원 합니다. 참조 [를 tooback 및 복원 방법을 Azure 백업을 암호화 하 여 가상 컴퓨터를 암호화](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption)합니다.

* Linux 운영 체제 볼륨을 암호화 하는 경우는 VM이 다시 시작 하는 현재 필요 hello 프로세스의 hello 끝에 있습니다. Hello 포털, powershell 또는 CLI를 통해이 작업을 수행할 수 있습니다.   암호화 tootrack hello 진행률 Get AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus에서 반환 하는 hello 상태 메시지를 주기적으로 폴링합니다.  암호화 완료 되 면이이 명령에서 반환 된 hello hello 상태 메시지가 표시 됩니다.  예를 들어 "ProgressMessage: 운영 체제 디스크가 성공적으로 암호화, hello VM 다시 부팅 하십시오" VM을 다시 시작 사용 하 고이 지점 hello에 있습니다.  

* Linux 용 azure 디스크 암호화 데이터 디스크 toohave Linux 이전 tooencryption에 탑재 된 파일 시스템에 필요

* 재귀적으로 탑재 된 데이터 디스크 Linux hello Azure 디스크 암호화에서 지원 되지 않습니다. 예를 들어 hello 대상 시스템에 /foo/bar에 디스크를 탑재 하 고 /foo/bar/baz, /foo/bar/baz의 hello 암호화에 다른 성공, 하지만/foo/막대의 암호화 되지 것입니다. 

* Azure 디스크 암호화는 hello 앞에서 언급 한 필수 구성 요소를 충족 하는 지원 되는 Azure 갤러리 이미지에만 지원 됩니다. 사용자 지정 이미지 고객 toocustom 파티션 구성표 및 이러한 이미지에 있을 수 있는 프로세스 동작 인해 지원 되지 않습니다. 또한 초기에 필수 조건을 충족했지만 작성 후 수정된 갤러리 이미지 기반 VM도 호환되지 않을 수 있습니다.  에 대 한 새로 갤러리 이미지에서 toostart은 이유로 hello 제안 Linux VM을 암호화 하기 위한 절차는, hello VM을 암호화 하 고 사용자 지정 소프트웨어나 데이터 toohello 필요에 따라 VM 추가 합니다.  

> [!NOTE]
> 암호화 된 Vm의 백업 및 복원 hello KEK 구성을 사용 하 여 암호화 된 Vm에 대해서만 지원 됩니다. KEK 없이 암호화된 VM에서는 지원되지 않습니다. KEK는 VM을 사용하도록 설정하는 선택적 매개 변수입니다.

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a>Azure Active Directory에서 Azure AD 응용 프로그램을 hello를 설정
Azure에서 실행 중인 VM에서 사용 하도록 설정 하는 암호화 toobe 필요할 때 Azure 디스크 암호화 생성 하 고 hello 암호화 키 tooyour 주요 자격 증명 모음을 작성 합니다. Key Vault에서 암호화 키를 관리하려면 Azure AD 인증이 필요합니다.

이런 목적으로 Azure AD 응용 프로그램을 만듭니다. Hello 블로그 게시물의 hello "hello 응용 프로그램에 대 한 Id 가져오기" 섹션에서 응용 프로그램 등록에 대 한 자세한 단계를 찾을 수 있습니다 [Azure 키 자격 증명 모음-단계별](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx)합니다. 이 게시물에는 Key Vault 설정 및 구성에 대한 유용한 예제도 다수 포함되어 있습니다. 인증을 위해 클라이언트 비밀 기반 인증 또는 클라이언트 인증서 기반 Azure AD 인증을 사용할 수 있습니다.

#### <a name="client-secret-based-authentication-for-azure-ad"></a>Azure AD에 대한 클라이언트 비밀 기반 인증
hello 다음 섹션에서는 Azure AD에 대 한 클라이언트 암호 기반 인증을 구성할 수 있습니다.

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a>Azure PowerShell을 사용하여 Azure AD 응용 프로그램 만들기
다음 PowerShell cmdlet toocreate Azure AD 응용 프로그램 hello를 사용 합니다.

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> $azureAdApplication.ApplicationId hello Azure AD ClientID 이며 $aadClientSecret hello 클라이언트 암호 이후 tooenable Azure 디스크 암호화를 사용 해야 합니다. Azure AD hello 클라이언트 암호를 적절 하 게 보호 합니다.

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a>Hello Azure 클래식 포털에서에서 Azure AD hello 클라이언트 ID와 암호를 설정합니다.
Hello를 사용 하 여 Azure AD 클라이언트 ID와 암호를 설정할 수도 있습니다 [Azure 클래식 포털]( https://manage.windowsazure.com)합니다. tooperform이 작업을 다음 hello지 않습니다.

1. Hello 클릭 **Active Directory** 탭 합니다.

 ![Azure 디스크 암호화](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. 클릭 **응용 프로그램 추가**, 다음 형식 hello 이름 및 응용 프로그램입니다.

 ![Azure 디스크 암호화](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. Hello 화살표 단추를 클릭 하 고 hello 응용 프로그램 속성을 구성 합니다.

 ![Azure 디스크 암호화](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. 하단 왼쪽된 모서리 toofinish hello에에서 hello 확인 표시를 클릭 합니다. hello 응용 프로그램 구성 페이지가 나타나고 hello Azure AD 클라이언트 ID는 hello hello 페이지 맨 아래에 표시 됩니다.

 ![Azure 디스크 암호화](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. Hello를 클릭 하 여 Azure AD hello 클라이언트 암호를 저장 **저장** 단추입니다. Note hello 키 텍스트 상자에 Azure AD hello 클라이언트 암호입니다. 비밀을 적절하게 보호합니다.

 ![Azure 디스크 암호화](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > 앞에 흐름 hello hello Azure 클래식 포털에서 지원 되지 않습니다.

##### <a name="use-an-existing-application"></a>기존 응용 프로그램 사용
tooexecute 명령 뒤 hello를 hello를 사용 하 여 [Azure AD PowerShell 모듈이](https://technet.microsoft.com/library/jj151815.aspx)합니다.

> [!NOTE]
> hello 다음 명령은 실행 해야 새 PowerShell 창에서. Azure PowerShell 또는 hello Azure 리소스 관리자 창 tooexecute hello 명령을 사용 하지 마십시오. Hello MSOnline 모듈 또는 Azure AD PowerShell에서 이러한 cmdlet은이 접근 방법이 권장 됩니다.

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a>Azure AD에 대한 인증서 기반 인증
> [!NOTE]
> Azure AD 인증서 기반 인증은 현재 Linux VM에서 지원되지 않습니다.

다음 섹션에서는 표시 방법을 hello tooconfigure Azure AD에 대 한 인증서 기반 인증 합니다.

##### <a name="create-an-azure-ad-application"></a>Azure AD 응용 프로그램 만들기
Azure AD 응용 프로그램 toocreate hello 다음 PowerShell cmdlet를 실행 합니다.

> [!NOTE]
> Hello 다음 대체 `yourpassword` 보안 암호 및 보호 방법 hello 암호를 포함 하는 문자열입니다.

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

이 단계를 완료 한 후 PFX 파일 tooyour 키 자격 증명 모음을 업로드 하 고 해당 인증서 tooa VM 액세스 필요한 정책의 toodeploy hello를 사용 하도록 설정 합니다.

##### <a name="use-an-existing-azure-ad-application"></a>기존 Azure AD 응용 프로그램 사용
기존 응용 프로그램에 대 한 인증서 기반 인증을 구성 하는 경우 여기에 표시 된 hello PowerShell cmdlet을 사용 합니다. 수 있는지 tooexecute 새 PowerShell 창에서.

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

이 단계를 완료 한 후 PFX 파일 tooyour 키 자격 증명 모음을 업로드 하 고 필요한 toodeploy hello 인증서 tooa VM hello 액세스 정책을 사용 하도록 설정 합니다.

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a>PFX 파일 tooyour 키 자격 증명 모음 업로드
이 프로세스에 대 한 자세한 내용은 참조 하십시오. [공식 Azure 키 자격 증명 모음 팀 블로그 hello](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx)합니다. 그러나 PowerShell cmdlet을 다음 hello hello 작업에 대 한 하기만 하면 됩니다. 있는지 tooexecute 될 Azure PowerShell 콘솔에서 합니다.

> [!NOTE]
> Hello 다음 대체 `yourpassword` 보안 암호 및 보호 방법 hello 암호를 포함 하는 문자열입니다.

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a>기존 VM 하 여 주요 자격 증명 모음 tooan에 인증서 배포
Hello PFX 업로드를 완료 한 후에 hello 주요 자격 증명 모음 tooan hello 다음 함께 존재 하는 VM에에서 인증서 배포:
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a>Hello Azure AD 응용 프로그램에 대 한 hello 주요 자격 증명 모음 액세스 정책을 설정합니다
Azure AD 응용 프로그램 권한 tooaccess hello 키 또는 hello 자격 증명 모음의 암호 필요합니다. 사용 하 여 hello [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant 권한 toohello 응용 프로그램 (있음 hello 응용 프로그램이 등록 될 때 생성 된) hello 클라이언트 ID를 사용 하 여 hello로 _– ServicePrincipalName_ 매개 변수 값입니다. toolearn hello 블로그 게시물을 더 참조 [Azure 키 자격 증명 모음-단계별](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx)합니다. 다음은 어떻게 tooperform이 작업을 통해의 예제 PowerShell:

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> Azure 디스크 암호화는 클라이언트 응용 프로그램을 Azure AD tooyour 액세스 정책에 따라 tooconfigure hello 필요: _WrapKey_ 및 _설정_ 사용 권한.

## <a name="terminology"></a>용어
이 기술을 사용 하 여 hello 용어 표 다음에서 사용 하는 일반적인 용어 hello toounderstand:

| 용어 | 정의 |
| --- | --- |
| Azure AD | Azure AD는 [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)입니다. Azure AD 계정은 Key Vault에서 비밀을 인증, 저장 및 검색하기 위한 필수 구성 요소입니다. |
| Azure Key Vault | Key Vault는 암호화 키 및 중요한 비밀을 안전하게 보호하는 FIPS(Federal Information Processing Standard) 유효성을 검사한 하드웨어 보안 모듈 기반의 암호화 키 관리 서비스입니다. 자세한 내용은 [Key Vault](https://azure.microsoft.com/services/key-vault/) 설명서를 참조하세요. |
| ARM | Azure 리소스 관리자 |
| BitLocker |[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) 업계에서 통용 되 Windows 볼륨 암호화 하는 기술로 Windows IaaS Vm에 tooenable 디스크 암호화를 사용 합니다. |
| BEK | BitLocker 암호화 키는 사용 되는 tooencrypt hello 운영 체제 부팅 볼륨 및 데이터 볼륨입니다. hello BitLocker 키를 암호로 키 자격 증명 모음에 통해 보호 됩니다. |
| CLI | [Azure 명령줄 인터페이스](../cli-install-nodejs.md)을 참조하세요. |
| DM-Crypt |[DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) 가 Linux IaaS Vm에 tooenable 디스크 암호화를 사용 하는 hello Linux ± â, 투명 한 디스크 암호화 하위 시스템입니다. |
| KEK | 키 암호화 키가 hello 비대칭 키 (RSA 2048) tooprotect 사용 또는 hello 비밀을 래핑할 수 있습니다. HSM(하드웨어 보안 모듈) 보호 키 또는 소프트웨어 보호 키를 제공할 수 있습니다. 자세한 내용은 [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) 설명서를 참조하세요. |
| PS cmdlet | [Azure PowerShell cmdlet](/powershell/azure/overview)을 참조하세요. |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a>Azure Disk Encryption을 위한 Key Vault 설정 및 구성
Azure 디스크 암호화 보호 방법 hello 디스크 암호화 키와 키 저장소의 암호는 합니다. Azure 디스크 암호화에 대 한 주요 자격 증명 모음을 tooset, 전체 hello hello 다음 섹션의 각 단계 합니다.

#### <a name="create-a-key-vault"></a>키 자격 증명 모음 만들기
주요 자격 증명 모음 toocreate hello 다음 옵션 중 하나를 사용 합니다.

* ["101-Key-Vault-Create" Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [Azure PowerShell Key Vault cmdlet](/powershell/module/azurerm.keyvault/#key_vault)
* Azure 리소스 관리자
* 어떻게 너무[주요 자격 증명 모음 보안](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)

> [!NOTE]
> 이미 설정한 경우 키 자격 증명 모음을 구독에 대 한, toohello 다음 섹션을 건너뜁니다.

![Azure 키 자격 증명 모음](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a>주요 암호화 키 설정(선택 사항)
Hello BitLocker 암호화 키에 대 한 보안에 대 한 추가 수준의 대 한 toouse는 KEK를 원하는 경우 KEK tooyour 주요 자격 증명 모음을 추가 합니다. 사용 하 여 hello [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate hello 키 자격 증명 모음에 키 암호화 키입니다. 또한 온-프레미스 키 관리 HSM에서 KEK를 가져올 수도 있습니다. 자세한 내용은 [Key Vault 설명서](https://azure.microsoft.com/documentation/services/key-vault/)를 참조하세요.

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

리소스 관리자 tooAzure 이동 하 여 또는 키 자격 증명 모음 인터페이스를 사용 하 여 hello KEK를 추가할 수 있습니다.

![Azure 키 자격 증명 모음](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a>Key Vault 사용 권한 설정
hello Azure 플랫폼 있어야 액세스 toohello 암호화 키 또는 키 자격 증명 모음 toomake의 비밀을 사용할 수 있는 toohello VM 부팅 하 고 hello 볼륨의 암호를 해독 합니다. toogrant 권한 toohello Azure 플랫폼 집합 hello **EnabledForDiskEncryption** hello 주요 자격 증명 모음 PowerShell cmdlet을 사용 하 여 자격 증명 모음에 hello 키의 속성:

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

Hello를 설정할 수도 있습니다 **EnabledForDiskEncryption** hello를 방문 하 여 속성 [Azure 리소스 탐색기](https://resources.azure.com)합니다.

Hello를 설정 해야 듯이, **EnabledForDiskEncryption** 주요 자격 증명 모음에는 속성입니다. 그렇지 않으면 hello 배포가 실패 합니다.

다음 그림과 같이 hello 주요 자격 증명 모음 인터페이스에서 Azure AD 응용 프로그램에 대 한 액세스 정책을 구성도 설정할 수 있습니다.

![Azure 키 자격 증명 모음](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Azure 키 자격 증명 모음](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

Hello에 **고급 액세스 정책은** 탭, 주요 자격 증명 모음 Azure 디스크 암호화를 활성화 되어 있는지 확인 합니다.

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a>디스크 암호화 배포 시나리오 및 사용자 환경
많은 디스크 암호화 시나리오를 활성화 하 고 hello 단계 toohello 시나리오에 따라 달라질 수 있습니다. hello 다음 섹션에서는 시나리오에 설명 hello 보다 자세히 설명에서 합니다.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a>Hello Marketplace에서에서 생성 된 새 IaaS Vm에 대 한 암호화를 사용 하도록 설정
Hello를 사용 하 여 hello azure에서 Marketplace에서에서 새 IaaS Windows VM에 디스크 암호화를 사용할 수 있습니다 [리소스 관리자 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image)합니다.

1. Azure 빠른 시작 hello 서식 파일에서 클릭 **tooAzure 배포**, hello에 hello 암호화 구성을 입력 **매개 변수** 블레이드에서 하 고 클릭 한 다음 **확인**합니다.

2. Hello 구독, 리소스 그룹, 리소스 그룹 위치, 법률 용어 및 계약을 선택한 다음 클릭 **만들기** 새 IaaS VM에 tooenable 암호화 합니다.

> [!NOTE]
> 이 템플릿은 Windows Server 2012 hello 갤러리 이미지를 사용 하는 새로운 암호화 된 Windows VM을 만듭니다.

이 [Resource Manager 템플릿](https://aka.ms/fde-rhel)을 사용하여 200GB RAID-0 배열이 있는 새 IaaS RedHat Linux 7.2 VM에서 디스크 암호화를 사용하도록 설정할 수 있습니다. Hello 서식 파일을 배포한 후 hello를 사용 하 여 hello VM 암호화 상태를 확인할 `Get-AzureRmVmDiskEncryptionStatus` 에 설명 된 대로 cmdlet [실행 중인 Linux VM의 OS 암호화 드라이브](#encrypting-os-drive-on-a-running-linux-vm)합니다. Hello 컴퓨터의 상태를 반환 하는 경우 _VMRestartPending_, hello VM을 다시 시작 합니다.

hello 다음 표에 나타난 hello 리소스 관리자 템플릿 매개 변수 Azure AD 클라이언트 ID를 사용 하 여 hello 마켓플레이스 시나리오에서 새 Vm에 대 한.

| 매개 변수 | 설명 |
| --- | --- |
| adminUserName | Hello 가상 컴퓨터에 대 한 관리 사용자 이름입니다. |
| adminPassword | Hello 가상 컴퓨터에 대 한 관리자 사용자 암호입니다. |
| newStorageAccountName | Hello 저장소 계정 toostore OS 및 데이터 Vhd의 이름입니다. |
| vmSize | Hello VM의 크기입니다. 현재 표준 A, D 및 G 시리즈만 지원됩니다. |
| virtualNetworkName | Hello 해당 hello VM NIC VNet의 이름에 속해야 합니다. |
| subnetName | Hello hello VM NIC 해당 VNet에에서 hello 서브넷의 이름에 속해야 합니다. |
| AADClientID | 사용 권한을 toowrite 비밀 tooyour 주요 자격 증명 모음을 가진 hello Azure AD 응용 프로그램의 클라이언트 ID입니다. |
| AADClientSecret | 사용 권한을 toowrite 비밀 tooyour 주요 자격 증명 모음을 가진 hello Azure AD 응용 프로그램의 클라이언트 암호입니다. |
| keyVaultURL | URL hello 키 자격 증명 모음에 해당 hello BitLocker 키를 업로드 해야 합니다. Hello cmdlet을 사용 하 여 얻을 수 `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`합니다. |
| keyEncryptionKeyURL | Hello 키 암호화 키를 사용 하는 tooencrypt hello의 URL (선택 사항) BitLocker 키를 생성 합니다. |
| keyVaultResourceGroup | 리소스 그룹 hello 주요 자격 증명 모음입니다. |
| vmName | Hello 암호화 작업이 hello VM 이름은 toobe에서 수행 합니다. |

> [!NOTE]
> _KeyEncryptionKeyURL_은 선택적 매개 변수입니다. 주요 자격 증명 모음에 직접 KEK toofurther 보호 방법을 hello 데이터 암호화 키 (암호 secret)를 가져올 수 있습니다.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a>고객 암호화 VHD 및 암호화 키에서 만든 새 IaaS VM에서 암호화 사용
이 시나리오에서는 hello 리소스 관리자 템플릿, PowerShell cmdlet 또는 CLI 명령을 사용 하 여 암호화를 사용할 수 있습니다. hello 다음 섹션에서는 큰 세부 hello 리소스 관리자 템플릿 및 CLI 명령에 합니다.

이 섹션에서는 Azure에서 사용할 수 있는 미리 암호화 된 이미지를 준비 하기 위한 중 하나에서 hello 지침을 따릅니다. Hello 이미지를 만든 후 hello 단계 hello 다음 섹션 toocreate 암호화 된 Azure VM에서에서 사용할 수 있습니다.

* [사전에 암호화된 Windows VHD 준비](#preparing-a-pre-encrypted-windows-vhd)
* [사전에 암호화된 Linux VHD 준비](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a>Hello 리소스 관리자 템플릿을 사용 하 여
Hello를 사용 하 여 암호화 된 VHD에서 디스크 암호화를 사용할 수 있습니다 [리소스 관리자 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm)합니다.

1. Azure 빠른 시작 hello 서식 파일에서 클릭 **tooAzure 배포**, hello에 hello 암호화 구성을 입력 **매개 변수** 블레이드에서 하 고 클릭 한 다음 **확인**합니다.

2. Hello 구독, 리소스 그룹, 리소스 그룹 위치, 법률 용어 및 계약을 선택한 다음 클릭 **만들기** tooenable 암호화 hello 새 IaaS VM입니다.

hello 다음 표에 나타난 hello 리소스 관리자 템플릿 매개 변수 암호화 된 VHD에 대 한.

| 매개 변수 | 설명 |
| --- | --- |
| newStorageAccountName | 운영 체제 VHD 암호화 하는 hello 저장소 계정 toostore hello의 이름입니다. 이 저장소 계정은 이미 만들어야 hello에 동일한 리소스 그룹 및 VM hello와 동일한 위치입니다. |
| osVhdUri | Hello 저장소 계정에서 hello OS VHD의 URI입니다. |
| osType | OS 제품 유형(Windows/Linux) |
| virtualNetworkName | Hello 해당 hello VM NIC VNet의 이름에 속해야 합니다. hello 이름 해야 이미 만들어져 hello에 동일한 리소스 그룹 및 VM hello와 동일한 위치입니다. |
| subnetName | Hello hello VM NIC 해당 VNet에 hello 서브넷의 이름에 속해야 합니다. |
| vmSize | Hello VM의 크기입니다. 현재 표준 A, D 및 G 시리즈만 지원됩니다. |
| keyVaultResourceID | Azure 리소스 관리자의 hello 주요 자격 증명 모음 리소스를 식별 하는 리소스 Id 번호입니다. Hello PowerShell cmdlet을 사용 하 여 얻을 수 `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`합니다. |
| keyVaultSecretUrl | Hello 키 자격 증명 모음에 설정 된 hello 디스크 암호화 키의 URL입니다. |
| keyVaultKekUrl | 생성 된 hello 디스크 암호화 키를 암호화 하기 위한 hello 키 암호화 키의 URL입니다. |
| vmName | Hello IaaS VM의 이름입니다. |

#### <a name="using-powershell-cmdlets"></a>PowerShell cmdlet 사용
Hello PowerShell cmdlet을 사용 하 여 암호화 된 VHD에서 디스크 암호화를 사용할 수 있습니다 [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk)합니다.  

#### <a name="using-cli-commands"></a>CLI 명령 사용
CLI 명령을 사용 하 여이 시나리오에 대 한 디스크 암호화 tooenable 다음 hello지 않습니다.

1. Key Vault에 대한 액세스 정책 설정:

   * 집합 hello **EnabledForDiskEncryption** 플래그:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * 사용 권한을 tooAzure AD 응용 프로그램 toowrite 비밀 tooyour 주요 자격 증명 모음을 설정 합니다.

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. 기존 또는 실행 중인 VM, 형식에서 tooenable 암호화:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. 암호화 상태 가져오기:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. 암호화 된 VHD 사용 하 여 hello hello로 매개 변수 뒤에서 새 VM에서 tooenable 암호화 `azure vm create` 명령:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a>Azure에서 기존 또는 실행 중인 IaaS Windows VM에서 암호화 사용
이 시나리오에서는 hello 리소스 관리자 템플릿, PowerShell cmdlet 또는 CLI 명령을 사용 하 여 암호화를 사용할 수 있습니다. hello 다음 섹션에 설명 자세히 어떻게 리소스 관리자 템플릿 및 CLI 명령을 사용 하 여 hello tooenable 합니다.

#### <a name="using-hello-resource-manager-template"></a>Hello 리소스 관리자 템플릿을 사용 하 여
디스크 암호화 기존 컨트롤이 나 hello를 사용 하 여 Azure에서 IaaS Windows Vm 실행에 사용할 수 있습니다 [리소스 관리자 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm)합니다.

1. Azure 빠른 시작 hello 서식 파일에서 클릭 **tooAzure 배포**, hello에 hello 암호화 구성을 입력 **매개 변수** 블레이드에서 하 고 클릭 한 다음 **확인**합니다.

2. Hello 구독, 리소스 그룹, 리소스 그룹 위치, 법률 용어 및 계약을 선택한 다음 클릭 **만들기** tooenable 암호화 hello 기존 컨트롤이 나 IaaS VM을 실행 합니다.

hello 다음 표에 나타난 기존 컨트롤이 나 실행 중인 Azure AD 클라이언트 ID를 사용 하는 Vm에 대 한 hello 리소스 관리자 템플릿 매개 변수.

| 매개 변수 | 설명 |
| --- | --- |
| AADClientID | 사용 권한을 toowrite 비밀 toohello 주요 자격 증명 모음을 가진 hello Azure AD 응용 프로그램의 클라이언트 ID입니다. |
| AADClientSecret | 사용 권한을 toowrite 비밀 toohello 주요 자격 증명 모음을 가진 hello Azure AD 응용 프로그램의 클라이언트 암호입니다. |
| keyVaultName | Hello 키의 이름 자격 증명 모음에 해당 hello BitLocker 키를 업로드 해야 합니다. Hello cmdlet을 사용 하 여 얻을 수 `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`합니다. |
|  keyEncryptionKeyURL | BitLocker 키를 생성 한 hello 키 암호화 키를 사용 하는 tooencrypt hello의 URL입니다. 이 매개 변수는 선택 하는 경우 선택적 **nokek** hello UseExistingKek 드롭 다운 목록에 있습니다. 선택 하는 경우 **kek** hello UseExistingKek 드롭 다운 목록에서 hello를 입력 해야 _keyEncryptionKeyURL_ 값입니다. |
| volumeType | Hello 암호화 작업이 수행 되는 볼륨의 형식입니다. 유효한 값은 _OS_, _Data_ 및 _All_입니다. |
| sequenceVersion | Hello BitLocker 작업의 시퀀스 버전입니다. Hello에서 디스크 암호화 연산이 수행 될 때마다 버전 번호를 하나씩 늘립니다. 동일한 VM입니다. |
| vmName | Hello 암호화 작업이 hello VM 이름은 toobe에서 수행 합니다. |

> [!NOTE]
> _KeyEncryptionKeyURL_은 선택적 매개 변수입니다. Hello 키 자격 증명 모음에 직접 KEK toofurther 보호 방법을 hello 데이터 암호화 키 (BitLocker 암호화 암호)를 가져올 수 있습니다.

#### <a name="using-powershell-cmdlets"></a>PowerShell cmdlet 사용
PowerShell cmdlet을 사용 하 여 Azure 디스크 암호화를 사용 하 여 암호화를 사용 하는 방법에 대 한 내용은 hello 블로그 게시물을 참조 하십시오. [1 부-Azure PowerShell을 사용한 Azure 디스크 암호화 탐색](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) 및 [탐색 Azure 디스크 암호화 Azure powershell-2 부](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)합니다.

#### <a name="using-cli-commands"></a>CLI 명령 사용
기존 컨트롤이 나 CLI 명령을 사용 하 여 Azure에서 IaaS Windows VM 실행에 tooenable 암호화 다음 hello지 않습니다.

1. tooset hello 키 자격 증명 모음에 대 한 액세스 정책:
   * 집합 hello **EnabledForDiskEncryption** 플래그:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * 사용 권한을 tooAzure AD 응용 프로그램 toowrite 비밀 tooyour 주요 자격 증명 모음을 설정 합니다.

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. 기존 또는 실행 중인 VM에서 tooenable 암호화:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. tooget 암호화 상태:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. 암호화 된 VHD 사용 하 여 hello hello로 매개 변수 뒤에서 새 VM에서 tooenable 암호화 `azure vm create` 명령:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a>Azure에서 기존 또는 실행 중인 IaaS Linux VM에서 암호화 사용
Hello를 사용 하 여 Azure에서 기존 또는 실행 중인 IaaS Linux VM에서 디스크 암호화를 사용할 수 있습니다 [리소스 관리자 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm)합니다.

1. 클릭 **tooAzure 배포** hello Azure 빠른 시작 서식 파일에 hello에 hello 암호화 구성을 입력 **매개 변수** 블레이드에서 하 고 클릭 한 다음 **확인**합니다.

2. Hello 구독, 리소스 그룹, 리소스 그룹 위치, 법률 용어 및 계약을 선택한 다음 클릭 **만들기** tooenable 암호화 hello 기존 컨트롤이 나 IaaS VM을 실행 합니다.

다음 표에서 hello 기존 컨트롤이 나 실행 중인 Azure AD 클라이언트 ID를 사용 하는 Vm에 대 한 리소스 관리자 템플릿 매개 변수를 나열 합니다.

| 매개 변수 | 설명 |
| --- | --- |
| AADClientID | 사용 권한을 toowrite 비밀 toohello 주요 자격 증명 모음을 가진 hello Azure AD 응용 프로그램의 클라이언트 ID입니다. |
| AADClientSecret | 사용 권한을 toowrite 비밀 tooyour 주요 자격 증명 모음을 가진 hello Azure AD 응용 프로그램의 클라이언트 암호입니다. |
| keyVaultName | Hello 키의 이름 자격 증명 모음에 해당 hello BitLocker 키를 업로드 해야 합니다. Hello cmdlet을 사용 하 여 얻을 수 `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`합니다. |
|  keyEncryptionKeyURL | BitLocker 키를 생성 한 hello 키 암호화 키를 사용 하는 tooencrypt hello의 URL입니다. 이 매개 변수는 선택 하는 경우 선택적 **nokek** hello UseExistingKek 드롭 다운 목록에 있습니다. 선택 하는 경우 **kek** hello UseExistingKek 드롭 다운 목록에서 hello를 입력 해야 _keyEncryptionKeyURL_ 값입니다. |
| volumeType | Hello 암호화 작업이 수행 되는 볼륨의 형식입니다. 지원되는 유효한 값은 _OS_ 또는 _All_(RHEL 7.2, CentOS 7.2, Ubuntu 16.04의 경우)이고 다른 모든 배포판의 경우 _Data_입니다. |
| sequenceVersion | Hello BitLocker 작업의 시퀀스 버전입니다. Hello에서 디스크 암호화 연산이 수행 될 때마다 버전 번호를 하나씩 늘립니다. 동일한 VM입니다. |
| vmName | Hello 암호화 작업이 hello VM 이름은 toobe에서 수행 합니다. |
| passPhrase | Hello 데이터 암호화 키로 강력한 암호를 입력 합니다. |

> [!NOTE]
> _KeyEncryptionKeyURL_은 선택적 매개 변수입니다. 주요 자격 증명 모음에 직접 KEK toofurther 보호 방법을 hello 데이터 암호화 키 (암호 secret)를 가져올 수 있습니다.

#### <a name="cli-commands"></a>CLI 명령
설치 하 고 hello를 사용 하 여 암호화 된 VHD에서 디스크 암호화를 사용할 수 있습니다 [CLI 명령을](../cli-install-nodejs.md)합니다. 기존 컨트롤이 나 CLI 명령을 사용 하 여 Azure에서 IaaS Linux Vm을 실행 중인 tooenable 암호화 다음 hello지 않습니다.

1. Hello 키 자격 증명 모음에 액세스 정책을 설정 합니다.

 * 집합 hello **EnabledForDiskEncryption** 플래그:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * 사용 권한을 tooAzure AD 응용 프로그램 toowrite 비밀 tooyour 주요 자격 증명 모음을 설정 합니다.

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. 기존 또는 실행 중인 VM에서 tooenable 암호화:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. 암호화 상태 가져오기:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. 암호화 된 VHD 사용 하 여 hello hello로 매개 변수 뒤에서 새 VM에서 tooenable 암호화 `azure vm create` 명령:
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a>암호화 된 IaaS VM의 hello 암호화 상태를 가져옵니다.
Azure 리소스 관리자를 사용 하 여 hello 암호화 상태를 가져올 수 있습니다 [PowerShell cmdlet](/powershell/azure/overview), 또는 CLI 명령입니다. 다음 섹션 hello 어떻게 toouse hello Azure 클래식 포털 및 CLI 명령 tooget hello 암호화 상태를 설명 합니다.

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a>Azure 리소스 관리자를 사용 하 여 암호화 된 Windows VM의 hello 암호화 상태를 가져옵니다.
Hello 다음을 수행 하 여 hello IaaS VM의 hello 암호화 상태를 Azure 리소스 관리자에서 얻을 수 있습니다.

1. Toohello 로그인 [Azure 클래식 포털](https://portal.azure.com/), 클릭 하 고 **가상 컴퓨터** hello 왼쪽된 창 toosee hello 구독의 가상 컴퓨터의 요약 보기에에서 있습니다. Hello에 hello 구독 이름을 선택 하 여 hello 가상 컴퓨터 보기를 필터링 할 수 **구독** 드롭 다운 목록입니다.

2. Hello의 hello 위쪽 **가상 컴퓨터** 페이지 **열**합니다.

3. Hello에 **선택 열** 블레이드를 **디스크 암호화**, 클릭 하 고 **업데이트**합니다. Hello 디스크 암호화 열 보여 주는 hello 암호화 상태 표시 되어야 _Enabled_ 또는 _해제_ hello 다음 그림에에서 나와 있는 것 처럼 각 VM에 대해:

 ![Azure의 Microsoft 맬웨어 방지](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a>Hello 디스크 암호화 PowerShell cmdlet을 사용 하 여 암호화 된 IaaS VM (Windows/Linux)의 hello 암호화 상태를 가져옵니다.
Hello 디스크 암호화 PowerShell cmdlet에서 hello IaaS VM의 hello 암호화 상태를 가져올 수 있습니다 `Get-AzureRmVMDiskEncryptionStatus`합니다. VM에 대 한 tooget hello 암호화 설정을 hello 다음을 입력 합니다.

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

hello 출력을 검사할 수 _Get AzureRmVMDiskEncryptionStatus_ 암호화에 대 한 Url을 입력 합니다.

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

OSVolumeEncrypted hello 및 DataVolumesEncrypted 설정 값을 보여 주 Azure 디스크 암호화를 사용 하 여 두 볼륨 암호화 된 too_Encrypted_ 설정 됩니다. PowerShell cmdlet을 사용 하 여 Azure 디스크 암호화를 사용 하 여 암호화를 사용 하는 방법에 대 한 내용은 hello 블로그 게시물을 참조 하십시오. [1 부-Azure PowerShell을 사용한 Azure 디스크 암호화 탐색](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) 및 [탐색 Azure 디스크 암호화 Azure powershell-2 부](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)합니다.

> [!NOTE]
> Linux Vm에서 hello에 대 한 3 toofour 분 걸리는 `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport hello 암호화 상태입니다.

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a>Hello 디스크 암호화 CLI 명령에서 hello IaaS VM의 hello 암호화 상태를 가져옵니다.
Hello 디스크 암호화 CLI 명령을 사용 하 여 hello IaaS VM의 hello 암호화 상태를 가져올 수 있습니다 `azure vm show-disk-encryption-status`합니다. VM에 대 한 tooget hello 암호화 설정을 Azure CLI 세션을 입력 합니다.

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a>실행 중인 Windows IaaS VM에서 암호화 사용 안 함
Hello Azure 디스크 암호화 리소스 관리자 템플릿 또는 PowerShell cmdlet을 통해 실행 중인 Windows 또는 Linux IaaS VM에 대 한 암호화를 사용 하지 않도록 설정할 수 있으며 hello 암호 해독 구성을 지정할 수 있습니다.

##### <a name="windows-vm"></a>Windows VM
hello 사용 안 함 암호화 단계는 hello OS, hello 데이터 볼륨에 또는 둘 다 Windows IaaS VM을 실행 하는 hello의 암호화를 해제 합니다. Hello OS 볼륨을 사용 하지 않도록 설정 하 고 hello 데이터 볼륨이 암호화 된 상태로 둡니다 수 없습니다. Hello 암호화 사용 안 함 작업을 수행 하는 경우 hello Azure 클래식 배포 모델 hello VM 서비스 모델을 업데이트 하 고 IaaS VM Windows hello를 암호 해독 된 표시 됩니다. hello VM의 hello 콘텐츠는 더 이상 휴지 암호화 됩니다. hello 암호 해독 경우 키 자격 증명 모음 및 hello 암호화 키 자료 (Windows 및 Linux에 대 한 암호에 대 한 BitLocker 암호화 키)를 삭제 하지 않습니다.

##### <a name="linux-vm"></a>Linux VM
hello 사용 안 함 암호화 단계는 Linux IaaS VM을 실행 하는 hello에 hello 데이터 볼륨의 암호화를 해제 합니다. 이 단계는 hello OS 디스크 암호화 되지 않은 경우에 작동 합니다.

> [!NOTE]
> Hello OS 디스크에 대 한 암호화를 사용 하지 않으면 Linux Vm에서 허용 되지 않습니다.

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>기존 또는 실행 중인 IaaS VM에서 암호화 사용 안 함
Hello를 사용 하 여 실행 중인 Windows IaaS Vm에 디스크 암호화를 비활성화할 수 [리소스 관리자 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm)합니다.

1. Azure 빠른 시작 hello 서식 파일에서 클릭 **tooAzure 배포**, hello에 hello 암호 해독 구성을 입력 **매개 변수** 블레이드에서 하 고 클릭 한 다음 **확인**합니다.

2. Hello 구독, 리소스 그룹, 리소스 그룹 위치, 법률 용어 및 계약을 선택한 다음 클릭 **만들기** 새 IaaS VM에 tooenable 암호화 합니다.

Linux Vm에 대 한 hello를 사용 하 여 암호화를 비활성화할 수 [실행 중인 Linux VM에 대 한 암호화를 사용 하지 않도록 설정](https://aka.ms/decrypt-linuxvm) 템플릿.

hello 다음 표에서 실행 중인 IaaS VM에 대 한 암호화를 사용 하지 않도록 설정 하는 것에 대 한 리소스 관리자 템플릿 매개 변수:

| 매개 변수 | 설명 |
| --- | --- |
| vmName | Hello 암호화 작업이 hello VM 이름은 toobe에서 수행 합니다.
| volumeType | 암호 해독 작업을 수행할 볼륨의 유형. 유효한 값은 _OS_, _Data_ 및 _All_입니다. Hello에 대 한 암호화를 사용 하지 않도록 설정 하지 않고 Windows IaaS VM OS/부팅 볼륨 실행에 대 한 암호화를 비활성화할 수 없습니다 _데이터_ 볼륨입니다. 또한 Linux Vm에서 hello OS 디스크에 암호화 사용 안 함은 허용 되지 않음을 note 합니다. |
| sequenceVersion | Hello BitLocker 작업의 시퀀스 버전입니다. Hello에 디스크 암호 해독 작업은 수행 될 때마다 버전 번호를 하나씩 늘립니다. 동일한 VM입니다. |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>기존 또는 실행 중인 IaaS VM에서 암호화 사용 안 함
hello PowerShell cmdlet을 사용 하 여 기존 또는 실행 중인 IaaS VM에 toodisable 암호화 참조 [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption)합니다. 이 cmdlet에는 Windows 및 Linux VM을 둘 다 지원합니다. toodisable 암호화 hello 가상 컴퓨터 확장을 설치합니다. 경우 hello _이름_ 매개 변수를 지정 하지 않으면 hello 기본 이름에 확장명 _Windows Vm에 대 한 AzureDiskEncryption_ 만들어집니다.

Linux Vm에서 hello AzureDiskEncryptionForLinux 확장 사용 됩니다.

> [!NOTE]
> 이 cmdlet hello 가상 컴퓨터를 다시 부팅합니다.

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a>Azure 관리 디스크를 사용하여 미리 암호화된 IaaS VM에 대한 암호화 사용
Hello Azure 관리 되는 디스크 ARM 템플릿 toocreate hello ARM 템플릿을 사용 하 여 미리 암호화 된 VHD에서 암호화 된 VM에 있는 사용   
[미리 암호화된 VHD/저장소 BLOB를 통해 암호화된 관리 디스크 새로 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a>Azure 관리 디스크를 사용하여 새로운 Linux IaaS VM에 대한 암호화 사용
Hello Azure 관리 되는 디스크 ARM 템플릿 toocreate 새 Linux IaaS VM에 있는 hello ARM 템플릿을 사용 하 여 암호화를 사용 하 여   
[전체 디스크 암호화를 사용하여 RHEL 7.2 배포](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a>Azure 관리 디스크를 사용하여 새로운 Windows IaaS VM에 대한 암호화 사용
 Hello Azure 관리 되는 디스크 ARM 템플릿 toocreate 새 Linux IaaS VM에 있는 hello ARM 템플릿을 사용 하 여 암호화를 사용 하 여   
 [갤러리 이미지로 암호화된 Windows IaaS 관리 디스크 VM 새로 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)

  > [!NOTE]
  >외부 VM 인스턴스 및 이전 tooenabling Azure 디스크 암호화 백업 관리 되는 디스크 기반 이거나 필수 toosnapshot는 합니다.  Hello 관리 되는 디스크의 스냅숏을 hello 포털에서 가져올 수 있습니다 또는 Azure 백업에 사용할 수 있습니다.  백업을은 암호화 하는 동안 복구 옵션 hello 경우 예기치 않은 실패의 가능한 지 확인 하십시오.  백업이 만들어지지 면 hello 집합 AzureRmVMDiskEncryptionExtension cmdlet hello-skipVmBackup 매개 변수를 지정 하 여 관리 되는 사용 되는 tooencrypt 디스크를 수 있습니다.  이 명령은 백업을 만들고 이 매개 변수가 지정될 때까지 관리 디스크 기반 VM에 대해 실패합니다.    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a>기존의 암호화된 프리미엄 이외 VM의 암호화 설정 업데이트
  Hello 기존 Azure 디스크 암호화를 지원 인터페이스 사용 [PS cmdlet, CLI 또는 ARM 템플릿] VM tooupdate hello 암호화 설정을 실행 하기 위한 AAD 클라이언트 ID/비밀 키 암호화 키 [KEK]에 대 한 암호 또는 Windows VM에 대 한 BitLocker 암호화 키와 같은 Linux VM 등 hello 업데이트 암호화 설정은 프리미엄 저장소에서 지원 되는 Vm에 대해서만 지원 됩니다. Premium Storage에서 지원하는 VM에는 지원되지 않습니다.

## <a name="appendix"></a>부록
### <a name="connect-tooyour-subscription"></a>Tooyour 구독 연결
계속 진행 하기 전에 검토 hello *필수 구성 요소* 이 문서의 섹션. 모든 필수 조건이 충족 되었는지 확인 한 후 hello 다음을 수행 하 여 tooyour 구독을 연결 합니다.

1. Azure PowerShell 세션을 시작 하 고 다음 명령을 hello로 tooyour Azure 계정에에서 로그인 합니다.

    `Login-AzureRmAccount`

2. 구독이 여러 개 있고 toospecify 하나의 toouse 원하는 hello toosee hello 구독 계정에 대해 다음을 입력 합니다.

    `Get-AzureRmSubscription`

3. toouse, 원하는 toospecify hello 구독 유형:

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. 구성 된 hello 구독 올바른지 tooverify, 유형:

    `Get-AzureRmSubscription`

5. tooconfirm hello Azure 디스크 암호화 cmdlet이 설치 유형:

    `Get-command *diskencryption*`

6. 다음 출력 hello hello Azure 디스크 암호화 PowerShell 설치를 확인 합니다.

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a>사전에 암호화된 Windows VHD 준비
hello 다음 섹션에서는 필요한 tooprepare Azure IaaS에서 암호화 된 VHD로 배포를 위한 Windows VHD 사전에 암호화 됩니다. 새 Windows VM (VHD) Azure 또는 Azure Site Recovery에서 부팅 및 정보 tooprepare hello를 사용 합니다.

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a>그룹 정책 tooallow 비 TPM 보호 운영 체제에 대 한 업데이트
Hello BitLocker 그룹 정책 설정을 구성 **BitLocker 드라이브 암호화**, 아래에서 찾을 수 있는 **로컬 컴퓨터 정책** > **컴퓨터 구성**  >  **관리 템플릿** > **Windows 구성 요소**합니다. 이 설정을 너무 변경할**운영 체제 드라이브** > **시작 시 추가 인증을 요구** > **호환되는TPM없이BitLocker허용**hello 다음 그림에에서 나온 것 처럼:

![Azure의 Microsoft 맬웨어 방지](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a>BitLocker 기능 구성 요소 설치
Windows Server 2012 이상 버전에서는 hello 다음 명령을 사용 합니다.

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

Windows Server 2008 r 2에 대 한 hello 다음 명령을 사용 합니다.

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a>Hello OS 볼륨을 사용 하 여 BitLocker를 위한 준비`bdehdcfg`
toocompress OS 파티션 hello 및 BitLocker에 대 한 hello 컴퓨터를 준비, hello 다음 명령을 실행 합니다.

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a>BitLocker를 사용 하 여 hello OS 볼륨 보호
사용 하 여 hello [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) 는 외부 키 보호기를 사용 하 여 hello 부팅 볼륨에 명령 tooenable 암호화 합니다. 또한 hello 외부 키 (.bek 파일) hello 외장형 드라이브 또는 볼륨에 배치 합니다. 암호화는 hello 다음 다시 부팅 후 hello 시스템/부팅 볼륨에 사용 됩니다.

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> BitLocker를 사용 하 여 hello 외부 키를 가져오기 위한 별도 데이터/리소스 VHD와 VM hello를 준비 합니다.

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a>실행 중인 Linux VM에서 OS 드라이브 암호화
실행 중인 Linux VM에는 운영 체제 드라이브의 암호화 hello 분포 뒤에 사용할 수 있습니다.

* RHEL 7.2
* CentOS 7.2
* Ubuntu 16.04

##### <a name="prerequisites-for-os-disk-encryption"></a>OS 디스크 암호화를 위한 필수 조건

* Azure 리소스 관리자의 hello 마켓플레이스 이미지 로부터 hello VM을 만들어야 합니다.
* 4GB 이상의 RAM이 있는 Azure VM(권장 크기는 7GB)이 있어야 합니다.
* (RHEL 및 CentOS) SELinux를 사용하지 않도록 설정합니다. toodisable SELinux, 참조 "4.4.2 합니다. 사용할 수 없도록 SELinux"hello [SELinux 사용자 및 관리자의 가이드](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) hello VM에 있습니다.
* SELinux 해제 한 후 한 번 이상 hello VM 다시 부팅 합니다.

##### <a name="steps"></a>단계
1. 이전에 지정한 hello 분포 중 하나를 사용 하 여 VM을 만듭니다.

 CentOS 7.2의 경우 특수 이미지를 통해 OS 디스크 암호화가 지원됩니다. toouse 이미지이 hello VM을 만들 때 SKU hello 대로 "7.2n"를 지정 합니다.
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. Tooyour 요구에 따라 hello VM을 구성 합니다. 것 tooencrypt 모든 hello (OS + 데이터) 드라이브를 지정 및 /etc/fstab에서 탑재 가능한 hello 데이터 드라이브 toobe를 필요 합니다.

 > [!NOTE]
 > UUID를 사용 하 여 데이터 드라이브/등/fstab hello 블록 장치 이름 (예를 들어 /dev/sdb1)를 지정 하는 대신에 toospecify =.... 암호화 하는 동안 VM hello 드라이브의 hello 순서가 변경 됩니다. Toomount 못합니다 VM 블록 장치의 특정 순서를 사용 하는 경우 암호화 후 합니다.

3. 세션 로그 아웃 한 hello SSH 합니다.

4. tooencrypt hello OS를 지정으로 volumeType **모든** 또는 **OS** 때 있습니다 [암호화 사용](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure)합니다.

 > [!NOTE]
 > `systemd` 서비스로 실행되지 않는 모든 사용자 공간 프로세스는 `SIGKILL`로 중지됩니다. Hello VM 다시 부팅 합니다. 실행 중인 VM에서 OS 디스크 암호화를 사용할 경우 VM의 가동 중지 시간을 계획하세요.

5. 주기적으로 hello에 hello 지침을 사용 하 여 암호화 hello 진행률을 모니터링할 [절로](#monitoring-os-encryption-progress)합니다.

6. Get AzureRmVmDiskEncryptionStatus "VMRestartPending" 표시 되 면 tooit에 로그인 하거나 hello 포털, PowerShell 또는 CLI를 사용 하 여 VM 다시 시작 합니다.
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
컴퓨터를 다시 부팅 하기 전에 저장 하는 것이 좋습니다 [진단 부팅](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) hello VM의 합니다.

#### <a name="monitoring-os-encryption-progress"></a>OS 암호화 진행 상태 모니터링
OS 암호화 진행 상태를 모니터링하는 방법은 세 가지가 있습니다.

* 사용 하 여 hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet hello ProgressMessage 필드를 검사 합니다.
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 약 40 hello VM이 "운영 체제는 시작 하는 암호화 디스크"에 도달 하면 후 걸리는 too50 분 프리미엄 저장소에서 VM을 백업 합니다.

 WALinuxAgent에서 [문제 #388](https://github.com/Azure/WALinuxAgent/issues/388)으로 인해 일부 배포판에서 `OsVolumeEncrypted` 및 `DataVolumesEncrypted`가 `Unknown`으로 표시됩니다. WALinuxAgent 2.1.5 버전 이상에서는 이 문제가 자동으로 수정됩니다. 표시 되 면 `Unknown` hello 출력에 hello Azure 리소스 탐색기를 사용 하 여 디스크 암호화 상태를 확인할 수 있습니다.

 너무 이동[Azure 리소스 탐색기](https://resources.azure.com/), 한 다음 왼쪽에 hello 선택 패널에서이 계층 구조를 확장 합니다.

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 Hello InstanceView, toosee 드라이브의 암호화 상태를 hello 아래로 스크롤하십시오.

 ![VM 인스턴스 보기](./media/azure-security-disk-encryption/vm-instanceview.png)

* [부트 진단](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/)을 살펴봅니다. Hello 이름 확장 프로그램에서에서 메시지를 접두사로와 야 `[AzureDiskEncryption]`합니다.

* Toohello SSH 통해 VM에에서 로그인 하 고 hello 확장 로그에서 가져오려면:

    /var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux

 서명 하지 않은 toohello VM의에서 OS 암호화가 진행 중인 동안 하는 것이 좋습니다. Hello 다른 두 가지 방법은 실패 한 경우에 hello 로그를 복사 합니다.

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a>사전에 암호화된 Linux VHD 준비
##### <a name="ubuntu-16"></a>Ubuntu 16
Hello 다음을 수행 하 여 hello 배포 설치 중에 암호화를 구성 합니다.

1. 선택 **암호화 된 볼륨 구성** hello 디스크를 분할할 수 있습니다.

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. 암호화되지 않아야 하는 별도의 부트 드라이브를 만듭니다. 루트 드라이브를 암호화합니다.

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. 암호를 제공합니다. Toohello 주요 자격 증명 모음을 업로드 하는 hello 암호입니다.

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. 분할을 완료합니다.

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. Hello VM 부팅 하 고 암호를 요구 하는 경우 3 단계에서 제공 하는 hello 암호를 사용 합니다.

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. VM hello를 사용 하 여 Azure에 업로드 하기 위한 준비 [이러한 지침](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/)합니다. Hello 마지막 단계 (프로 비전 해제 hello VM)를 아직 실행 하지 마십시오.

Hello 다음을 수행 하 여 Azure를 사용한 암호화 toowork를 구성 합니다.

1. 다음 스크립트는 hello hello 콘텐츠와 함께 /usr/local/sbin/azure_crypt_key.sh, 파일을 만듭니다. Azure에서 사용 하는 hello 암호 파일 이름 이므로 주의 toohello KeyFileName, 지불 합니다.

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. Hello crypt 구성에서 변경 */등/crypttab*합니다. 다음과 같이 표시되어야 합니다.
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. 편집 하는 경우 *azure_crypt_key.sh* Windows에서 복사한 실행 tooLinux `dos2unix /usr/local/sbin/azure_crypt_key.sh`합니다.

4. Toohello 스크립트 실행 권한을 추가 합니다.
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. 줄을 추가하여 */etc/initramfs-tools/modules*를 편집합니다.
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. 실행 `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` 적용 합니다.

7. 이제 VM hello를 프로 비전 해제할 수 있습니다.

 ![Ubuntu 16.04 설치](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. Toohello 다음 단계를 계속 하 고 [VHD 업로드](#upload-encrypted-vhd-to-an-azure-storage-account) 를 Azure로 합니다.

##### <a name="opensuse-132"></a>openSUSE 13.2
tooconfigure hello 배포 설치 중에 암호화 다음 hello지 않습니다.
1. Hello 디스크를 분할 하는 경우 선택 **볼륨 그룹 암호화**, 암호를 입력 합니다. 이 hello 암호 tooyour 주요 자격 증명 모음을 업로드 합니다.

 ![openSUSE 13.2 설치](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. 암호를 사용 하 여 VM hello를 부팅 합니다.

 ![openSUSE 13.2 설치](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. 준비 tooAzure hello 지침에 따라 업로드 하기 위한 VM hello [SLES 또는 openSUSE 가상 컴퓨터를 Azure에 대 한 준비](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131)합니다. Hello 마지막 단계 (프로 비전 해제 hello VM)를 아직 실행 하지 마십시오.

Azure 통해 암호화 toowork tooconfigure 다음 hello지 않습니다.
1. Hello /etc/dracut.conf 편집한 hello 다음 줄 추가:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. Hello hello 끝날 때이 줄 주석 /usr/lib/dracut/modules.d/90crypt/module-setup.sh 파일:
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. Hello 다음 hello 파일 /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh hello 맨 앞에 줄을 추가 합니다.
 ```
    DRACUT_SYSTEMD=0
 ```
다음 항목을 그 아래 항목으로 바꿉니다.
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
to:
```
    if [ 1 ]; then
```
4. /Usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh 편집한 너무 추가할 "# 열기 LUKS 장치":

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. 실행 `/usr/sbin/dracut -f -v` tooupdate hello initrd 합니다.

6. 프로 비전 해제할 수 이제 VM hello 및 [VHD 업로드](#upload-encrypted-vhd-to-an-azure-storage-account) 를 Azure로 합니다.

##### <a name="centos-7"></a>CentOS 7
tooconfigure hello 배포 설치 중에 암호화 다음 hello지 않습니다.
1. 디스크를 분할할 때 **내 데이터 암호화**를 선택합니다.

 ![CentOS 7 설치](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. 루트 파티션에 대해 **암호화**가 선택되어 있는지 확인합니다.

 ![CentOS 7 설치](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. 암호를 제공합니다. 이 hello 암호 tooyour 주요 자격 증명 모음을 업로드 합니다.

 ![CentOS 7 설치](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. Hello VM 부팅 하 고 암호를 요구 하는 경우 3 단계에서 제공 하는 hello 암호를 사용 합니다.

 ![CentOS 7 설치](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. hello "CentOS 7.0 이상" 지침을 사용 하 여 Azure에 업로드 하기 위한 준비 hello VM [CentOS 기반 가상 컴퓨터를 Azure에 대 한 준비](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70)합니다. Hello 마지막 단계 (프로 비전 해제 hello VM)를 아직 실행 하지 마십시오.

6. 프로 비전 해제할 수 이제 VM hello 및 [VHD 업로드](#upload-encrypted-vhd-to-an-azure-storage-account) 를 Azure로 합니다.

Azure 통해 암호화 toowork tooconfigure 다음 hello지 않습니다.

1. Hello /etc/dracut.conf 편집한 hello 다음 줄 추가:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. Hello hello 끝날 때이 줄 주석 /usr/lib/dracut/modules.d/90crypt/module-setup.sh 파일:
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. Hello 다음 hello 파일 /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh hello 맨 앞에 줄을 추가 합니다.
```
    DRACUT_SYSTEMD=0
```
다음 항목을 그 아래 항목으로 바꿉니다.
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
to
```
    if [ 1 ]; then
```
4. /Usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh를 편집 하 고 hello "# 열기 LUKS 장치" 뒤에이 추가 합니다.
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. Hello 실행 "/ usr/sbin/dracut-f-v" tooupdate hello initrd 합니다.

![CentOS 7 설치](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a>암호화 된 VHD tooan Azure 저장소 계정에 업로드
BitLocker 암호화 또는 DM Crypt 암호화 사용 하도록 설정한 후 hello 로컬 VHD 요구 업로드 toobe tooyour 저장소 계정을 암호화 됩니다.

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a>Hello 미리 암호화 된 VM tooyour 주요 자격 증명 모음에 대 한 hello 디스크 암호화 암호를 업로드 합니다.
이전에 가져온 hello 디스크 암호화 암호 키 저장소의 암호로 업로드 해야 합니다. hello 주요 자격 증명 모음 toohave 디스크 암호화 및 Azure AD 클라이언트에서 사용 하도록 권한이 필요 합니다.

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a>KEK로 암호화되지 않은 디스크 암호화 암호
키 저장소를 사용 하 여의 hello 보안을 tooset [집합 AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret)합니다. Windows 가상 컴퓨터를 설정한 경우 hello bek base64 문자열로 인코딩된 파일과 tooyour 주요 자격 증명 모음 hello를 사용 하 여 업로드 된 다음 `Set-AzureKeyVaultSecret` cmdlet. Linux 용 hello 암호 base64 문자열로 인코딩한 다음 toohello 주요 자격 증명 모음을 업로드 합니다. 또한 있는지 확인 하십시오 hello 키 자격 증명 모음에 hello 암호를 만들 때 해당 hello 태그 설정 됩니다.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

사용 하 여 hello `$secretUrl` hello에 대 한 다음 단계에서 [KEK를 사용 하지 않고 hello OS 디스크를 연결](#without-using-a-kek)합니다.

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a>KEK로 암호화된 디스크 암호화 암호
Hello 비밀 toohello 자격 증명 모음 키를 업로드 하기 전에 키 암호화 키를 사용 하 여 선택적으로 암호화할 수 있습니다. 사용 하 여 hello 래핑 [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst hello 키 암호화 키를 사용 하 여 hello 보안을 암호화 합니다. hello이 wrap 작업의 출력은 hello를 사용 하 여 비밀으로 업로드할 수 있습니다 하는 base64 인코딩된 URL 문자열을 [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

사용 하 여 `$KeyEncryptionKey` 및 `$secretUrl` hello에 대 한 다음 단계에서 [KEK를 사용 하 여 hello OS 디스크를 연결](#using-a-kek)합니다.

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a>OS 디스크를 연결할 때 비밀 URL 지정
#### <a name="without-using-a-kek"></a>KEK 사용 안 함
Toopass hello OS 디스크를 연결 하는 동안 필요한 `$secretUrl`합니다. hello URL hello "디스크 암호화 암호는 KEK를 사용 하 여 암호화 되지 않습니다." 섹션에 생성 되었습니다.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a>KEK 사용
Hello OS 디스크를 연결할 경우 전달 `$KeyEncryptionKey` 및 `$secretUrl`합니다. hello URL hello "디스크 암호화 암호는 KEK를 사용 하 여 암호화 되지 않습니다." 섹션에 생성 되었습니다.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a>이 가이드 다운로드
Hello에서이 가이드를 다운로드할 수 있습니다 [TechNet 갤러리](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)합니다.

## <a name="for-more-information"></a>Blob에 대한 자세한 내용은
[Azure PowerShell를 사용하여 Azure Disk Encryption 탐색 - 1부](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[Azure PowerShell를 사용하여 Azure Disk Encryption 탐색 - 2부](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)

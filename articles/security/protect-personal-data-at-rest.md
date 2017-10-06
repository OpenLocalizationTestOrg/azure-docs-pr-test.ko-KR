---
title: "aaaAzure 암호화와 함께 저장 된 상태의 개인 데이터 보호 | Microsoft Docs"
description: "이 문서는 Azure tooprotect 개인 데이터를 사용 하는 데 도움이 되는 시리즈의 일부"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a>Azure 암호화 기술: 암호화로 미사용 개인 데이터 보호

이 문서를 사용 하 여 이해 하 고 Azure 암호화 기술을 toosecure 데이터를 사용 하 여 저장 된 상태의 수 있습니다.

미사용 데이터 암호화 toomeet 규정 준수와 데이터 개인 정보 보호 요구 사항 및 모범 사례 tooprotect 중요 하거나 개인적인 데이터 반드시 필요 합니다.
휴지 암호화 hello 디스크에 있는 경우 데이터는 암호화 되도록 하 여 hello 암호화 되지 않은 데이터에 액세스 하지 못하도록 설계 된 tooprevent hello 공격자가입니다.

## <a name="scenario"></a>시나리오 

Hello 미국에서에서 본사는 큰 크루즈 회사 hello 영국 제도 뿐만 아니라 hello 지중해 발트어 바다에서 해당 작업 toooffer 일정 확장 합니다. toosupport 이탈리아, 독일, 덴마크, hello 영국에 따라 여러 개의 더 작은 크루즈 줄 획득 비슷한 작업

hello 회사 hello 클라우드에서 Microsoft Azure toostore 회사 데이터를 사용합니다. 이 수 직원 또는 고객 정보가 다음과 같은 포함

- 주소
- 전화 번호
- 납세자 번호
- 의료 보험 정보
- 신용 카드 정보

hello 회사 필요로 하는 데이터 액세스 가능한 toothose 부서 이와 동시에 직원 및 고객 데이터의 hello 개인 정보를 보호 해야 합니다. 액세스할 수 있어야 합니다.

hello 크루즈 줄에는 현재 및 과거 고객과 개인 정보 tootrack 관계를 포함 하는 보상 및 충성도 프로그램 멤버의 큰 데이터베이스 유지 관리 합니다.

### <a name="problem-statement"></a>문제 설명

hello 회사 (예: 부서 급여 및 예약) 해야 하는 데이터 액세스 가능한 toothose 부서 이와 동시에 직원의 고 고객의 개인 데이터의 hello 개인 정보를 보호 해야 합니다. 이 개인 데이터 hello 제어 기업 데이터 센터 외부에서 저장 되 고 hello 회사의 물리적으로 제어 아래에 있지 않습니다.

### <a name="company-goal"></a>회사 목표

다중 계층된 방어 보안 전략의 일부로, 클라우드 저장소에 상주 하는 것을 포함 하 여 개인 데이터가 포함 된 모든 데이터 원본의 암호화는 회사 목표 tooensure 것 합니다. Persons 이득 액세스 toohello 개인 데이터를 권한이 없으면 렌더링 하 고 읽을 수 없는 형식에서 이어야 합니다. 암호화를 적용하는 경우 사용자 또는 관리자에게 쉽고 투명해야 합니다.

## <a name="solutions"></a>솔루션

Azure 서비스는 여러 도구와 기술 toohelp 제공 암호화 하 여 저장 된 상태의 개인 데이터를 보호 합니다.

### <a name="azure-key-vault"></a>Azure 키 자격 증명 모음

[Azure 키 자격 증명 모음](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) hello 키에서 Azure 서비스의 tooencrypt 데이터를 사용 하 고는 hello 권장 키 저장소 및 관리 솔루션에 대 한 안전한 저장소를 제공 합니다. 암호화 키 관리는 필수 toosecuring 저장 된 데이터입니다.

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a>개인 데이터를 암호화 하는 Azure 키 자격 증명 모음 tooprotect 키를 사용 하려면 어떻게 해야 합니까?

Azure 키 자격 증명 모음 toouse 구독 tooan Azure 계정이 필요합니다. Azure PowerShell도 설치해야 합니다. 단계는 PowerShell cmdlet toodo hello 다음을 사용 하 여 포함 합니다.

1. Tooyour 구독 연결

2. 키 자격 증명 모음 만들기

3. 키 또는 키 자격 증명 모음 보안 toohello 추가

4. Hello 주요 자격 증명 모음을 사용 하 여 Azure Active directory는 응용 프로그램 등록

5. Hello 응용 프로그램 toouse hello 키 또는 암호를 권한 부여

주요 자격 증명 모음 toocreate hello 새로 AzureRmKeyVault PowerShell CmDlt을 사용 합니다. 자격 증명 모음 이름, 리소스 그룹 이름 및 지리적 위치를 할당합니다. 다른 Cmdlet 통해 키를 관리 하는 경우 자격 증명 모음 이름 hello를 사용 합니다. Hello REST API를 통해 hello 자격 증명 모음을 사용 하는 응용 프로그램 hello 자격 증명 모음 URI를 사용 합니다.

Azure Key Vault에서는 소프트웨어로 보호된 키를 제공하거나 .PFX 파일에서 기존 키를 가져올 수 있습니다. 또한 hello 자격 증명 모음에 암호를 저장할 수 있습니다.

로컬 HSM에 키를 생성 하 고 hello HSM 경계를 종료 하는 hello 키 없이 tooHSMs hello 키 자격 증명 모음 서비스에에서 전송할 수도 있습니다.

단계를 hello Azure 키 자격 증명 모음을 사용 하는 자세한 방법은 다음과 [Azure 키 자격 증명 모음 시작 합니다.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)

Azure Key Vault와 함께 사용되는 PowerShell cmdlet 목록은 [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0)를 참조하세요.

### <a name="azure-disk-encryption-for-windows"></a>Windows용 Azure Disk Encryption

[Windows 및 Linux IaaS VM용 Azure Disk Encryption](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)은 Azure 가상 컴퓨터에서 미사용 개인 데이터를 보호하고 Azure Key Vault와 통합합니다. Azure 디스크 암호화를 사용 하 여 [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) windows에서 및 [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) OS 및 hello 데이터 디스크를 둘 다 hello Linux tooencrypt 합니다. Azure Disk Encryption은 Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, Windows 8 및 Windows 10 클라이언트에서 지원됩니다.

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a>Azure 디스크 암호화 tooprotect 개인 데이터를 사용 하려면 어떻게 해야 합니까?

Azure 디스크 암호화 toouse 구독 tooan Azure 계정이 필요합니다. Windows 용 tooenable Azure 디스크 암호화와 Linux Vm의 경우, 다음 hello지 않습니다.

1. Hello Azure 디스크 암호화 리소스 관리자 템플릿, PowerShell 또는 hello 명령줄 인터페이스 (CLI) tooenable 디스크 암호화를 사용 하 고 암호화 구성을 지정 키를 누릅니다. 

2. 주요 자격 증명 모음에서 Azure 플랫폼 tooread hello 암호화 자료 toohello를 액세스 하는 권한 부여 합니다.

3. Azure Active Directory (AAD) 응용 프로그램 identity toowrite hello 암호화 키 재료 tooyour 키 자격 증명 모음을 제공 합니다.

Azure VM hello 및 hello 주요 자격 증명 모음 구성 업데이트 하 고 암호화 된 VM을 설정 합니다.

Azure 디스크 암호화 하 여 주요 자격 증명 모음 toosupport을 설정할 때 추가 보안 및 암호화 된 가상 컴퓨터의 toosupport 백업에 대 한 키 암호화 키 KEK ()를 추가할 수 있습니다.

![](media/protect-personal-data-at-rest/create-key.png)

특정 배포 시나리오 및 사용자 환경에 대한 자세한 지침은 [Windows 및 Linux IaaS VM용 Azure Disk Encryption](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)에 포함되어 있습니다.

### <a name="azure-storage-service-encryption"></a>Azure 저장소 서비스 암호화

[Azure 저장소 서비스 암호화 SSE () 미사용 데이터에 대 한](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) 하면 보호 하 고 데이터 toomeet 조직 보안 및 규정 준수 행 결과 보호 합니다. Azure 저장소는 자동으로 256 비트 AES 암호화 이전 toopersisting toostorage를 사용 하 여 데이터를 암호화 하 고 이전 tooretrieval 암호를 해독 합니다. 이 서비스는 Azure Blob 및 파일에서 사용할 수 있습니다.

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a>저장소 서비스 암호화 tooprotect 개인 데이터를 사용 하려면 어떻게 해야 합니까?

저장소 서비스 암호화 tooenable 다음 hello지 않습니다.

1. Azure 포털 hello에 로그인 합니다.

2. 저장소 계정을 선택합니다.

3. 설정에서 hello Blob 서비스 섹션에서 암호화를 선택 합니다.

4. Hello 파일 서비스 섹션에서 암호화를 선택 합니다.

Hello 암호화 설정을 클릭 한 후 사용 하도록 설정 하거나 저장소 서비스 암호화를 사용 하지 않도록 설정할 수 있습니다.

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

새 데이터가 암호화됩니다. 이 저장소 계정에 있는 기존 파일의 데이터는 암호화되지 않은 상태로 유지됩니다.

암호화를 사용 하도록 설정한 후 hello 메서드를 다음 중 하나를 사용 하 여 데이터 toohello 저장소 계정에 복사 합니다.

1. Blob 또는 hello 사용 하 여 파일 복사 [AzCopy 명령 줄 유틸리티](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy)합니다.

2. [SMB를 사용 하 여 파일 공유를 탑재](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) Robocopy toocopy 파일과 같은 유틸리티를 사용할 수 있도록 합니다.

3. Blob 또는 파일 데이터 tooand 사이 또는 blob 저장소에서 사용 하 여 저장소 계정을 복사 [.NET 등의 저장소 클라이언트 라이브러리](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs)합니다.

4.  사용 하 여 한 [저장소 탐색기](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload 암호화가 설정 되어 tooyour 저장소 계정 blob입니다.

### <a name="transparent-data-encryption"></a>투명한 데이터 암호화

투명 한 데이터 암호화 (TDE)는의 기능이 며 SQL Azure는 기준인 hello 데이터베이스 및 서버 수준 모두에 데이터를 암호화할 수 있습니다. TDE는 이제 기본적으로 새로 만든 모든 데이터베이스에서 사용하도록 설정됩니다. TDE는 실시간 I/O 암호화 및 hello 데이터 및 로그 파일의 암호 해독을 수행합니다.

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a>TDE tooprotect 개인 데이터를 사용 하려면 어떻게 해야 합니까?

Hello REST API를 사용 하 여 또는 PowerShell을 사용 하 여 hello Azure 포털을 통해 TDE를 구성할 수 있습니다. hello Azure 포털을 사용 하 여 기존 데이터베이스에 TDE tooenable 다음 hello지 않습니다.

1. 방문 hello Azure 포털에서 <https://portal.azure.com> 및 Azure 관리자 또는 참가자 계정으로 로그인 합니다.

2. Hello 왼쪽된 배너에서 tooBROWSE를 클릭 한 다음 SQL 데이터베이스를 클릭 합니다.

3. Hello 왼쪽된 창에서 선택한 SQL 데이터베이스, 사용자 데이터베이스를 클릭 합니다.

4. Hello 데이터베이스 블레이드 모든 설정을 클릭 합니다.

5. Hello 설정 블레이드에서에서 투명 한 데이터 암호화 부분 tooopen hello 투명 한 데이터 암호화 블레이드를 클릭 합니다.

6. Hello 데이터 암호화 단추 tooOn 이동한 다음 (hello 페이지의 위쪽 hello) 저장을 클릭 hello 데이터 암호화 블레이드에서 tooapply hello 설정 합니다. hello 암호화 상태는 hello 투명 한 데이터 암호화의 진행률과를 hello 비슷합니다.

![데이터 암호화를 사용하도록 설정](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

Hello 문서에서 TDE로 보호 된 데이터베이스를 암호 해독에 방법과 tooenable TDE 수 발견 하는 방법에 대 한 지침 [Azure SQL 데이터베이스를 사용한 투명 한 데이터 암호화 합니다.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)

## <a name="summary"></a>요약

hello 회사 hello Azure 클라우드에에서 저장 된 개인 데이터를 암호화할 해당 목표를 달성할 수 있습니다. Azure 디스크 암호화를 사용 하 여 이렇게 하려면 너무 전체 볼륨을 보호 합니다. 여기에 hello 운영 체제 파일 및 개인 식별이 가능한 정보 및 기타 중요 한 데이터를 저장 된 데이터 파일을 모두 포함 될 수 있습니다. Azure 저장소 서비스 암호화 blob 및 파일에 저장 되어 있는 개인 데이터를 사용 하는 tooprotect 될 수 있습니다. Azure SQL 데이터베이스에 저장된 데이터의 경우 투명한 데이터 암호화는 무단 노출로부터 개인 정보를 보호합니다.

Azure에서 사용 되는 tooencrypt 데이터 있는 tooprotect hello 키는 hello 회사는 Azure 키 자격 증명 모음 사용. 이 hello 키 관리 프로세스를 간소화 하 고 활성화 hello에 액세스 하 고 개인 데이터 암호화 키의 회사 toomaintain 제어 합니다.

## <a name="next-steps"></a>다음 단계

- [Azure Disk Encryption 문제 해결 가이드](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [Azure 가상 컴퓨터 암호화](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [Azure Data Lake Store의 데이터 암호화](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [미사용 Azure Cosmos DB 데이터베이스 암호화](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)

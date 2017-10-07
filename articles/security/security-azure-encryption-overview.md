---
title: "aaaAzure 암호화 개요 | Microsoft Docs"
description: "Azure에서 다양한 암호화 옵션에 대해 알아보기"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/18/2017
ms.author: barclayn
ms.openlocfilehash: ef9ab46de32b857e99e8fe628a61386b95cf197f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-overview"></a>Azure 암호화 개요

이 문서에서는 Microsoft Azure에서 암호화가 사용되는 방식에 대한 개요를 제공합니다. 미사용 데이터 암호화, 암호화를 포함 하 여 비행 및 키 자격 증명 모음 키 관리에서 암호화의 주요 영역 hello를 처리 합니다. 각 섹션에는 더 자세한 정보에 대한 링크가 포함됩니다.

## <a name="encryption-of-data-at-rest"></a>미사용 데이터 암호화

미사용 데이터에는 모든 디지털 형식으로 된, 실제 미디어의 영구 저장소에 상주하는 정보가 포함됩니다. 여기에는 자기 또는 광학 미디어의 파일, 보관된 데이터 및 데이터 백업이 포함됩니다. Microsoft Azure는 다양 한 데이터 저장소 솔루션 toomeet 파일, 디스크, blob 및 테이블 저장소를 비롯 한 다른 요구를 제공 합니다. Microsoft 암호화 tooprotect 제공 [Azure SQL 데이터베이스](../sql-database/sql-database-technical-overview.md), [CosmosDB](../cosmos-db/introduction.md), 및 Azure 데이터 레이크 합니다.

Hello Azure 소프트웨어-as a Service (SaaS) 플랫폼으로-서비스 (PaaS)에서 미사용 데이터 암호화를 서비스에 대 한 사용할 수 및 인프라-as a Service (IaaS) 클라우드 모델. 이 문서를 요약 한 리소스 toohelp Azure의 암호화 옵션을 사용 합니다.

Azure에서 미사용 데이터는 암호화 하는 방법에 대 한 설명은 자세한 이라는 hello 문서를 참조 하십시오. [Azure 데이터--휴지 암호화](azure-security-encryption-atrest.md)

## <a name="azure-encryption-models"></a>Azure 암호화 모델

Azure는 서비스 관리 키를 사용하는 서버 쪽 암호화, Azure Key Vault의 고객 관리 키 사용 또는 고객 제어 하드웨어의 고객 관리 키 사용과 같은 다양한 암호화 모델을 지원합니다. 클라이언트 쪽 암호화를 사용 하면 toomanage 및 저장소 키 하면 온-프레미스 또는 다른 위치를 보호 합니다.

### <a name="client-side-encryption"></a>클라이언트 쪽 암호화

클라이언트 쪽 암호화는 Azure 외부에서 수행됩니다. 클라이언트 쪽 암호화에는 다음이 포함됩니다.

- Hello 고객의 데이터 센터에서 실행 하는 응용 프로그램 또는 서비스 응용 프로그램 암호화 된 데이터
- Azure에서 수신될 때 이미 암호화된 데이터입니다.

클라이언트 쪽 암호화와 함께 hello 클라우드 서비스 공급자 액세스 toohello 암호화 키가 없다고와이 데이터를 암호 해독할 수 없습니다. Hello 키의 전체 제어를 유지 합니다.

### <a name="server-side-encryption"></a>서버 쪽 암호화

세 가지 서버 쪽 암호화 모델 hello 요구 사항에 따라 선택할 수 있는 다른 키 관리 특성을 제공 합니다.

- **서비스 관리 키**는 낮은 오버헤드로 제어와 편의성을 모두 제공합니다.

- **고객 관리 키** 제어할 수 hello 키, hello 기능 toobring를 포함 하 여 고유한 키 (BYOK) 또는 toogenerate 새로 합니다.

- **서비스 관리 키에서 ccustomer controlledhardware에** Microsoft의 제어 범위 밖에 있는 소유 리포지토리에 toomanage 키 수 있도록 합니다. 이를 HYOK(Host Your Own Key)라고 합니다. 그러나 구성이 복잡하고 대부분의 Azure 서비스는 이 모델을 지원하지 않습니다.

### <a name="azure-disk-encryption"></a>Azure 디스크 암호화

사용 하 여 Windows 및 Linux 가상 컴퓨터를 보호할 수 있습니다 [Azure 디스크 암호화](azure-security-disk-encryption.md), hello를 사용 하 여 [Windows BitLocker](https://technet.microsoft.com/library/cc766295(v=ws.10).aspx) 기술 및 Linux [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) tooprotect 운영 체제 디스크 및 전체 볼륨 암호화 된 데이터 디스크.

사용자의 [Azure Key Vault](../key-vault/key-vault-whatis.md) 구독에서 암호화 키 및 비밀이 보호됩니다. 백업 및 hello Azure 백업 서비스를 사용 하 여 hello KEK 구성을로 암호화 된 암호화 된 Vm을 복원할 수 있습니다.

### <a name="azure-storage-service-encryption"></a>Azure Storage 서비스 암호화

서버 쪽 및 클라이언트 쪽 시나리오에서 Azure 저장소의 미사용 데이터(Blob 및 파일)를 암호화할 수 있습니다.

[Azure 저장소 서비스 암호화](../storage/storage-service-encryption.md) 저장 하 고 자동으로 만드는 완전히 투명 하 게 사용자가 처리 하는 hello를 검색 하는 경우 해독 하기 전에 (SSE) 데이터를 자동으로 암호화할 수 있습니다. 저장소 서비스 암호화 256 비트를 사용 하 여 [AES 암호화](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), hello 중 하나를 사용할 수는 가장 강력한 블록 암호화 하며 암호화, 해독 및 투명 한 방식에서 키 관리를 처리 합니다.

### <a name="client-side-encryption-of-azure-blobs"></a>Azure Blob의 클라이언트 쪽 암호화

다양한 방법으로 Azure Blob의 클라이언트 쪽 암호화를 수행할 수 있습니다.

클라이언트 응용 프로그램 이전 toouploading에서.NET NuGet 패키지 tooencrypt 데이터에 대 한 hello Azure 저장소 클라이언트 라이브러리를 사용할 수 있는 것 tooAzure 저장소입니다.

에 대 한 자세한 toolearn 및.NET NuGet 패키지용 Azure 저장소 클라이언트 라이브러리 다운로드 hello 라는 hello 문서를 참조 하십시오. [8.3.0 Windows Azure 저장소](https://www.nuget.org/packages/WindowsAzure.Storage)

클라이언트 쪽 암호화를 사용 하 여 Azure 키 자격 증명 데이터 일회성 대칭 콘텐츠 암호화 키 (CEK) hello Azure 저장소 클라이언트 SDK에 의해 생성 된를 사용 하 여 암호화 됩니다. hello CEK는 대칭 키 또는 비대칭 키 쌍 중 일 수 있는 암호화 키 KEK (키)를 사용 하 여 암호화 됩니다. 로컬로 관리하거나 Azure Key Vault에 저장할 수 있습니다. hello 암호화 된 데이터는 다음 tooAzure 저장소 서비스에 업로드 합니다.

toolearn 클라이언트 쪽 암호화 Azure 키 자격 증명에 대 한 자세한 방법 tooinstructions 시작, 라는 hello 문서를 참조 하 고 [자습서: 암호화 및 Azure 키 자격 증명 모음을 사용 하 여 Microsoft Azure 저장소에서 blob를 암호 해독](../storage/storage-encrypt-decrypt-blobs-key-vault.md)

마지막으로, toohello 클라이언트를 다운로드할 때 데이터 저장소, tooAzure 및 toodecrypt hello 데이터를 업로드 하기 전에 Java tooperform 클라이언트 쪽 암호화에 대 한 hello Azure 저장소 클라이언트 라이브러리를 사용할 수도 있습니다. 또한 이 라이브러리는 저장소 계정 키 관리를 위해 [Azure Key Vault](https://azure.microsoft.com/services/key-vault/)와의 통합을 지원합니다.

### <a name="encryption-of-data-at-rest-with-azure-sql-database"></a>Azure SQL 데이터베이스에서 미사용 데이터 암호화

[Azure SQL Database](../sql-database/sql-database-technical-overview.md)는 관계형 데이터, 공간, JSON 및 XML과 같은 구조를 지원하는 Microsoft Azure의 범용 관계형 데이터베이스 서비스입니다. Azure SQL hello 투명 한 데이터 암호화 (TDE) 기능을 통해 서버 쪽 암호화와 hello 항상 암호화 기능을 통해 클라이언트 쪽 암호화를 지원합니다.

#### <a name="transparent-data-encryption"></a>투명한 데이터 암호화

[TDE 투명 한 데이터 암호화](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde) 가 사용 되는 tooencrypt [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016), [Azure SQL 데이터베이스](../sql-database/sql-database-technical-overview.md), 및 [Azure SQL 데이터 웨어하우스](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) 실시간으로 데이터 파일 복구 하는 동안 hello 데이터베이스 부트 레코드에 저장 되는 데이터베이스 암호화 키 (DEK)를 사용 합니다.

TDE는 AES 및 3DES 암호화 알고리즘을 사용하여 데이터 및 로그 파일을 보호합니다. Hello 데이터베이스 파일의 암호화 hello 페이지 수준에서 수행 됩니다. 암호화 된 데이터베이스에 hello 페이지 toodisk 기록 되기 전에 암호화 됩니다 및 메모리에 읽게 때 암호가 해독 됩니다. 기본적으로 TDE는 이제 새로 만든 Azure SQL 데이터베이스에서 사용하도록 설정됩니다.

#### <a name="always-encrypted"></a>상시 암호화

hello [항상 암호화](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine) 기능에 SQL Azure를 통해 Azure SQL 데이터베이스에서 클라이언트 응용 프로그램 이전 toostoring 내 tooencrypt 데이터 및 온-프레미스 데이터베이스 관리 toothird tooenable 위임을 사용 하면 당사자 및 분리를 소유 하 고 hello 데이터 및 관리 하지만 액세스 tooit 수 없는 사용자에 게 볼 수 있는 유지 관리 합니다.

#### <a name="cellcolumn-level-encryption"></a>셀/열 수준 암호화

Azure SQL 데이터베이스 TRANSACT-SQL을 사용 하 여 데이터의 tooapply 대칭 암호화 tooa 열을 수 있습니다. 이 라고 [셀 수준 암호화 또는 열 수준 암호화](https://docs.microsoft.com/sql/relational-databases/security/encryption/encrypt-a-column-of-data) CLE ()를 사용할 수 있으므로 tooencrypt 특정 열 이나 특정 셀 데이터의 서로 다른 암호화 키를 사용 합니다. 이를 통해 페이지에서 데이터를 암호화하는 TDE보다 더 세분화된 암호화 기능이 제공됩니다.

CLE에는 인증서의 공개 키 hello 또는 3DES를 사용 하 여 암호에는 대칭 또는 비대칭 키를 사용 하 여 tooencrypt 데이터를 사용할 수 있는 기본 제공 함수가 있습니다.

### <a name="cosmos-db-database-encryption"></a>Cosmos DB 데이터베이스 암호화

[Azure Cosmos DB](../cosmos-db/database-encryption-at-rest.md)는 전 세계에 배포된 Microsoft의 멀티모델 데이터베이스입니다. 기본적으로 비휘발성 저장소 (솔리드 스테이트 드라이브)의 Cosmos DB에 저장 하는 사용자 데이터는 암호화 없는 컨트롤 tooturn 켜기 / 끄기입니다. 미사용 암호화는 보안 키 저장소 시스템, 암호화된 네트워크 및 암호화 API를 비롯한 수많은 보안 기술을 사용하여 구현되었습니다. 암호화 키는 Microsoft에서 관리하며 Microsoft의 내부 지침에 따라 순환됩니다.

### <a name="at-rest-encryption-in-azure-data-lake"></a>Azure Data Lake의 미사용 암호화

[Azure 데이터 레이크](../data-lake-store/data-lake-store-encryption.md) 는 모든 종류의 데이터는 기업 전체의 저장소 요구 사항이 나 스키마의 단일 위치 이전 tooany 형식 정의에서 수집 합니다. Azure 데이터 레이크 저장소 지원 "에 기본적으로" hello 계정 만드는 동안 설정 된 미사용 데이터의 투명 한 암호화 합니다. 기본적으로 데이터 레이크 저장소, hello 키를 관리 하지만 hello 옵션 toomanage 있는 해당 사용자가 직접 합니다.

세 가지 유형의 키는 데이터 암호화 및 해독에 사용 됩니다: 마스터 암호화 키 (MEK), 데이터 암호화 키 (DEK) 및 블록 암호화 키 (BEK) hello 합니다. hello MEK 사용 되는 tooencrypt hello DEK 영구 미디어에 저장 된 이며 hello BEK DEK hello 및 hello 데이터 블록에서 파생 됩니다. 고유한 키를 관리 하는 경우에 hello MEK 회전할 수 있습니다.

## <a name="encryption-of-data-in-transit"></a>전송 중 데이터 암호화

Azure에서는 한 위치 tooanother에서 개인 데이터를 유지 하기 위한 여러 메커니즘을 제공 합니다.

### <a name="tlsssl-encryption-in-azure"></a>Azure에서 TLS/SSL 암호화

Microsoft hello를 사용 하 여 [Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) hello 클라우드 서비스와 고객 간에 이동할 때 tooprotect 데이터 프로토콜입니다. Microsoft 데이터 센터 tooAzure 서비스를 연결 하는 클라이언트 시스템 TLS 연결을 협상 합니다. TLS는 강력한 인증, 메시지 개인 정보 및 무결성(메시지 변조, 가로채기 및 위조의 검색 가능), 상호 운용성, 알고리즘 유연성, 배포 및 사용 편의성을 제공합니다.

[PFS(Perfect Forward Secrecy)](https://en.wikipedia.org/wiki/Forward_secrecy)는 고유한 키로 고객의 클라이언트 시스템 및 Microsoft의 클라우드 서비스 간의 연결을 보호합니다. 또한 연결은 RSA 기반 2,048비트 암호화 키 길이를 사용합니다. 이 조합은 쉽게 없는 다른 사용자에 대 한 toointercept 및 액세스 데이터를 전송 중인 합니다.

### <a name="azure-storage-transactions"></a>Azure Storage 트랜잭션

Hello Azure 포털을 통해 Azure 저장소 상호 작용 하는 경우 모든 트랜잭션을 수행 HTTPS를 통해. Azure 저장소와 HTTPS toointeract 통해 hello 저장소 REST API를 사용할 수도 있습니다. Hello 저장소 계정에 필요한 보안 전송을 사용 하 여 저장소 계정에 hello REST Api tooaccess 개체를 호출할 때 HTTPS hello 사용을 적용할 수 있습니다.

공유 액세스 서명 ([SAS](../storage/storage-dotnet-shared-access-signature-part-1.md)), tooAzure 저장소 개체에 액세스, 공유 액세스 서명을 사용 하는 경우 HTTPS 프로토콜을 사용할 수만 해당 hello 옵션 toospecify 포함 toodelegate 사용된 될 수 있습니다. 이렇게 하면 모든 링크와 SAS 토큰을 보내는 사용자가 hello 적절 한 프로토콜입니다.

[SMB 3.0](https://technet.microsoft.com/library/dn551363(v=ws.11).aspx#BKMK_SMBEncryption) 사용 되는 tooaccess Azure 파일 공유에 암호화를 지 원하는 및 Windows Server 2012 R2, Windows 8, Windows 8.1 및 지역 간 액세스를 허용 하는 Windows 10에서 사용할 수 있으며 hello 바탕 화면에도 액세스 합니다.

클라이언트 쪽 암호화 데이터를 암호화 hello tooAzure 저장소 전송한 전에 hello 네트워크를 통해 전송할 때 암호화 되어 있도록 합니다.

### <a name="smb-encryption-over-azure-virtual-networks"></a>Azure Virtual Networks를 통해 SMB 암호화 

[SMB 3.0](https://support.microsoft.com/help/2709568/new-smb-3-0-features-in-the-windows-server-2012-file-server) tooprotect 변조 및 도청 공격 이상 버전에서 Windows Server 2012를 실행 하는 Azure Vm은 Azure 가상 네트워크를 통해 전송 되는 데이터를 암호화 하 여 전송 보안 기능 toomake 데이터 hello, 합니다. 관리자가 전체 서버 hello 또는 특정 공유에 대 한 SMB 암호화를 사용할 수 있습니다.

기본적으로, 공유 또는 서버에 SMB 암호화가 설정 된 후 SMB 3 클라이언트에만 허용 tooaccess 암호화 hello 공유 합니다.

## <a name="in-transit-encryption-in-azure-virtual-machines"></a>Azure Virtual Machines에서 전송 중 암호화

및 Windows를 실행 하는 Azure Vm 간에 전송 되는 데이터는 다양 한 방법으로 hello 연결 hello 특징에 따라에서 암호화 됩니다.

### <a name="rdp-sessions"></a>RDP 세션

연결 하 고 로그온 tooan hello를 사용 하 여 Azure VM 수 [원격 데스크톱 프로토콜](https://msdn.microsoft.com/library/aa383015(v=vs.85).aspx) (RDP)는 RDP 클라이언트가 설치 된 Mac 또는 Windows 클라이언트 컴퓨터에서 합니다. TLS에서 RDP 세션에서 hello 네트워크를 통해 전송 되는 데이터를 보호할 수 있습니다.

또한 Azure에서 원격 데스크톱 tooconnect tooa Linux VM을 사용할 수 있습니다.

### <a name="secure-access-toolinux-vms-with-ssh"></a>SSH 된 tooLinux Vm 액세스 보안

사용할 수 있습니다 [보안 셸](../virtual-machines/linux/ssh-from-windows.md) (SSH) tooconnect tooLinux Vm 원격 관리를 위해 Azure에서 실행 합니다. SSH는 안전하지 않은 연결에서 안전하게 로그인할 수 있도록 하는 암호화된 연결 프로토콜입니다. Azure에서 호스팅되는 Linux Vm에 대 한 hello 기본 연결 프로토콜입니다. 인증을 위해 SSH 키를 사용 하 여 hello에 대 한 암호 toolog 필요를 제거 됩니다. SSH는 인증에 공개/개인 키 쌍(비대칭 암호화)을 사용합니다.

## <a name="azure-vpn-encryption"></a>Azure VPN 암호화

TooAzure hello 네트워크를 통해 전송 중인 hello 데이터의 보안 터널 tooprotect hello 개인 만드는 가상 개인 네트워크를 통해 연결할 수 있습니다.

### <a name="azure-vpn-gateway"></a>Azure VPN Gateway

[Azure VPN 게이트웨이](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md) 암호화 사용된 toosend 트래픽 가상 네트워크와 공용 연결을 통해 온-프레미스 위치 간의 또는 가상 네트워크 간에 트래픽을 toosend 일 수 있습니다.

사이트 간 VPN은 전송 암호화에 [IPsec](https://en.wikipedia.org/wiki/IPsec)을 사용합니다. Azure VPN Gateway는 기본 제안 집합을 사용합니다. 특정 암호화 알고리즘 및 키 길이와 Azure VPN 게이트웨이 toouse 사용자 지정 IPsec/IKE 정책을 구성 하지 않고 수 있습니다 hello Azure 기본 정책 집합입니다.

### <a name="point-to-site-vpn"></a>지점 및 사이트 간 VPN

지점-사이트 Vpn 개별 클라이언트 컴퓨터를 허용할 tooan Azure 가상 네트워크에 액세스 합니다. [hello Secure Socket Tunneling Protocol](https://technet.microsoft.com/library/2007.06.cableguy.aspx) (SSTP) 사용 하는 toocreate hello VPN 터널 이며 방화벽 (hello 터널 HTTPS 연결으로 표시 됨)를 포함할 수 있습니다. 지점 및 사이트 간 연결에 사용자 고유의 내부 PKI 루트 CA를 사용할 수 있습니다.

인증서 인증 또는 PowerShell hello Azure 포털을 사용 하 여 지점-사이트 VPN 연결 tooa 가상 네트워크를 구성할 수 있습니다.

toolearn 지점-사이트 VPN 연결 tooAzure Vnet에 대 한 자세한 참조: [지점 및 사이트 연결 tooa VNet 구성 인증 인증을 사용 하 여: Azure 포털](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md) 및

[지점 및 사이트 연결 tooa VNet 구성 인증서 인증을 사용 하 여: PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="site-to-site-vpn"></a>사이트 간 VPN 

사이트 간 VPN 게이트웨이 연결에 사용 되는 tooconnect는 온-프레미스 IPsec/IKE (IKEv1 또는 IKEv2) VPN 터널을 통해 Azure 가상 네트워크 tooan 네트워크입니다. 이러한 종류의 연결에는 VPN 장치에 있는 온-프레미스 외부와 접한 공용 IP 주소 할당 tooit가 필요 합니다.

Hello Azure 포털, PowerShell 또는 Azure 명령줄 인터페이스 (CLI) hello를 사용 하 여 사이트 간 VPN 연결 tooa 가상 네트워크를 구성할 수 있습니다.

자세한 내용은 다음을 읽어보세요.

[Hello Azure 포털에서에서 사이트 간 연결을 만들려면](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

[사이트 간 연결 만들기](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

[CLI를 사용하여 사이트 간 VPN 연결로 가상 네트워크 만들기](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="in-transit-encryption-in-azure-data-lake"></a>Azure Data Lake의 전송 중 암호화

전송되는 데이터(즉, 동작 중인 데이터)는 항상 Data Lake Store에서 암호화됩니다. 또한 tooencrypting 데이터 사전 toostoring toopersistent 미디어 hello 데이터는 항상 전송에 보호 HTTPS를 사용 하 여 합니다. HTTPS는 hello hello 데이터 레이크 저장소 REST 인터페이스에 지원 되는 유일한 프로토콜입니다.

Azure 데이터 레이크에서 전송 중인 데이터의 암호화에 대해 자세히 toolearn 이라는 hello 문서를 참조 하십시오. [Azure 데이터 레이크 저장소의 데이터를 암호화 합니다.](../data-lake-store/data-lake-store-encryption.md)

## <a name="key-management-with-azure-key-vault"></a>Azure Key Vault으로 키 관리

적절 한 보호 및 관리 hello 키 없이 암호화 쓸모 없게 됩니다. Azure 주요 자격 증명은 관리 하 고 클라우드 서비스에서 사용 되는 액세스 tooencryption 키를 제어 하기 위한 Microsoft의 권장된 솔루션입니다. Tooservices 또는 Azure Active Directory 계정을 통해 toousers 권한 tooaccess 키를 할당할 수 있습니다.

Azure 키 자격 증명 모음에서는 조직 hello 필요 tooconfigure의 patch, 및 하드웨어 보안 모듈 (Hsm) 및 키 관리 소프트웨어를 유지 관리 합니다. Azure 키 자격 증명 모음과 Microsoft 표시 되지 않습니다. 키 및 응용 프로그램에 대 한 직접 액세스 toothem; 없는 합니다. 제어를 유지 합니다. 또한 HSM에서 키를 가져오거나 생성할 수도 있습니다.

## <a name="next-steps"></a>다음 단계

- [Azure 보안 개요](security-get-started-overview.md)
- [Azure 네트워크 보안 개요](security-network-overview.md)
- [Azure 데이터베이스 보안 개요](azure-database-security-overview.md)
- [Azure 가상 컴퓨터 보안 개요](security-virtual-machines-overview.md)
- [휴지 상태의 데이터 암호화](azure-security-encryption-atrest.md)
- [데이터 보안 및 암호화 모범 사례](azure-security-data-encryption-best-practices.md)

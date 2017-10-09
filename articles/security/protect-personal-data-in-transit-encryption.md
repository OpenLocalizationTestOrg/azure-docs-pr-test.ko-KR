---
title: "Azure에서 암호화를 사용 하 여 전송 중에 aaaProtect 개인 데이터 | Microsoft Docs"
description: "Azure tooprotect 개인 데이터에 암호화를 사용 하 여"
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
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a>Azure 암호화 기술: 암호화를 사용하여 전송 중인 개인 데이터 보호

이 문서는 이해 하 고 전송 중에 Azure 암호화 기술을 toosecure 데이터를 사용 하는 데 도움이 됩니다. 

개인 데이터의 개인 정보 보호 hello 보호 hello 네트워크를 통과할 때 여러 레이어로 된 방어 보안 전략의 필수적인 부분입니다. 전송 중에 암호화에는 디자인 된 tooprevent 전송 tooview 또는 사용 하 여 hello 데이터 수 없도록 차단 하는 공격자는입니다.

## <a name="scenario"></a>시나리오

Hello 미국에서 본사는 큰 크루즈 회사 hello 지중해, Adriatic, 발트어 바다 뿐 아니라 hello 영국 제도에서 해당 작업 toooffer 여정이 확장 합니다. toosupport 이탈리아를 더 작은 여러 크루즈 줄 획득 이러한 노력 독일, 덴마크 및 hello 영국 

hello 회사 hello 클라우드에서 Microsoft Azure toostore 회사 데이터를 사용합니다. 여기에는 전 세계 고객 기반의 이름, 주소, 전화 번호 및 신용 카드 정보와 같이 식별 가능한 개인 정보가 포함됩니다. 또한 모든 위치에 주소, 전화 번호, 세금 id 번호, 회사 직원에 대 한 의료 보험 정보 등 기존의 인적 자원 정보를 포함 합니다. hello 크루즈 줄에는 현재 및 과거 고객과 개인 정보 tootrack 관계를 포함 하는 보상 및 충성도 프로그램 멤버의 큰 데이터베이스 유지 관리 합니다.

Hello world 주변에 있는 여행사 및 원격 사무실 hello 회사에서에서 고객의 개인 데이터 hello 데이터베이스에 입력 됩니다. 고객 정보를 포함 하는 문서는 hello 네트워크 tooAzure 저장소를 통해 전송 됩니다.

## <a name="problem-statement"></a>문제 설명

hello 회사에서 고객의의 hello 개인 정보를 보호 해야 하 고 Azure 서비스에서 전송 tooand 동안 직원의 개인 데이터는 키를 누릅니다.

## <a name="company-goal"></a>회사 목표

회사 목표 tooensure hello 개인 데이터 디스크 끄기 때 암호화 됩니다. 권한 없는 사람이 가로챌 hello 디스크 외부 개인 데이터를 렌더링 하 고 읽을 수 없는 형식에서 이어야 합니다. 암호화를 적용하는 경우 사용자 또는 관리자에게 쉽고 완전히 투명해야 합니다.

## <a name="solutions"></a>솔루션

Azure 서비스는 여러 도구와 기술 toohelp 제공 전송 되는 개인 데이터를 보호 합니다.

### <a name="azure-storage"></a>Azure 저장소

Hello world, toohello Azure 데이터 센터에에서 모든 위치에 실제로 있을 수 있습니다 hello 클라이언트에서 hello 클라우드에 저장 된 데이터를 전송 되어야 합니다. Hello에 다시 전달를 사용자가 해당 데이터를 검색할 때 방향이 반대입니다. 데이터 hello를 통해 전송 되는 공용 인터넷 공격자의 목표가 인터 셉 션의 위험에 항상 됩니다. 개인 데이터의 중요 한 tooprotect hello 개인 정보 보호 위치 간에 이동 하는 것으로 전송 수준 암호화 toosecure를 사용 하 여

HTTPS 프로토콜 hello hello 인터넷을 통해 안전 하 고 암호화 된 통신 채널을 제공합니다. REST Api를 호출할 때 HTTPS 및 Azure 저장소의 사용된 tooaccess 개체 있어야 합니다. 사용 하는 경우 hello HTTPS 프로토콜의 사용 적용 [공유 액세스 서명](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate tooAzure 저장소 개체에 액세스 합니다. SAS에는 두 가지 유형, 즉 서비스 SAS와 계정 SAS가 있습니다.

#### <a name="how-do-i-construct-a-service-sas"></a>서비스 SAS를 구성하려면 어떻게 할까요?

서비스 SAS 대리자 액세스 tooa 리소스의 hello 저장소 서비스 (blob, 큐, 테이블 또는 파일 서비스) 중 하나입니다. 서비스 SAS tooconstruct 다음 hello지 않습니다.

1. Hello 서명 됨 버전 필드 지정

2. Hello 서명 됨 리소스 (Blob 및 파일 서비스에만 해당)를 지정 합니다.

3. 쿼리 매개 변수 tooOverride 응답 헤더 (Blob 서비스 및 파일 서비스에만 해당)를 지정 합니다.

4. Hello 테이블 이름 (테이블 서비스에만 해당)를 지정 합니다.

5. Hello 액세스 정책 지정

6. Hello 서명 유효성 간격 지정

8. 권한을 지정합니다.

9. IP 주소 또는 IP 범위를 지정합니다.

10. Hello HTTP 프로토콜을 지정 합니다.

11. 테이블 액세스 범위를 지정합니다.

12. Hello 서명 됨 식별자를 지정 합니다.

13. Hello 서명을 지정 합니다.

자세한 지침은 [서비스 SAS 구성](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN)을 참조하세요.

#### <a name="how-do-i-construct-an-account-sas"></a>계정 SAS를 구성하려면 어떻게 할까요?

계정 SAS 액세스 tooresources 하나 이상의 hello 저장소 서비스에 위임합니다. 또한 액세스 tooread, 쓰기 및 삭제 작업을 blob 컨테이너, 테이블, 큐 및 서비스 SAS와 함께 사용할 수 없는 파일 공유를 위임할 수 있습니다. 계정 SAS 생성할 때 서비스 sa 비슷한 toothat 않습니다. 자세한 지침은 [계정 SAS 구성](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)을 참조하세요.

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a>REST API를 호출할 때 HTTPS를 적용하려면 어떻게 할까요?

저장소 계정에서 REST Api tooaccess 개체를 호출할 때 HTTPS tooenforce hello 사용을 활성화할 수 있습니다 필요한 전송 보안 hello 저장소 계정에 대 한. 

1. Hello Azure 포털에서에서 선택 **저장소 계정 만들기**, 기존 저장소 계정을 선택 하거나 **설정** 차례로 **구성**합니다.

2. **보안 전송 필요** 아래에서 **사용**을 선택합니다.

![저장소 계정 만들기](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

자세한 내용은 포함 하 여 tooenable 필수 전송 보안 프로그래밍 방식으로 참조 하는 방법 [전송 보안을 설정 해야](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer)합니다.

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a>Azure File Storage에서 데이터를 암호화하려면 어떻게 할까요?

tooencrypt 데이터와 전송 중에 [Azure 파일 저장소](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), SMB를 사용할 수 있습니다 Windows 8, 8.1 및 10 및 Windows Server 2012 R2 및 Windows Server 2016 3.x 합니다. Hello Azure 파일 서비스를 사용 하는 암호화 되지 않은 모든 연결 실패 "보안 전송 필요"를 사용 하도록 설정 합니다. SMB 2.1, SMB 3.0 암호화 없이 및 일부 버전의 Linux SMB 클라이언트 hello 사용 하는 시나리오를 포함 합니다.

#### <a name="azure-client-side-encryption"></a>Azure 클라이언트 쪽 암호화

클라이언트 응용 프로그램과 Azure Storage 간에 전송되는 데이터를 보호하기 위한 또 다른 옵션은 [클라이언트 쪽 암호화](https://docs.microsoft.com/azure/storage/storage-client-side-encryption)입니다. Azure 저장소로 전송 하기 전에 hello 데이터는 암호화 및 hello 클라이언트 쪽에서 받은 후 hello 데이터를 암호 해독할 때 Azure 저장소에서 hello 데이터를 검색 합니다.

### <a name="azure-site-to-site-vpn"></a>Azure 사이트 간 VPN

회사 네트워크 또는 사용자와 hello Azure 가상 네트워크 간에 데이터가 전송는 효과적인 방법은 tooprotect 개인 데이터는 toouse는 [사이트 간](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) 또는 [지점 및 사이트](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) 가상 개인 네트워크 (VPN). VPN 연결 hello 인터넷 간에 암호화 된 보안 터널을 만듭니다.

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a>사이트 간 VPN 연결을 만들려면 어떻게 할까요?

사이트 간 VPN hello 회사 네트워크 tooAzure에서 여러 사용자를 연결합니다. hello Azure 포털에서에서 사이트 간 연결 toocreate 다음 hello지 않습니다.

1. 가상 네트워크를 만듭니다.

2. DNS 서버를 지정합니다.

3. Hello 게이트웨이 서브넷을 만듭니다.

4. Hello VPN 게이트웨이 만듭니다. 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. Hello 로컬 네트워크 게이트웨이 만듭니다.

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. VPN 장치를 구성합니다.

7. Hello VPN 연결을 만듭니다.

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. Hello VPN 연결을 확인 합니다.

자세한 지침은에 어떻게 toocreate는 사이트 및 사이트 간 연결에 hello Azure 포털에서 참조 [hello Azure 포털에서에서 사이트-사이트 만들기 연결 합니다.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a>지점 및 사이트 간 VPN 연결을 만들려면 어떻게 할까요?

지점-사이트 VPN 개별 클라이언트 컴퓨터 tooa 가상 네트워크에서 보안 연결을 만듭니다. 집 이나 호텔 또는 회의 센터에서와 같은 원격 위치에서 tooconnect tooAzure을 원하는 경우에 유용 합니다. toocreate hello Azure 포털에서에서 지점 및 사이트 연결

1. 가상 네트워크를 만듭니다.

2. 게이트웨이 서브넷을 추가합니다.

3. DNS 서버를 지정합니다. (선택 사항)

4. 가상 네트워크 게이트웨이를 만듭니다.

5. 인증서를 생성합니다.

6. Hello 클라이언트 주소 풀을 추가 합니다.

7. Hello 루트 인증서 공용 인증서 데이터를 업로드 합니다.

8. 생성 하 고 hello VPN 클라이언트 구성 패키지를 설치 합니다.

9. 내보낸 클라이언트 인증서를 설치합니다.

10. TooAzure를 연결 합니다.

11. 연결을 확인합니다.

자세한 내용은 참조 [지점 및 사이트 연결 tooa VNet 구성 인증서 인증을 사용 하 여: Azure 포털입니다.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)

### <a name="ssltls"></a>SSL/TLS

다른 위치에서 SSL/TLS 프로토콜 tooexchange 데이터를 항상 사용 하는 것이 좋습니다. Toouse를 선택 하는 조직은 [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove 큰 데이터 집합 전용된 고속 WAN 링크를 통해 hello 데이터 hello 보호 하기 위해 다른 프로토콜 또는 SSL/TLS를 사용 하 여 응용 프로그램 수준에서 암호화할 수도 있습니다.

### <a name="encryption-by-default"></a>기본적으로 암호화

Microsoft Azure 클라우드 서비스의 고객 간에 전송 중에 암호화 tooprotect 데이터를 사용합니다. Hello Azure 포털을 통해 Azure 저장소와 상호 작용 하는, 하는 경우 HTTPS를 통해 모든 트랜잭션이 발생 합니다.

[전송 계층 보안](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS)는 hello 프로토콜 Microsoft 데이터 센터 toonegotiate tooMicrosoft 클라우드 서비스를 연결 하는 클라이언트 시스템을 시도 합니다. TLS는 강력한 인증, 메시지 개인 정보 보호 및 무결성(메시지 변조, 가로채기 및 위조에 대한 검색 가능), 상호 운용성, 알고리즘 유연성, 배포 및 사용 편의성을 제공합니다.

또한 고객의 클라이언트 시스템과 Microsoft의 클라우드 서비스 간의 각 연결에서 고유한 키를 사용하도록 [PFS(Perfect Forward Secrecy)](https://en.wikipedia.org/wiki/Forward_secrecy)도 채택되었습니다. 연결 tooMicrosoft 클라우드 서비스 활용 기반으로 하는 RSA 2048 비트 암호화 키 길이입니다. TLS, RSA 2048 비트 키 길이 조합의 hello 및 PFS 훨씬 더 어려워집니다 다른 사용자에 대 한 Microsoft 클라우드 서비스와 고객 간에 전송 되는 데이터에 액세스 하 toointercept 합니다.

전송 중인 데이터는 항상 [Data Lake Store](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview)에서 암호화됩니다. 또한 tooencrypting 데이터 사전 toostoring toopersistent 미디어 hello 데이터는 항상 전송에 보호 HTTPS를 사용 하 여 합니다. HTTPS는 hello hello 데이터 레이크 저장소 REST 인터페이스에 지원 되는 유일한 프로토콜입니다.

## <a name="summary"></a>요약

hello 회사 HTTPS 연결 tooAzure 저장소를 적용, 공유 액세스 서명을 사용 하 여 및 hello 저장소 계정에 필요한 전송 보안을 사용 하 여 이러한 데이터의 개인 데이터 및 hello의 개인 정보 보호 목표를 수행할 수 있습니다. 또한 SMB 3.0 연결을 사용하고 클라이언트 쪽 암호화를 구현하여 개인 데이터를 보호할 수도 있습니다. 사이트 간 VPN 연결에는 Azure 가상 네트워크의 회사 네트워크 toohello hello 및 개별 사용자의 지점-사이트 VPN 연결 있는 개인 데이터 안전 하 게 통과할 수 안전한 터널을 만듭니다. Microsoft의 기본 암호화 사례 개인 데이터의 hello 개인 정보를 추가로 보호 합니다.

## <a name="next-steps"></a>다음 단계

- [Azure 데이터 보안 및 암호화 모범 사례](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [VPN Gateway 계획 및 설계](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [VPN 게이트웨이 FAQ](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [Azure App Service에 대한 SSL 인증서 구입 및 구성](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)

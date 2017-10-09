---
title: "aaaSQL VM 연결 tooAzure 검색 | Microsoft Docs"
description: "암호화 된 연결을 사용 하도록 설정 하 고 Azure 검색에서 인덱서에서 Azure 가상 컴퓨터 (VM)에서 hello 방화벽 tooallow 연결 tooSQL 서버를 구성 합니다."
services: search
documentationcenter: 
author: HeidiSteen
manager: pablocas
editor: 
ms.assetid: 46e42e0e-c8de-4fec-b11a-ed132db7e7bc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: heidist
ms.openlocfilehash: 1f0db8a2812b0a7d012e58bb873c4b2b29fa1338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-connection-from-an-azure-search-indexer-toosql-server-on-an-azure-vm"></a>Azure VM에서 Azure 검색 인덱서 tooSQL 서버에서에서 연결을 구성 합니다.
설명한 것 처럼 [인덱서를 사용 하 여 Azure SQL 데이터베이스 연결 tooAzure 검색](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md#faq)를 만들기에 대 한 인덱서 **Azure Vm에서 SQL Server** (또는 **SQL Azure Vm** 줄여서)은 Azure 검색에서 지 원하는 지만 몇 가지 보안 관련 필수 구성 요소 tootake 첫 번째 care of 있습니다. 

**작업 기간:** 약 30 분 이미 가정 하 고 hello VM에 인증서를 설치 합니다.

## <a name="enable-encrypted-connections"></a>암호화 연결 사용
Azure Search에는 공용 인터넷 연결을 통한 모든 인덱서 요청에 대한 암호화된 채널이 필요합니다. 이 섹션에서는 hello 단계 toomake이이 작업을 나열 합니다.

1. Hello 인증서 tooverify hello 주체 이름이의 hello 속성 hello hello Azure VM의 정규화 된 도메인 이름 (FQDN) 확인 하십시오. CertUtils 같은 도구를 사용 하거나 인증서 스냅인 tooview hello 속성 hello 수 있습니다. Hello에 hello VM 서비스 블레이드 Essentials 섹션에서 FQDN hello를 얻을 수 있습니다 **공용 IP 주소/d n S 이름 레이블** 필드 hello에 [Azure 포털](https://portal.azure.com/)합니다.
   
   * 최신 hello를 사용 하 여 만든 Vm에 대 한 **리소스 관리자** 템플릿을 hello FQDN 서식이 `<your-VM-name>.<region>.cloudapp.azure.com`합니다. 
   * 로 만들어진 오래 된 Vm에 대 한 한 **클래식** VM을 FQDN 서식이 hello `<your-cloud-service-name.cloudapp.net>`합니다. 
2. Hello 레지스트리 편집기 (regedit)를 사용 하 여 SQL Server toouse hello 인증서를 구성 합니다. 
   
    이 작업에는 보통 SQL Server 구성 관리자가 사용되지만 이 시나리오에 대해서는 사용할 수 없습니다. 것 hello hello hello Azure에서 VM의 FQDN hello FQDN hello (식별 hello 도메인 hello 로컬 컴퓨터 또는 hello 네트워크 도메인 toowhich 가입 된) VM 기준으로 일치 하지 않으므로 인증서를 가져온 찾을 수 없습니다. 이름이 일치 하지 않을 경우 regedit toospecify hello 인증서를 사용 합니다.
   
   * Regedit에서 toothis 레지스트리 키를 찾아: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\[MSSQL13.MSSQLSERVER]\MSSQLServer\SuperSocketNetLib\Certificate`합니다.
     
     hello `[MSSQL13.MSSQLSERVER]` 파트는 버전 및 인스턴스 이름에 따라 달라 집니다. 
   * Hello의 hello 값 설정 **인증서** 키 toohello **지문** toohello VM 가져온 hello SSL 인증서의 합니다.
     
     여러 가지 방법으로 tooget hello 지문은 일부 다른 항목 보다 더 합니다. Hello에서 복사 하는 경우 **인증서** 스냅인 MMC에서 있습니다 수 선택 됩니다는 보이지 않는 선행 문자 [이 지원 문서에 설명 된 대로](https://support.microsoft.com/kb/2023869/)를 시도할 때 오류가 발생 하는 연결입니다. 이 문제를 해결하기 위한 여러 가지 해결 방법이 존재합니다. 가장 쉬운 hello toobackspace 스타일러스가 하 고 다시 hello hello 지문 tooremove hello 선행 문자 regedit에서 hello 키 값 필드에서의 첫 번째 문자를 입력 합니다. 또는 다른 도구 toocopy hello 지문을 사용할 수 있습니다.
3. Toohello 서비스 계정 권한을 부여 합니다. 
   
    SQL Server 서비스 계정 hello hello SSL 인증서의 개인 키 hello에 대 한 적절 한 권한이 부여 되 고 있는지 확인 합니다. 이 단계를 무시하면 SQL Server가 시작되지 않습니다. Hello를 사용할 수 있습니다 **인증서** 스냅인 또는 **CertUtils** 이 작업에 대 한 합니다.
4. Hello SQL Server 서비스를 다시 시작 합니다.

## <a name="configure-sql-server-connectivity-in-hello-vm"></a>Hello VM에서에서 SQL Server 연결을 구성 합니다.
Azure 검색에 필요한 hello 암호화 된 연결을 설정한 후에 다음과 같은 추가 구성 단계 내장 tooSQL Azure Vm에는 서버. 아직 수행 하지 않은 경우 hello 다음 단계는 다음이 문서 중 하나를 사용 하 여 toofinish 구성입니다.

* 에 대 한는 **리소스 관리자** VM 참조 [tooa 리소스 관리자를 사용 하 여 Azure에서 SQL Server 가상 컴퓨터를 연결](../virtual-machines/windows/sql/virtual-machines-windows-sql-connect.md)합니다. 
* 에 대 한는 **클래식** VM 참조 [tooa Azure 클래식에서 SQL Server 가상 컴퓨터를 연결](../virtual-machines/windows/classic/sql-connect.md)합니다.

특히, 각 문서에 대 한 hello 섹션을 검토 "hello 인터넷에 연결" 됩니다.

## <a name="configure-hello-network-security-group-nsg"></a>Hello 보안 그룹 NSG (네트워크) 구성
것이 tooconfigure hello NSG 및 해당 하는 Azure 끝점 또는 액세스 제어 목록 (ACL) toomake Azure VM tooother 액세스할 수 있는 당사자입니다. 작업을 수행 하면이 tooallow 하기 전에 사용자 고유의 응용 프로그램 논리 tooconnect tooyour SQL Azure VM 될 확률이 합니다. Azure 검색 연결 tooyour SQL Azure VM에 대 한 더 차이가 있습니다. 

아래 hello 링크 NSG 구성 VM 배포에 대 한 지침을 제공 합니다. TooACL Azure 검색 끝점의 IP 주소에 따라 다음이 지침을 따르세요.

> [!NOTE]
> 배경 지식은 [네트워크 보안 그룹이란?](../virtual-network/virtual-networks-nsg.md)
> 
> 

* 에 대 한는 **리소스 관리자** VM 참조 [어떻게 ARM 배포용 toocreate Nsg](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)합니다. 
* 에 대 한는 **클래식** VM 참조 [어떻게 클래식 배포에 대 한 toocreate Nsg](../virtual-network/virtual-networks-create-nsg-classic-ps.md)합니다.

IP 주소 지정은 문제를 쉽게 해결할 경우 hello 문제 및 가능한 해결 방법에 대해 알고 있는 몇 가지 과제 내포할 수 있습니다. 나머지 단원 들을 hello hello ACL에서에서 관련된 tooIP 주소 문제를 처리 하기 위한 권장 사항을 제공 합니다.

#### <a name="restrict-access-toohello-search-service-ip-address"></a>액세스 toohello 검색 서비스 IP 주소를 제한 합니다.
넓은 tooany 연결 요청을 열고 하 여 SQL Azure Vm을 만드는 대신 hello ACL에서에서 검색 서비스의 hello 액세스 toohello IP 주소를 제한 하는 것이 좋습니다. Hello IP를 쉽게 알아볼 수 ping을 실행 하는 주소 hello FQDN (예를 들어 `<your-search-service-name>.search.windows.net`) 검색 서비스의 합니다.

#### <a name="managing-ip-address-fluctuations"></a>IP 주소 변동 관리
검색 서비스에 하나의 검색 단위만 (즉, 하나의 복제본과 하나의 파티션), 라우팅 서비스를 시작 하면 검색 서비스의 IP 주소를 가진 기존 ACL을 무효화 하는 동안 hello IP 주소가 변경 됩니다.

한 가지 방법은 tooavoid hello 후속 연결 오류 toouse 두 개 이상의 하나의 복제본과 Azure 검색의 한 파티션만 합니다. 이렇게 하면 hello 비용 커지지만 hello IP 주소 문제가 해결 되 합니다. Azure Search에서는 검색 단위가 둘 이상인 경우 IP 주소가 변경되지 않습니다.

두 번째 방식은 tooallow hello 연결 toofail을 다음 hello NSG에에서 Acl hello를 다시 구성 합니다. 평균적으로 IP 주소 toochange 몇 주 간격 기대할 수 있습니다. 드물게 제어 인덱싱을 수행하는 고객의 경우 이 방법을 실행할 수 있습니다.

세 번째 실행 가능한 (하지만 특히 안전 하지 않은) 방법을 검색 서비스 프로 비전 된 Azure 지역 hello toospecify hello IP 주소 범위입니다. 에 있는 공용 IP 주소 리소스가 할당 됩니다. tooAzure IP 범위 목록이 hello를 게시 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)합니다. 

#### <a name="include-hello-azure-search-portal-ip-addresses"></a>Hello Azure 검색 포털 IP 주소를 포함 합니다.
Azure 포털 toocreate 인덱서 hello를 사용 하는 Azure 검색 포털 논리 만든 시간 동안 액세스 tooyour SQL Azure VM도 필요 합니다. `stamp2.search.ext.azure.com`을 ping하여 Azure Search 포털 IP 주소를 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계
Hello 방식을 구성에서는 Azure 검색 인덱서 hello 데이터 원본으로 Azure VM에서 SQL Server을 이제 지정할 수 있습니다. 참조 [인덱서를 사용 하 여 Azure SQL 데이터베이스 연결 tooAzure 검색](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md) 자세한 정보에 대 한 합니다.


---
title: "aaaGeneric LDAP 커넥터 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooconfigure Microsoft 일반 LDAP 커넥터입니다."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 984beeb0-4d91-4908-ad81-c19797c4891b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 25031b4da196bd073902b04b0705762bfa0118b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="generic-ldap-connector-technical-reference"></a>일반 LDAP 커넥터 기술 참조
이 문서에서는 hello 일반 LDAP 커넥터를 설명 합니다. hello 문서 toohello 제품 다음이 적용 됩니다.

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * 핫픽스 4.1.3671.0 이상 [KB3092178](https://support.microsoft.com/kb/3092178)을 사용해야 합니다.

Hello 커넥터 MIM2016 및 FIM2010R2 hello에서 다운로드할 수는 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=717495)합니다.

이 문서는 hello 형식을 사용 하 여 tooIETF Rfc를 참조할 때 (RFC [RFC number] / [RFC 문서의 섹션]), 예를 들어 (RFC 4512/4.3).
자세한 내용은 http://tools.ietf.org/html/rfc4500 (필요 tooreplace 4500 hello 올바른 RFC 번호로)에서 찾을 수 있습니다.

## <a name="overview-of-hello-generic-ldap-connector"></a>Hello 일반 LDAP 커넥터 개요
일반 LDAP 커넥터 hello toointegrate hello 동기화 서비스를 LDAP v3 서버와 수 있습니다.

특정 작업 및 스키마 요소, tooperform 델타 가져오기 필요한 것 같은에 지정 되지 않은 hello IETF rfc를 대체 합니다. 이러한 작업의 경우 명시적으로 지정된 LDAP 디렉터리만 지원됩니다.

상위 수준 측면에서 같은 기능 hello hello hello 커넥터의 현재 버전에서 지원 됩니다.

| 기능 | 지원 |
| --- | --- |
| 연결된 데이터 원본 |hello 커넥터 모든 LDAP v3 서버 (RFC 4510 호환)를 사용할 수 있습니다. Hello 다음으로 테스트 되었습니다. <li>Microsoft Active Directory Lightweight Directory Services(AD LDS)</li><li>Microsoft Active Directory 글로벌 카탈로그(AD GC)</li><li>389 디렉터리 서버</li><li>Apache 디렉터리 서버</li><li>IBM Tivoli DS</li><li>Isode 디렉터리</li><li>NetIQ eDirectory</li><li>Novell eDirectory</li><li>DJ 열기</li><li>DS 열기</li><li>LDAP 열기(openldap.org)</li><li>Oracle(이전에 Sun) 디렉터리 서버 Enterprise Edition</li><li>RadiantOne 가상 디렉터리 서버(VDS)</li><li>Sun One 디렉터리 서버</li>**다음과 같이 주목할 만한 디렉터리는 지원되지 않습니다.** <li>Microsoft Active Directory 도메인 서비스 (AD DS) [사용 하 여 기본 제공 Active Directory Connector을 대신 hello 데 사용]</li><li>Oracle Internet Directory(OID)</li> |
| 시나리오 |<li>개체 수명 주기 관리</li><li>그룹 관리</li><li>암호 관리</li> |
| 작업 |작업을 수행 하는 hello 모든 LDAP 디렉터리에 지원 됩니다. <li>전체 가져오기</li><li>내보내기</li>작업을 수행 하는 hello 지정 된 디렉터리 에서만 지원 됩니다.<li>델타 가져오기</li><li>암호 설정, 암호 변경</li> |
| 스키마 |<li>Hello LDAP 스키마 (RFC3673 및 RFC4512/4.2)에서 스키마 검색</li><li>구조 클래스, 보조 클래스 및 extensibleObject 개체 클래스(RFC4512/4.3)를 지원합니다.</li> |

### <a name="delta-import-and-password-management-support"></a>델타 가져오기 및 암호 관리 지원
델타 가져오기 및 암호 관리에 지원되는 디렉터리:

* Microsoft Active Directory Lightweight Directory Services(AD LDS)
  * 델타 가져오기에 모든 작업을 지원합니다.
  * 암호 설정 지원
* Microsoft Active Directory 글로벌 카탈로그(AD GC)
  * 델타 가져오기에 모든 작업을 지원합니다.
  * 암호 설정 지원
* 389 디렉터리 서버
  * 델타 가져오기에 모든 작업을 지원합니다.
  * 암호 설정 및 암호 변경 지원
* Apache 디렉터리 서버
  * 이 디렉터리에 영구 변경 로그가 없으므로 델타 가져오기를 지원하지 않습니다.
  * 암호 설정 지원
* IBM Tivoli DS
  * 델타 가져오기에 모든 작업을 지원합니다.
  * 암호 설정 및 암호 변경 지원
* Isode 디렉터리
  * 델타 가져오기에 모든 작업을 지원합니다.
  * 암호 설정 및 암호 변경 지원
* Novell eDirectory 및 NetIQ eDirectory
  * 델타 가져오기에 대한 추가, 업데이트 및 이름 바꾸기 작업을 지원합니다.
  * 델타 가져오기에 대한 삭제 작업을 지원하지 않습니다.
  * 암호 설정 및 암호 변경 지원
* DJ 열기
  * 델타 가져오기에 모든 작업을 지원합니다.
  * 암호 설정 및 암호 변경 지원
* DS 열기
  * 델타 가져오기에 모든 작업을 지원합니다.
  * 암호 설정 및 암호 변경 지원
* LDAP 열기(openldap.org)
  * 델타 가져오기에 모든 작업을 지원합니다.
  * 암호 설정 지원
  * 암호 변경을 지원하지 않습니다.
* Oracle(이전에 Sun) 디렉터리 서버 Enterprise Edition
  * 델타 가져오기에 모든 작업을 지원합니다.
  * 암호 설정 및 암호 변경 지원
* RadiantOne 가상 디렉터리 서버(VDS)
  * 버전 7.1.1 이상을 사용해야 합니다.
  * 델타 가져오기에 모든 작업을 지원합니다.
  * 암호 설정 및 암호 변경 지원
* Sun One 디렉터리 서버
  * 델타 가져오기에 모든 작업을 지원합니다.
  * 암호 설정 및 암호 변경 지원

### <a name="prerequisites"></a>필수 조건
Hello 커넥터를 사용 하기 전에 hello 동기화 서버에 hello 다음 있는지 확인 합니다.

* Microsoft.NET 4.5.2 Framework 이상

### <a name="detecting-hello-ldap-server"></a>Hello LDAP 서버를 검색합니다.
hello 커넥터는 다양 한 기술 toodetect에 의존 하 고 hello LDAP 서버를 식별 합니다. hello 커넥터 사용 하 여 hello 루트 DSE, 공급 업체 이름/버전 및 hello 스키마 toofind 고유 개체 및 tooexist 특정 LDAP 서버에 알려진 특성을 검사 합니다. 이 데이터를 하는 경우 발견, 사용 되는 toopre는-hello 커넥터에서에서 hello 구성 옵션을 채웁니다.

### <a name="connected-data-source-permissions"></a>연결된 데이터 원본 사용 권한
tooperform 가져오기 및 내보내기 hello 연결 된 디렉터리의 hello 개체에는 작업, hello 커넥터 계정에 충분 한 권한이 있어야 합니다. hello 커넥터 권한을 toobe 수 tooexport 쓰기 및 읽기 권한 toobe 수 tooimport 필요 합니다. 사용 권한 구성이 자체 hello 대상 디렉터리의 hello 관리 경험 내에서 수행 됩니다.

### <a name="ports-and-protocols"></a>포트 및 프로토콜
hello 커넥터는 기본적으로이 LDAP에 대 한 389 및 636 LDAPS에 대 한 hello 구성에 지정 된 hello 포트 번호를 사용 합니다.

LDAPS의 경우 SSL 3.0 또는 TLS를 사용해야 합니다. SSL 2.0은 지원되지 않으며 활성화될 수 없습니다.

### <a name="required-controls-and-features"></a>필수 제어 및 기능
hello 다음과 같은 LDAP 컨트롤/기능에서 사용할 수 있어야 커넥터 toowork hello에 대 한 LDAP 서버 hello 제대로:  
`1.3.6.1.4.1.4203.1.5.3` True/False 필터

hello True/False 필터 자주 보고 되지 않는다 LDAP 디렉터리에서 지 원하는 대로 및 hello에 표시할 수 있습니다 **글로벌 페이지** 아래 **필수 기능 찾지**합니다. 사용 되는 toocreate는 **또는** 예를 들어 여러 개체 유형을 가져올 때 LDAP 쿼리에 필터입니다. 하나 이상의 개체 형식을 가져올 수 있으면 LDAP 서버가 이 기능을 지원합니다.

Hello 앵커 hello 다음 에서도 사용할 수 있어야 고유 식별자가 있는 디렉터리를 사용 하는 경우 (자세한 내용은 참조 hello [앵커 구성](#configure-anchors) 섹션):  
`1.3.6.1.4.1.4203.1.5.1` 모든 작업 특성

Hello 디렉터리 하나 호출 toohello 디렉터리에 표시할 수 있는 것 보다 더 많은 개체 경우 것이 좋습니다 toouse 페이징 합니다. 페이징 toowork hello 다음 옵션 중 하나가 필요 합니다.

**옵션 1:**  
`1.2.840.113556.1.4.319` pagedResultsControl

**옵션 2:**  
`2.16.840.1.113730.3.4.9` VLVControl  
`1.2.840.113556.1.4.473` SortControl

두 옵션 모두 hello 커넥터 구성에서 사용 되는 경우 pagedResultsControl 사용 됩니다.

`1.2.840.113556.1.4.417` ShowDeletedControl

ShowDeletedControl은 hello USNChanged 델타 가져오기 메서드 toobe 삭제 수 toosee 개체와만 사용 됩니다.

hello 커넥터 toodetect hello 있는 hello 서버 옵션을 시도합니다. Hello 옵션을 검색할 수 없는 경우 경고가 hello 커넥터 속성에서 hello 글로벌 페이지에 없는 것입니다. 모든 LDAP 서버 모든 컨트롤/기능을 지원 하며이 경고는 존재 하는 경우에 hello 커넥터 문제 없이 작동 될 수 있습니다.

### <a name="delta-import"></a>델타 가져오기
델타 가져오기는 지원 디렉터리를 감지한 때 사용할 수 있습니다. 현재 메서드를 다음 hello 사용:

* LDAP Accesslog. [http://www.openldap.org/doc/admin24/overlays.html#Access Logging](http://www.openldap.org/doc/admin24/overlays.html#Access Logging)을 참조하세요.
* LDAP Changelog. [http://tools.ietf.org/html/draft-good-ldap-changelog-04](http://tools.ietf.org/html/draft-good-ldap-changelog-04)
* TimeStamp. Novell/NetIQ eDirectory hello 커넥터 사용 하 여 마지막 날짜/시간 tooget 만들고 개체를 업데이트 합니다. Novell/NetIQ eDirectory 해당 의미 tooretrieve 삭제 된 개체를 제공 하지 않습니다. 다른 델타 가져오기 메서드 hello LDAP 서버에서 실행 중인 경우이 옵션을 사용할 수도 있습니다. 이 옵션은 삭제 수 tooimport 개체가 없습니다.
* USNChanged. [https://msdn.microsoft.com/library/ms677627.aspx](https://msdn.microsoft.com/library/ms677627.aspx)

### <a name="not-supported"></a>지원되지 않음
hello 같은 LDAP 기능 지원 되지 않습니다.

* 서버 간 LDAP 조회(RFC 4511/4.1.10)

## <a name="create-a-new-connector"></a>새 커넥터 만들기
tooCreate 일반 LDAP 커넥터의 **동기화 서비스** 선택 **관리 에이전트** 및 **만들기**합니다. 선택 hello **일반 LDAP (Microsoft)** 커넥터입니다.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericldap/createconnector.png)

### <a name="connectivity"></a>연결
Hello 연결 페이지 hello 호스트, 포트 및 바인딩 정보를 지정 해야 합니다. 바인딩에 추가 옵션을 선택에 따라 정보 hello 다음 섹션에에서 제공 될 수도 있습니다.

![연결](./media/active-directory-aadconnectsync-connector-genericldap/connectivity.png)

* hello 연결 시간 제한 설정은 hello 스키마를 검색 하는 경우에 첫 번째 연결 toohello 서버 hello에 대 한 사용 됩니다.
* 바인딩이 익명인 경우 사용자 이름/암호 또는 인증서 어느 것도 사용할 수 없습니다.
* 다른 바인딩의 경우 사용자 이름/암호 중 하나에 정보를 입력하거나 인증서를 선택합니다.
* Kerberos tooauthenticate를 사용 하는 경우 다음 제공 hello 영역/hello 사용자의 도메인입니다.

hello **별칭 특성** RFC4522 구문 사용 하 여 hello 스키마에 정의 된 특성에 대 한 텍스트 상자를 사용 합니다. 스키마 검색 하는 동안 이러한 특성을 검색할 수 없습니다 및 hello 커넥터 tooidentify 특성 도움이 필요 합니다. 예를 들어 hello 특성 별칭 상자 toocorrectly에 다음을 입력 해야 하는 hello 이진 특성으로 hello userCertificate 특성을 식별 합니다.

`userCertificate;binary`

hello 다음은이 구성은 같을 수 있습니다에 대 한 예제입니다.

![연결](./media/active-directory-aadconnectsync-connector-genericldap/connectivityattributes.png)

선택 hello **operational 특성 스키마에 포함할** 확인란 tooalso hello 서버에서 만들어진 특성을 포함 합니다. 여기에 hello 개체를 만든 시점과 마지막 업데이트 시간 같은 특성이 포함 됩니다.

선택 **스키마에 확장 가능한 특성을 포함** 경우 확장 가능한 개체 (RFC4512/4.3)를 사용 하 고이 옵션을 사용 하면 모든 개체에 사용 되는 모든 특성 toobe 합니다. 이 옵션을 선택 하면에서는 hello 스키마 매우 큰 있도록 hello 연결 된 디렉터리를 사용 하지 않는 한이 기능 hello 좋습니다 tookeep hello 옵션을 선택 해제 합니다.

### <a name="global-parameters"></a>글로벌 매개 변수
Hello 글로벌 매개 변수 페이지에서 hello DN toohello 델타 변경 로그 및 추가 LDAP 기능을 구성 합니다. hello 페이지는 hello LDAP 서버에서 제공 하는 hello 정보로 채워져서입니다.

![연결](./media/active-directory-aadconnectsync-connector-genericldap/globalparameters.png)

hello 맨 위 섹션에는 hello 서버 자체를 hello 서버 hello 이름 등에서 제공 하는 정보가 표시 됩니다. hello 커넥터 hello 필수 컨트롤이 루트 DSE hello에 존재 하는지 확인 합니다. 이러한 제어가 나열되지 않으면 경고가 표시됩니다. 일부 LDAP 디렉터리의 루트 DSE hello에서 모든 기능을 나열 하지 않는 한 경고가 있는 경우에 문제 없이 커넥터가 작동 hello 가능한입니다.

hello **컨트롤 지원** 특정 작업에 대 한 hello 동작을 제어 하는 확인란을 선택 합니다.

* 트리 삭제를 선택한 경우 계층은 LDAP 호출을 사용하여 삭제됩니다. 선택 하지 않은 트리 delete와 hello 커넥터 필요한 경우 재귀 삭제를 수행 하지 않습니다.
* 선택한 페이지 된 결과 함께 hello 커넥터 hello 크기가 hello 실행 단계에 지정 된 페이징된 가져오기를 수행 합니다.
* VLVControl hello 및 SortControl는는 대체 toohello pagedResultsControl tooread 데이터 hello LDAP 디렉터리입니다.
* 3 가지 옵션 모두 (pagedResultsControl, VLVControl, 및 SortControl)는 선택 되어 있으면 다음 hello 커넥터가 가져옵니다 큰 디렉터리 경우 실패할 수 있는 한 번에 모든 개체를.
* ShowDeletedControl은 hello 델타 가져오기 방법 USNChanged 경우에 사용 됩니다.

hello 변경 로그 DN는 예를 들어 hello 델타 변경 로그에서 사용 하는 hello 명명 컨텍스트 **cn = changelog**합니다. 이 값 이어야 합니다 toobe 수 toodo 델타 가져오기 지정 합니다.

hello 다음은 기본 변경 로그 DNs의 목록입니다.

| 디렉터리 | 델타 변경 로그 |
| --- | --- |
| Microsoft AD LDS 및 AD GC |자동으로 검색됨. USNChanged. |
| Apache 디렉터리 서버 |사용할 수 없음. |
| 디렉터리 389 |변경 로그. 기본 값 toouse: **cn = changelog** |
| IBM Tivoli DS |변경 로그. 기본 값 toouse: **cn = changelog** |
| Isode 디렉터리 |변경 로그. 기본 값 toouse: **cn = changelog** |
| Novell/NetIQ eDirectory |사용할 수 없음. TimeStamp. hello 커넥터 사용 하 여 마지막 업데이트 날짜/시간 tooget 추가 되 고 레코드를 업데이트 합니다. |
| DJ/DS 열기 |변경 로그.  기본 값 toouse: **cn = changelog** |
| LDAP 열기 |액세스 로그. 기본 값 toouse: **cn = accesslog** |
| Oracle DSEE |변경 로그. 기본 값 toouse: **cn = changelog** |
| RadiantOne VDS |가상 디렉터리. 연결 된 디렉터리 tooVDS hello에 따라 다릅니다. |
| Sun One 디렉터리 서버 |변경 로그. 기본 값 toouse: **cn = changelog** |

hello 암호 특성은 hello 특성 hello 커넥터의 hello 이름 암호 변경 및 암호 설정 작업에서 tooset hello 암호를 사용 해야 합니다.
이 값은 기본적으로 너무 설정**userPassword** 되지만 특정 LDAP 시스템에 필요할 때 변경할 수 있습니다.

Hello 추가 파티션 목록에서 자동으로 검색 가능한 tooadd 추가 네임 스페이스입니다. 여러 서버 모두 가져와야 hello 논리적 클러스터를 구성 하는 경우이 설정을 사용할 수 있습니다 예를 들어 동시 합니다. 한 포리스트의 여러 도메인을 가질 수을 Active Directory와 마찬가지로 있지만 하나의 스키마를이 상자에 hello 추가 네임 스페이스를 입력 하 여 시뮬레이션할 수 있지만 동일한 hello를 공유 하는 모든 도메인. 각 네임 스페이스 서로 다른 서버에서 가져올 수 있으며 추가로 hello 파티션 구성 및 계층 페이지에 구성 됩니다. Ctrl + Enter tooget 새 줄을 사용 합니다.

### <a name="configure-provisioning-hierarchy"></a>프로비전 계층 구성
이 페이지는 사용 되는 toomap hello DN 구성 요소, 예를 들어 OU toohello 개체 형식을 프로비저닝해야 예를 들어 조직 구성 단위입니다.

![프로비전 계층 구조](./media/active-directory-aadconnectsync-connector-genericldap/provisioninghierarchy.png)

프로 비전 계층을 구성 하 여 구성할 수 있습니다 hello 커넥터 tooautomatically 필요할 때 구조를 만듭니다. 예를 들어 경우 네임 스페이스 dc = contoso, dc = com 및 새 개체 cn = Joe, ou, 시애틀 = c = US, dc = contoso, dc = com 프로 비전 되 면 다음 하는 것이 아직 hello 커넥터 미국 형식 국가 및 Seattle에 대해 organizationalUnit 개체를 만들 수 hello 디렉터리에 있습니다.

### <a name="configure-partitions-and-hierarchies"></a>파티션 및 계층 구조 구성
Hello 파티션 및 계층 구조 페이지에서 모든 네임 스페이스를 선택 tooimport 및 내보내기 계획 개체와 사용 합니다.

![파티션](./media/active-directory-aadconnectsync-connector-genericldap/partitions.png)

각 네임 스페이스에 대 한 것도 hello 연결 화면에 지정 된 hello 값을 재정의 가능한 tooconfigure 연결 설정 합니다. 이러한 값은 tootheir 빈 기본값을 두면 hello 정보 hello 연결 화면에서 사용 됩니다.

커넥터에서 가져오기 및 내보내기는 컨테이너 및 Ou hello 가능한 tooselect 이기도 합니다.

검색을 수행할 때이 hello 파티션에 모든 컨테이너에서 수행 됩니다. 경우에이 동작은 tooperformance 저하 잠재 고객 있는 많은 수의 컨테이너입니다.

>[!NOTE]
부터 hello 2017 년 3 월 업데이트 toohello 일반 LDAP 커넥터 검색 범위 tooonly hello 선택 컨테이너에 제한 될 수 있습니다. Hello 이미지 아래에 나와 있는 것 처럼 선택한 컨테이너에만 검색' hello 확인란을 선택 하 여이 작업을 수행할 수 있습니다.

![선택한 컨테이너에서만 검색](./media/active-directory-aadconnectsync-connector-genericldap/partitions-only-selected-containers.png)

### <a name="configure-anchors"></a>앵커 구성
이 페이지는 미리 구성된 값이 있으며 변경될 수 없습니다. Hello 서버 공급 업체를 식별 하는 경우 개체에 대 한 예제 hello GUID에 대 한 변경할 수 없는 특성으로 hello 앵커를 채워질 수 있습니다. 검색 되지 않았습니다 하거나 toonot 알려져 있는 경우 변경할 수 없는 특성이 다음 hello 커넥터 dn (고유 이름)를 사용 하 여 hello 앵커로 합니다.

![anchors](./media/active-directory-aadconnectsync-connector-genericldap/anchors.png)


hello 다음은 LDAP 서버 및 사용 하 고 hello 앵커의 목록입니다.

| 디렉터리 | 앵커 특성 |
| --- | --- |
| Microsoft AD LDS 및 AD GC |objectGUID |
| 389 디렉터리 서버 |dn |
| Apache 디렉터리 |dn |
| IBM Tivoli DS |dn |
| Isode 디렉터리 |dn |
| Novell/NetIQ eDirectory |GUID |
| DJ/DS 열기 |dn |
| LDAP 열기 |dn |
| Oracle ODSEE |dn |
| RadiantOne VDS |dn |
| Sun One 디렉터리 서버 |dn |

## <a name="other-notes"></a>기타 참고 사항
이 섹션에서는 특정 toothis 커넥터 파일이 나 다른 이유로 중요 한 tooknow 측면의 정보를 제공 합니다.

### <a name="delta-import"></a>델타 가져오기
Open ldap에서 hello 델타 워터 마크는 UTC 날짜/시간입니다. 이러한 이유로 FIM 동기화 서비스 사이의 hello Open LDAP hello 시계 동기화 되어야 합니다. 그렇지 않은 경우 hello 델타 변경 로그의 일부 항목을 생략 될 수 있습니다.

Novell eDirectory에 대 한 hello 델타 가져오기 모든 개체 삭제가 인식 하지 못합니다. 이러한 이유로 필요는 toorun 전체를 정기적으로 가져오는 toofind 모든 삭제 된 개체입니다.

항상이 델타를 사용 하 여 디렉터리 변경 날짜/시간을 기반으로 하는 로그를 정기적으로 시간에 전체 가져오기 toorun 권장 합니다. 이 프로세스는 hello 동기화 엔진 toofind 및 dissimilarities 사이의 hello LDAP 서버는 현재 hello 커넥터 공간을 허용 합니다.

## <a name="troubleshooting"></a>문제 해결
* 참조 hello tooenable 로깅 tootroubleshoot 커넥터 hello 하는 방법에 대 한 내용은 [어떻게 커넥터에 대 한 ETW 추적 tooEnable](http://go.microsoft.com/fwlink/?LinkId=335731)합니다.

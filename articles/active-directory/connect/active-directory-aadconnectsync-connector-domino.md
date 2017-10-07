---
title: "aaaLotus Domino 커넥터 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooconfigure Microsoft Lotus Domino 커넥터입니다."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: e07fd469-d862-470f-a3c6-3ed2a8d745bf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: affef1fec91eb39f7e91ec274fdd1b3a9c4a32fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="lotus-domino-connector-technical-reference"></a>Lotus Domino 커넥터 기술 참조
이 문서에서는 hello Lotus Domino 커넥터에 설명 합니다. hello 문서 toohello 제품 다음이 적용 됩니다.

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * 핫픽스 4.1.3671.0 이상 [KB3092178](https://support.microsoft.com/kb/3092178)을 사용해야 합니다.

Hello 커넥터 MIM2016 및 FIM2010R2 hello에서 다운로드할 수는 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=717495)합니다.

## <a name="overview-of-hello-lotus-domino-connector"></a>Lotus Domino 커넥터 hello 개요
Lotus Domino 커넥터 hello IBM의 Lotus Domino 서버와 toointegrate hello 동기화 서비스가 있습니다.

상위 수준 측면에서 같은 기능 hello hello hello 커넥터의 현재 버전에서 지원 됩니다.

| 기능 | 지원 |
| --- | --- |
| 연결된 데이터 원본 |서버:  <li>Lotus Domino 8.5.x</li><li>Lotus Domino 9.x</li>클라이언트:<li>Lotus Domino 8.5.x</li><li>Lotus Notes 9.x</li> |
| 시나리오 |<li>개체 수명 주기 관리</li><li>그룹 관리</li><li>암호 관리</li> |
| 작업 |<li>전체 및 델타 가져오기</li><li>내보내기</li><li>HTTP 암호에 대한 암호 설정 및 변경</li> |
| 스키마 |<li>사람(로밍 사용자, 연락처(인증서가 없는 사람))</li><li>그룹</li><li>리소스(리소스, 회의실, 온라인 모임)</li><li>메일 내 데이터베이스</li><li>지원되는 개체에 대한 특성의 동적 검색</li> |

hello Lotus Domino 커넥터 Lotus Domino 서버와 Lotus Notes 클라이언트 toocommunicate hello를 사용합니다. 이 종속성의 결과로 지원된 Lotus Notes 클라이언트 hello 동기화 서버에 설치 되어야 합니다. hello 클라이언트와 서버 hello hello 통신 hello Lotus Notes.NET Interop (Interop.domino.dll) 인터페이스를 통해 구현 됩니다. 이 인터페이스는 hello Microsoft.NET 플랫폼 사이의 Lotus Notes 클라이언트 hello 통신을 용이 하 게 하 고 액세스 tooLotus Domino 문서 및 뷰를 지원 합니다. 델타 가져오기에 대 한 것도 가능 선택한 hello 델타 가져오기 방법) (따라 해당 hello c + + 네이티브 인터페이스를 사용 합니다.

### <a name="prerequisites"></a>필수 조건
Hello 커넥터를 사용 하기 전에 hello 동기화 서버의 필수 구성 요소를 다음 hello 있는지 확인 합니다.

* Microsoft.NET 4.5.2 Framework 이상
* 동기화 서버에 hello Lotus Notes 클라이언트를 설치 해야
* Lotus Domino 커넥터 hello hello 기본 Lotus Domino LDAP 스키마 데이터베이스 (schema.nsf) toobe hello Domino 디렉터리 서버에 필요합니다. 나타나지 않는 경우 실행 하거나 hello Domino 서버의 hello LDAP 서비스를 다시 시작 하 여 설치할 수 있습니다.

### <a name="connected-data-source-permissions"></a>연결된 데이터 원본 사용 권한
tooperform hello의 지원 되는 모든 작업 Lotus Domino 커넥터에서 다음 그룹의 구성원 이어야 합니다.

* 모든 권한 관리자
* 관리자
* 데이터베이스 관리자

hello 다음 표에 각 작업에 대해 필요한 hello 사용 권한이 있습니다.

| 작업 | 액세스 권한 |
| --- | --- |
| 가져오기 |<li>공용 문서 읽기</li><li> 전체 관리자 액세스 (때는 전체 액세스 관리자 그룹의 구성원 인 경우 자동으로 해야 hello 유효한 액세스 tooin ACL.)</li> |
| 암호 내보내기 및 설정 |유효한 액세스: <li>문서 만들기</li><li>문서 삭제</li><li>공용 문서 읽기</li><li>공용 문서 작성</li><li>문서 복제 또는 복사</li>내보내기 작업 역할을 수행 하는 hello도 필요 합니다. <li>CreateResource</li><li>GroupCreator</li><li>GroupModifier</li><li>UserCreator</li><li>UserModifier</li> |

### <a name="direct-operations-and-adminp"></a>직접 작업 및 AdminP
작업 직접 toohello Domino 디렉터리를 이동 또는 AdminP hello를 통해 처리 합니다. hello 다음 표에 나열 모든 지원 되는 개체, 작업 및 hello 관련 구현 메서드가 해당 하는 경우:

**기본 주소록**

| Object | 생성 | 업데이트 | 삭제 |
| --- | --- | --- | --- |
| 사람 |AdminP |직접 |AdminP |
| 그룹 |AdminP |직접 |AdminP |
| MailInDB |직접 |직접 |직접 |
| 리소스 |AdminP |직접 |AdminP |

**보조 주소록**

| Object | 생성 | 업데이트 | 삭제 |
| --- | --- | --- | --- |
| 사람 |해당 없음 |직접 |직접 |
| 그룹 |직접 |직접 |직접 |
| MailInDB |직접 |직접 |직접 |
| 리소스 |해당 없음 |해당 없음 |해당 없음 |

리소스를 만들 때 Notes 문서가 생성됩니다. 마찬가지로, 리소스가 삭제 되 면 hello 메모 문서가 삭제 됩니다.

### <a name="ports-and-protocols"></a>포트 및 프로토콜
IBM Lotus Notes 클라이언트 및 Domino 서버는 NRPC가 TCP/IP를 사용해야 하는 NRPC(Notes Remote Procedure Call)을 사용하여 통신합니다. hello 기본 포트 번호, 1352 이지만 hello Domino 관리자가 변경할 수 있습니다.

### <a name="not-supported"></a>지원되지 않음
작업을 수행 하는 hello hello hello Lotus Domino 커넥터의 현재 버전에서 지원 되지 않습니다.

* 서버 간에 사서함을 이동합니다.

## <a name="create-a-new-connector"></a>새 커넥터 만들기
### <a name="client-software-installation-and-configuration"></a>클라이언트 소프트웨어 설치 및 구성
Lotus Notes hello 서버에 설치 해야 **전에** hello 커넥터를 설치 합니다.

설치할 때 **단일 사용자 설치**를 수행하도록 합니다. 기본 hello **다중 사용자 설치** 작동 하지 않습니다.  
![Notes1](./media/active-directory-aadconnectsync-connector-domino/notes1.png)

Hello 기능 페이지 hello 필수 Lotus Notes 기능을 설치 하 고 **클라이언트 단일 로그온**합니다. 단일 로그온 hello 커넥터 toobe toohello Domino 서버의 수 toolog 필요 합니다.  
![Notes2](./media/active-directory-aadconnectsync-connector-domino/notes2.png)

**참고:** 시작 Lotus Notes hello에 있는 사용자와 동일한 서버 hello 계정이 면 hello 커넥터의 서비스 계정으로 사용 합니다. 또한 서버 hello에 tooclose hello Lotus Notes 클라이언트에 있는지 확인 합니다. 실행할 수 없으며 hello에서 동일한 시간 hello 커넥터 tooconnect toohello Domino 서버를 시도 합니다.

### <a name="create-connector"></a>커넥터 만들기
Lotus Domino 커넥터 tooCreate에 **동기화 서비스** 선택 **관리 에이전트** 및 **만들기**합니다. 선택 hello **Lotus Domino (Microsoft)** 커넥터입니다.  
![CreateConnector](./media/active-directory-aadconnectsync-connector-domino/createconnector.png)

동기화 서비스의 버전 hello 기능 tooconfigure 기능 제공 **아키텍처**, hello 커넥터 tooits 기본 값 toorun 설정 되어 있는지 확인 **프로세스**합니다.

### <a name="connectivity"></a>연결
Hello 연결 페이지 hello Lotus Domino 서버 이름을 지정 하 고 hello 로그온 자격 증명을 입력 해야 합니다.  
![연결](./media/active-directory-aadconnectsync-connector-domino/connectivity.png)

hello Domino 서버 속성 hello 서버 이름에 대 한 두 가지 형식을 지원합니다.

* ServerName
* ServerName/DirectoryName

hello **ServerName/t o r y** hello 커넥터 연락처 Domino 서버 hello 때 더 빠른 응답이 제공 형식은이 특성에 대 한 hello 원하는 형식입니다.

hello 제공 UserID 파일 hello 동기화 서비스의 hello 구성 데이터베이스에 저장 됩니다.

**델타 가져오기** 의 경우 다음과 같은 옵션이 있습니다.

* **없음**. hello 커넥터 모든 델타 가져오기를 수행 하지 않습니다.
* **추가/업데이트**. hello 커넥터는 델타 가져오기 추가 및 업데이트 작업을 수행 합니다. 삭제의 경우 **전체 가져오기** 작업이 필요합니다. 이 작업은 hello.Net interop를 사용 합니다.
* **추가/업데이트/삭제**. hello 커넥터는 델타 가져오기 추가, 업데이트 및 삭제 작업입니다. 이 작업은 hello 네이티브 c + + 인터페이스를 사용 합니다.

**스키마 옵션** hello 다음 옵션을 사용 해야 합니다.

* **기본 스키마**. hello 커넥터 hello Domino 서버에서 hello 스키마를 검색합니다. 이 옵션을이 선택은 hello 기본 옵션입니다.
* **DSML-스키마**. Hello Domino 서버 hello 스키마를 표시 하지 않습니다 하는 경우에 사용 합니다. 그런 다음 hello 스키마와 함께 DSML 파일을 만들고 대신 가져올 수 있습니다. DSML에 대한 자세한 내용은 [OASIS](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=dsml)를 참조하세요.

다음을 클릭할 때 hello UserID 및 암호 구성 매개 변수 확인 됩니다.

### <a name="global-parameters"></a>글로벌 매개 변수
Hello 글로벌 매개 변수 페이지에서 hello 표준 시간대와 hello 가져오기를 구성 하 고 내보내기 작업 옵션입니다.  
![글로벌 매개 변수](./media/active-directory-aadconnectsync-connector-domino/globalparameters.png)

hello **Domino 서버 표준 시간대** Domino 서버의 hello 위치 매개 변수를 정의 합니다.

이 구성 옵션은 필요한 toosupport **델타 가져오기** 작업 hello 동기화 서비스 hello 마지막 두 개의 imports 간 변경 내용을 확인 지원 수 있기 때문입니다.

>[!Note]
Hello 2017 년 3 월 업데이트 hello 글로벌 매개 변수 화면부터 hello 사용자 삭제 중 hello 옵션 toodelete hello 사용자 메일 데이터베이스를 포함 됩니다.

![사용자 사서함 삭제](./media/active-directory-aadconnectsync-connector-domino/AdminP.png)

#### <a name="import-settings-method"></a>설정 가져오기 메서드
hello **다른 이름으로 전체 가져오기 수행** 는 다음과 같은이 옵션:

* 검색
* 보기(권장)

**검색** 는 Domino에 대 한 인덱싱을 사용 하는 hello 인덱스는 실시간으로 업데이트 되지 않습니다 및 hello 서버에서 반환 된 hello 데이터는 항상 올바른 자주 발생 합니다. 변경 사항이 많은 시스템의 경우 이 옵션은 일반적으로 잘 작동하지 않고 상황에 따라 잘못된 삭제가 발생합니다. 그러나 **검색**은 **보기**보다 빠릅니다.

**보기** hello 하므로 권장 옵션 hello 데이터의 올바른 상태를 제공 합니다. 검색 보다 다소 느립니다.

#### <a name="creation-of-virtual-contact-objects"></a>가상 연락처 개체 만들기
hello **을 만들 수 있도록 \_연락처 개체** 는 다음과 같은이 옵션:

* 없음
* 비참조 값
* 참조 및 비참조 값

Domino에서 다른 개체 참조 특성 많은 다양 한 형식 tooreference 포함할 수 있습니다. toobe 수 toorepresent 다른 변형 hello 커넥터 구현 \_연락처 개체를 라고도 **가상 연락처** (VC). 이러한 개체 tooexisting MV 개체 참여할 수 있도록 생성 되거나 새 개체로 프로젝션 합니다. 이러한 방식으로 특성 참조를 보존할 수 있습니다.

이 설정을 사용 하면 참조 특성의 hello 콘텐츠는 DN 형식 하지 않은 경우는 \_연락처 개체가 만들어집니다. 예를 들어 그룹의 멤버 특성은 SMTP 주소를 포함할 수 있습니다. 가능한 toohave shortName 이기도 및 참조 특성에 다른 특성이 존재 합니다. 이 시나리오의 경우 **비참조 값**을 선택합니다. 이 구성은 hello Domino 구현에 대 한 가장 일반적인 설정입니다.

Lotus Domino 구성된 toohave 별도 주소록 경우 hello 동일한 개체를 나타내는 다른 고유 이름으로, 가능한 tooalso 만들 \_주소록에 부여 된 모든 참조 값에 대 한 연락처 개체입니다. 이 시나리오에 대 한 선택 hello **참조 및 비 참조 값** 옵션입니다.

Hello 특성에 여러 값이 있는 경우 **FullName** Domino, 다음 시겠습니까 가상 연락처 tooenable hello 생성 참조가 확인 될 수 있도록 합니다. 예를 들어, 이 특성은 결혼 또는 이혼 후에 여러 값을 가질 수 있습니다. Hello 확인란을 선택 **사용... FullName은 이 시나리오에 대해 여러 값**을 포함합니다.

Hello 올바른 특성에 가입 하면 hello \_연락처 개체 조인된 toohello MV 개체 여야 합니다.

이들이 개체에는 VC =\_연락처 tootheir DN 추가 합니다.

#### <a name="import-settings-conflict-object"></a>설정 가져오기, 충돌 개체
**충돌 개체 제외**

큰 Domino 구현에서 여러 개체 tooreplication 문제 때문에 동일한 DN을 hello 있을 수는. 이러한 경우 hello 커넥터 두 개체의 다른 UniversalIDs 하지만 동일한 DN 표시 됩니다. 이 충돌 hello 커넥터 공간에 생성 되는 임시 개체를 리라 예상 되었습니다. hello 커넥터 복제 희생자도 Domino에서 선택 된 hello 개체를 무시할 수 있습니다. hello 권장 구성은 tookeep이 확인란이을 선택 합니다.

#### <a name="export-settings"></a>설정 내보내기
경우 hello 옵션 **참조 업데이트에 대 한 사용 AdminP** 를 선택 하지 않은, 참조 특성, 멤버 등의 내보내기는 직접 호출 되 고 hello AdminP 프로세스를 사용 하지 않습니다. AdminP 구성된 toomaintain 참조 무결성을 되지 않은 경우에이 옵션을 사용 합니다.

#### <a name="routing-information"></a>라우팅 정보
Domino, 되는 참조 특성에 포함 된 접미사 toohello DN으로 라우팅 정보가 있습니다. 예를 들어 hello member 특성 그룹에 포함할 수 **CN =example/organization@ABC**합니다. hello 접미사 @ABC hello 라우팅 정보입니다. hello 라우팅 정보를 사용 하 여 Domino toosend 메일 toohello 올바른 Domino 시스템에서 다른 조직에 있는 시스템 될 수 있습니다. Hello 라우팅 정보 필드에 hello 커넥터의 범위에 hello 조직 내에서 사용 된 hello 라우팅 접미사를 지정할 수 있습니다. 다음이 값 중 하나를 접미사로에서 있으면 참조 특성 hello 라우팅 정보 hello 참조에서 제거 됩니다. 참조 값에 대해 hello 라우팅 접미사를 지정 하는 이러한 값의 일치 하는 tooone 수 없는 경우는 \_연락처 개체가 만들어집니다. 이러한 \_연락처 개체를 사용 하 여 만들어진 **RO = @<RoutingSuffix>**  DN hello에 삽입 합니다. 이러한 \_hello 특성 다음 사항도 연락처 개체 추가 tooa 실제 개체를 필요한 경우 조인 tooallow: \_routingName, \_contactName \_displayName, 및 UniversalID 합니다.

#### <a name="additional-address-books"></a>추가 주소록
없는 경우 **안내** 보조 주소록의 hello 이름을 제공 하는 설치 된 후 이러한 주소록을 수동으로 입력할 수 있습니다.

#### <a name="multivalued-transformation"></a>다중값 변환
Lotus Domino의 많은 특성은 다중값입니다. hello 해당 메타 버스 특성은 일반적으로 단일 값입니다. Hello 가져오기 및 hello 내보내기 작업 옵션을 구성 하 여 사용 하도록 설정 하면 hello 커넥터 toohelp 필요한 hello 변환의 영향을 받는 hello 특성을 사용 합니다.

**내보내기**  
hello 내보내기 작업 옵션 두 가지 모드를 지원합니다.

* 항목 추가
* 항목 바꾸기

**항목 바꾸기** – Domino에이 옵션을 항상 hello 커넥터 제거 hello hello 특성의 현재 값을 선택 하 고 hello 제공 된 값으로 대체 합니다. 제공 하는 hello 단일 값 또는 다중값 가능 반환 합니다.

예: hello 도우미의 특성 person 개체는 다음 값에는 hello:

* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

라는 새 도우미 경우 **David Alexander** 는 hello 결과 toothis person 개체에 할당:

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf

**항목 추가** –이 옵션을 선택 하면 hello 커넥터는 hello 특성 hello 위쪽 hello 데이터 목록에 새 값을 삽입과 Domino에 hello 기존 값을 유지 합니다.

예: hello 도우미의 특성 person 개체는 다음 값에는 hello:

* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

라는 새 도우미 경우 **David Alexander** 는 hello 결과 toothis person 개체에 할당:

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf
* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

**가져오기**  
hello 가져오기 작업 옵션 두 가지 모드를 지원합니다.

* 기본값
* 다중값된 tooSingle 값

**기본** – hello 기본 옵션을 특성을 가져오는 모든 hello의 모든 값을 선택 합니다.

**다중값된 tooSingle 값** –이 옵션을 선택 하면 다중 값된 특성은 단일 값 특성으로 변환 됩니다. 둘 이상의 값이 있으면 (또한이 값은 일반적으로 hello 최신) hello 위에 hello 값이 사용 됩니다.

예: hello 도우미의 특성 person 개체는 다음 값에는 hello:

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf
* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

hello 가장 최근의 업데이트 toothis 특성은 **David Alexander**합니다. 커넥터만 가져옵니다 hello 작업 옵션 가져오기 tooMultivalued tooSingle 값에 설정 되어 있지만 **David Alexander** hello 커넥터 공간으로 합니다.

단일 값 특성으로 hello 논리 tooconvert 다중 값된 특성 toohello 그룹 멤버 특성 및 toohello 개인 fullname 특성에 적용 되지 않습니다.

그 가능한 tooconfigure 가져오고 특성 당 다중값된 특성에 대 한 변환 규칙 예외 toohello 전역 규칙으로 내보낼 수도 있습니다. tooconfigure이 옵션을 [objecttype]를 입력 합니다. [attributename] hello에 **제외 특성 목록을 가져올** 및 **제외 특성 목록 내보내기** 텍스트 상자입니다. 예를 들어 Person.Assistant를 입력 하 고 hello 전역 플래그를 tooimport를 설정 하는 경우 모든 값을 유일한 hello 첫 번째 값을 가져옵니다 hello 길잡이 대 한.

#### <a name="certifiers"></a>인증자
모든 조직/조직 구성 단위는 hello 커넥터에 의해 표시 됩니다. toobe 수 tooexport 사람 개체 toohello 기본 주소 주소록의 암호로 인증자가 필요 합니다.

모든 certifiers 있으면 hello 같은 암호를 hello **모든 Certifers에 대 한 암호** 사용할 수 있습니다. 다음 여기에 hello 암호를 입력 하 고만 hello 인증자 파일을 지정 합니다.

만 가져올 경우 다음 않아도 toospecify 모든 certifiers 합니다.

### <a name="configure-provisioning-hierarchy"></a>프로비전 계층 구성
Hello Lotus Domino 커넥터를 구성할 때이 대화 상자 페이지를 건너뜁니다. Lotus Domino 커넥터 hello 프로 비전 하는 계층 구조를 지원 하지 않습니다.  
![프로비전 계층 구조](./media/active-directory-aadconnectsync-connector-domino/provisioninghierarchy.png)

### <a name="configure-partitions-and-hierarchies"></a>파티션 및 계층 구조 구성
파티션 및 계층 구조를 구성 하면 hello 기본 주소록 NAB=names.nsf 호출을 선택 해야 합니다. 또한 toohello 기본 주소록을 선택할 수 있습니다 주소록 보조 사이트가 있는 경우.  
![파티션](./media/active-directory-aadconnectsync-connector-domino/partitions.png)

### <a name="select-attributes"></a>특성 선택
특성을 구성할 때 **\_MMS\_**라는 접두사가 붙은 모든 특성을 선택해야 합니다. 새 개체 tooLotus Domino 프로 비전 할 때 이러한 특성은 필요

![특성](./media/active-directory-aadconnectsync-connector-domino/attributes.png)

## <a name="object-lifecycle-management"></a>개체 수명 주기 관리
이 섹션에서는 hello 다양 한 개체 Domino에 대 한 개요를 제공 합니다.

### <a name="person-objects"></a>사용자 개체
hello person 개체 조직 및 조직 구성 단위에 사용자를 나타냅니다. 또한 toohello 기본 특성을 Domino 관리자에 게 사용자 지정 특성 tooa Person 개체를 추가할 수 있습니다. 최소한 사용자 개체는 모든 필수 특성을 포함해야 합니다. 필수 특성의 전체 목록은 [Lotus Notes 속성](#lotus-notes-properties)을 참조하세요. tooregister person 개체 hello 다음 필수 구성 요소를 충족 되어야 합니다.

* hello 주소록 (names.nsf) 정의 되어 있어야 하며 hello 기본 주소록 해야 합니다.
* Hello O/OU 인증자 Id와 hello 암호 tooregister 특정 사용자에에서 있어야 hello 조직 / 조직 구성 단위입니다.
* 사용자 개체에 대해 Lotus Notes 속성의 특정 집합을 설정해야 합니다. 이러한 속성은 hello person 개체를 프로 비전에 사용 됩니다. 자세한 내용은 호출 하는 hello 섹션을 참조 하십시오. [Lotus Notes 속성](#lotus-notes-properties) 이 문서의 뒷부분에 나오는 합니다.
* hello 초기 HTTP에 대 한 사용자 암호가 특성과 집합 프로 비전 중입니다.
* hello person 개체 hello 다음 세 가지 지원 되는 형식 중 하나 여야 합니다.
  1. 메일 파일 및 사용자 ID 파일을 포함하는 일반 사용자
  2. 로밍 사용자(로밍하는 모든 데이터베이스파일을 포함하는 일반 사용자)
  3. 연락처(ID 파일이 없는 사용자)

(연락처 제외) 사원 추가로으로 그룹화 할 수 미국 사용자와 International 사용자 hello hello 값에 의해 정의 된 대로 \_MMS\_IDRegType 속성입니다. 이러한 사용자는 hello Notes 클라이언트 tooaccess Lotus Domino 서버를 사용 하 여, 메모 Id 및 개인 문서. Notes 메일을 사용 중인 경우 메일 파일도 갖게 됩니다. hello 사용자 등록된 toobecome 활성 이어야 합니다. 자세한 내용은 다음을 참조하세요.

* [Notes 사용자 설정](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_SETTING_UP_NOTES_USERS.html)
* [사용자 등록](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_REGISTERING_USERS.html)
* [사용자 관리](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_USERS_5151.html)
* [사용자 이름 바꾸기](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_USER_AUTOMATICALLY.html)

이 작업은 모두 Lotus Domino에서 수행 되며 다음 hello 동기화 서비스도 가져옵니다.

### <a name="resources-and-rooms"></a>리소스 및 공간
리소스는 Lotus Domino에 있는 데이터베이스의 다른 형식입니다. 리소스는 프로젝터와 같은 다양한 유형의 장비가 있는 회의실일 수 있습니다. Hello 리소스 종류 특성에 의해 정의 된 Lotus Domino 커넥터에서 지 원하는 리소스의 하위 유형이 있습니다.

| 리소스의 형식 | 리소스 형식 특성 |
| --- | --- |
| 공간 |1 |
| 리소스(기타) |2 |
| 온라인 모임 |3 |

Hello 리소스 개체 유형 toowork hello 다음이 필요 합니다.

* 리소스 예약 데이터베이스 연결 hello Domino 서버에 이미 존재 합니다.
* hello 리소스에 대해 이미 정의 된 hello 사이트가

hello 리소스 예약 데이터베이스는 세 가지 유형의 문서 포함 되어 있습니다.

* 사이트 프로필
* 리소스
* 예약

리소스 예약 데이터베이스의 설정에 대 한 자세한 내용은 참조 하십시오. [hello 리소스 예약 데이터베이스 설정](https://www-01.ibm.com/support/knowledgecenter/SSKTMJ_8.0.1/com.ibm.help.domino.admin.doc/DOC/H_SETTING_UP_THE_RESOURCE_RESERVATIONS_DATABASE.html)합니다.

**리소스 만들기, 업데이트 및 삭제**  
hello Create, Update 및 Delete 작업 수행 됩니다 hello 리소스 예약 데이터베이스의 hello Lotus Domino 커넥터에서. 리소스 (즉, hello 기본 주소록) Names.nsf의 문서도 생성 됩니다. 리소스를 편집 및 삭제하는 방법에 대한 자세한 내용은 [리소스 문서 편집 및 삭제](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_EDITING_AND_DELETING_RESOURCE_DOCUMENTS.html)를 참조하세요.

**리소스에 대한 작업 가져오기 및 내보내기**  
hello 리소스는 다른 개체 형식 처럼 hello 동기화 서비스에서 내보낸 가져온된 tooand 될 수 있습니다. 리소스로 개체 유형 선택 hello 구성 하는 중입니다. 성공적인 내보내기 작업의 경우 리소스 형식, 회의 데이터베이스 및 사이트 이름에 대한 세부 정보가 있어야 합니다.

### <a name="mail-in-databases"></a>메일 내 데이터베이스
메일에서 데이터베이스에는 디자인 된 tooreceive 메일 있는 데이터베이스입니다. 특정 Lotus Domino 사용자 계정과 연결되지 않은 Lotus Domino 사서함입니다(즉, 고유한 파일 ID 및 암호 없음). 메일 내 데이터베이스는 자신 및 전자 메일 주소와 연관된 고유한 사용자 ID("짧은 이름")입니다.

여러 사용자들 간에 공유할 수 있는 고유한 전자 메일 주소를 사용하는 개별 사서함을 필요로 하지 않는 경우(예: group@contoso.com) 메일 내 데이터베이스를 만듭니다. hello 액세스 toothis 사서함을 통해 해당 목록 ACL (액세스 제어)를 허용 되는 tooopen hello 사서함 hello Notes 사용자의 hello 이름이 포함 된 제어 됩니다.

목록이 필요한 hello 특성에 대 한 호출 hello 섹션을 참조 [필수 특성](#mandatory-attributes) 이 문서의 뒷부분에 나오는 합니다.

데이터베이스 메일을 설계 된 tooreceive 이면 데이터베이스 메일의 문서 Lotus Domino에 만들어집니다. 이 문서는 hello 데이터베이스의 복사본을 저장 하는 모든 서버의 Domino 디렉터리에 있어야 합니다. 메일 내 데이터베이스 문서를 만드는 자세한 내용은 [메일 내 데이터베이스 문서 만들기](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_A_MAILIN_DATABASE_DOCUMENT_FOR_A_NEW_DATABASE_OVERVIEW.html)를 참조하세요.

이미 존재 해야 hello 데이터베이스 메일에서 데이터베이스를 만들기 전에 (만들어야 Lotus 관리자) hello Domino 서버에 있습니다.

### <a name="group-management"></a>그룹 관리
다음 리소스는 hello에서 hello Lotus Domino 그룹 관리에 대 한 세부적인된 개요를 얻을 수 있습니다.

* [그룹 사용](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_USING_GROUPS_OVER.html)
* [그룹 만들기](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS_MIDTOPIC_55038956829238418.html)
* [그룹 만들기 및 수정](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS.html)
* [그룹 관리](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_GROUPS_1804.html)
* [그룹 이름 바꾸기](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_GROUP_STEPS.html)

### <a name="password-management"></a>암호 관리
등록된 Lotus Domino 사용자의 경우 두 가지 형식의 암호가 있습니다.

1. 사용자 암호(User.id 파일에 저장됨)
2. 인터넷/HTTP 암호

hello Lotus Domino 커넥터 HTTP 암호로 작업만 지원합니다.

tooperform 암호 관리 hello 커넥터에서 관리 에이전트 디자이너 hello에 대 한 암호 관리를 사용 해야 합니다. tooenable 암호 관리를 선택 **암호 관리를 사용 하도록 설정** hello에 **확장 구성** 대화 상자 페이지입니다.  
![암호 관리 사용](./media/active-directory-aadconnectsync-connector-domino/configureextensions.png)

Lotus Domino 커넥터 지원 hello 인터넷 암호에 대 한 작업 수행:

* 암호 설정: 암호 설정 hello 사용자 Domino에 새 HTTP/인터넷 암호를 설정합니다. 기본적으로 hello 계정이 잠겨 있지 않은 합니다. hello 플래그를 잠금 해제 hello 동기화 엔진의 hello WMI 인터페이스에 노출 됩니다.
* 암호 변경:이 시나리오에서는 사용자 toochange hello 암호 하거나 지정된 된 시간 후 증명된 toochange 암호입니다. 이 작업 tootake 환경에 대 한 모두 이전 hello와 hello 새 암호는 필수입니다. 이 변경 되 면 hello 새 암호 Lotus Domino에 업데이트 됩니다.

자세한 내용은 다음을 참조하세요.

* [Hello 인터넷 잠금 기능을 사용 하 여](http://www.ibm.com/developerworks/lotus/library/domino8-lockout/)
* [인터넷 암호 관리](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_NOTES_AND_INTERNET_PASSWORD_SYNCHRONIZATION_7570_OVER.html)

## <a name="reference-information"></a>참조 정보
이 섹션 예: 특성 설명 및 hello Lotus Domino 커넥터에 대 한 특성 요구 사항을 나열합니다.

### <a name="lotus-notes-properties"></a>Lotus Notes 속성
사람 개체 tooyour Lotus Domino 디렉터리의 프로 비전 할 때 개체 채워진 특정 값을 가진 특정 속성 집합이 있어야 합니다. 이러한 값은 만들기 작업에 필요합니다.

hello 다음 표에 이러한 속성 목록과 대 한 설명을 제공 합니다.

| 속성 | 설명 |
| --- | --- |
| \_MMS_AltFullName |hello 사용자의 대체 전체 이름입니다. |
| \_MMS_AltFullNameLanguage |hello 언어 toobe hello 사용자의 대체 전체 이름을 지정 하는 데 사용 합니다. |
| \_MMS_CertDaysToExpire |hello부터의 일 수 hello hello 인증서 하기 전에 현재 날짜에 만료 됩니다. 지정 하지 않으면 hello 기본 날짜는 현재 날짜 hello에서 2 년입니다. |
| \_MMS_Certifier |Hello 인증자의 hello 조직 계층 이름을 포함 하는 속성입니다. 예: OU=OrganizationUnit, O=조직, C=국가. |
| \_MMS_IDPath |Hello 속성이 비어 사용자 식별 파일이 hello 동기화 서버에 로컬로 만들어집니다. Hello 속성에는 파일 이름이 있으면 사용자 ID 파일 hello madata 폴더에 만들어집니다. hello 속성의 전체 경로 포함할 수도 있습니다. |
| \_MMS_IDRegType |개인은 연락처, 미국 사용자 및 국제 사용자로 분류할 수 있습니다. hello 다음 표에 나타난 hello 가능한 값. <li>0 - 연락처</li><li>1 - 미국 사용자</li><li>2 - 국제 사용자</li> |
| \_MMS_IDStoreType |미국 및 국제 사용자에 대한 필수 속성입니다. hello 속성 hello 사용자 id 또는 hello 사람의 메일 파일 hello Notes 주소록의 첨부 파일로 저장 되는지 여부를 지정 하는 정수 값을 포함 합니다. Hello 사용자 ID 파일 hello 주소록에 첨부 파일을 경우 필요에 따라 만들 수 있습니다을 가진 파일로 \_MMS_IDPath 합니다. <li>비어 있음 - ID 자격 증명 모음의 저장소 ID 파일, ID 파일 없음(연락처에 사용됨)</li><li> 1-hello 메모 주소록에 첨부 파일입니다. hello \_사용자 식별 파일 첨부 파일에 대 한 MMS_Password 속성을 설정 해야 합니다</li><li>2 - 사용자의 메일 파일의 저장소 ID입니다. hello \_MMS_UseAdminP toofalse toolet hello 메일을 설정 해야 hello 사람 등록 하는 동안 파일을 만들 수 있습니다. hello \_사용자 식별 파일에 대 한 MMS_Password 속성을 설정 해야 합니다.</li> |
| \_MMS_MailQuotaSizeLimit |hello 전자 메일에서 데이터베이스 파일에 허용 되는 메가바이트 hello 수입니다. |
| \_MMS_MailQuotaWarningThreshold |경고가 발생 하기 전에 hello 전자 메일에서 데이터베이스 파일에 허용 되는 메가바이트 hello 수입니다. |
| \_MMS_MailTemplateName |hello 전자 메일 템플릿 파일을 사용 하는 toocreate hello 사용자의 전자 메일 파일입니다. 템플릿이 지정 된 hello 지정 된 템플릿을 사용 하 여 hello 메일 파일이 만들어집니다. 서식 파일이 없는 지정 된 경우 hello 기본 서식 파일은 사용 되는 toocreate hello 파일입니다. |
| \_MMS_OU |선택적 속성 hello 인증자에서 hello OU 이름입니다. 이 속성은 연락처에 대해 비어 있어야 합니다. |
| \_MMS_Password |사용자에 대한 필수 속성입니다. hello 속성 hello 개체의 hello 식별 파일에 대 한 hello 암호를 포함합니다. |
| \_MMS_UseAdminP |Hello Domino 서버 (비동기 toohello 내보내기 프로세스)에서 hello AdminP 프로세스가 hello 메일 파일을 만들 경우 속성 집합 tootrue 해야 합니다. 속성이 toofalse, hello 메일 파일이 만들어집니다 hello로 Domino 사용자 (hello 내보내기 프로세스에서 동기). |

관련된 식별 파일이 있는 사용자가 hello \_MMS_Password 속성 값을 포함 해야 합니다. Lotus Notes 클라이언트 hello 통해 전자 메일 액세스를 메일 서버 hello 및 사용자의 MailFile 속성 값을 포함 해야 합니다.

웹 브라우저를 통해 전자 메일 tooaccess hello 다음과 같은 속성 값을 포함 해야 합니다.

* MailFile-hello 메일 파일이 저장 된 hello Lotus Domino 서버의 hello 경로 포함 하는 필수 속성입니다.
* 메일 서버-hello Lotus Domino 서버 hello 이름을 포함 하는 필수 속성입니다. 이 기간은 hello 이름 toouse hello Domino 서버의 hello Lotus 메일 파일을 만들 때입니다.
* HTTPPassword-hello 개체에 대 한 hello 웹 액세스 암호를 포함 하는 선택적 속성입니다.

tooaccess 메일 기능 없이 Domino 서버 hello, hello HTTPPassword 속성 값을 포함 해야 합니다. MailFile 속성 hello 및 hello 메일 서버 속성을 비워 둘 수 있습니다.

와 \_MMS_ IDStoreType (메일 파일에서 store id), 2 = hello NotesRegistrationclass MailSystem 속성 tooREG_MAILSYSTEM_INOTES (3)을 설정 합니다.

### <a name="mandatory-attributes"></a>필수 특성
hello Lotus Domino 커넥터는 주로 이러한 유형의 개체 (문서 형식)를 지원합니다.

* 그룹
* 메일 내 데이터베이스
* 사람
* 연락처(인증자가 없는 사용자)
* 리소스

이 섹션에는 각 지원 되는 개체 tooexport tooa Domino 서버에 대 한 필수 hello 속성이 나열 됩니다.

| 개체 유형 | 필수 특성 |
| --- | --- |
| 그룹 |<li>ListName</li> |
| Main-In 데이터베이스 |<li>FullName</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |
| 사람 |<li>LastName</li><li>MailFile</li><li>ShortName</li><li>\_MMS_Password</li><li>\_MMS_IDStoreType</li><li>\_MMS_Certifier</li><li>\_MMS_IDRegType</li><li>\_MMS_UseAdminP</li> |
| 연락처(인증자가 없는 사용자) |<li>\_MMS_IDRegType</li> |
| 리소스 |<li>FullName</li><li>ResourceType</li><li>ConfDB</li><li>ResourceCapacity</li><li>사이트</li><li>displayName</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |

## <a name="common-issues-and-questions"></a>일반적인 문제 및 질문
### <a name="schema-detection-does-not-work"></a>스키마 검색이 작동하지 않습니다.
toobe 수 toodetect hello 스키마는 hello schema.nsf이 파일은 hello Domino 서버에 있습니다. 이 파일 LDAP hello 서버에 설치 된 경우에 나타납니다. Hello 스키마를 검색할 수 없는 경우 hello 다음을 확인 합니다.

* hello Domino 서버의 hello 루트 폴더에 hello 파일 schema.nsf 있으면
* hello 사용자에 게 권한 toosee hello schema.nsf 파일.
* Hello LDAP 서버를 다시 시작을 강제 적용 합니다. 열기 **Lotus Domino 콘솔** 사용 하 여 **LDAP ReloadSchema 알** 명령 tooreload hello 스키마입니다.

### <a name="not-all-secondary-address-books-are-visible"></a>일부 보조 주소록이 표시되지 않습니다.
hello Domino 커넥터에는 hello 기능 **안내** toobe 수 toofind hello 보조 주소록 합니다. Hello 보조 주소록 경우를 확인 하는 경우 [안내](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_DIRECTORY_ASSISTANCE.html) 사용 하도록 설정 되었으며 Domino 서버 hello에 구성 합니다.

### <a name="custom-attributes-in-domino"></a>Domino의 사용자 지정 특성
여러 가지가 Domino tooextend hello 스키마의 hello 커넥터에서 사용 될 사용자 지정 특성으로 표시 되도록 합니다.

**접근 방식1: Lotus Domino 스키마 확장**

1. Domino {PUBNAMES 디렉터리 서식 파일의 복사본 만들기. NTF} 따라 [이러한 단계](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (하지 사용자 지정 해야 hello 기본 IBM Lotus Domino 디렉터리 서식 파일):
2. 열기 hello Domino 복사 디렉터리 템플릿 {CONTOSO. Domino 디자이너에서 만든와 다음이 단계를 수행 하는 NTF} 템플릿:
   * 공유 요소를 클릭하고 하위 폼을 확장합니다.
   * ${ObjectName} InheritableSchema 하위 폼을 두 번 클릭 (여기서 {ObjectName}은 hello 이름 hello 기본 구조 개체 클래스의 예: 사용자).
   * {MyPersonAtrribute (를) 스키마로 tooadd 원하는 hello 특성 및 해당 toothat 특성 이름을 지정 합니다. Hello 선택 하 여 필드를 만들어 **만들기** 메뉴와 선택 **필드** 메뉴에서 합니다.
   * Hello 추가 된 필드를 해당 유형, 스타일, 크기, 글꼴 및 필드 속성 창에서 기타 관련된 매개 변수를 선택 하 여 해당 속성을 설정 합니다.
   * 해당 특성에 대해 지정 된 hello 이름으로 동일를 기본값 유지 hello 특성 (특성 이름이 MyPersonAttribute 이면 hello로 hello 기본값을 유지 예를 들어 이름이 같은).
   * 업데이트 된 값으로 hello ${ObjectName} InheritableSchema 하위 폼을 저장 합니다.
3. Hello Domino 디렉터리 템플릿을 {PUBNAMES 바꾸기. NTF} hello 새 사용자 지정된 템플릿을 {CONTOSO와. NTF} 따라 [이러한 단계](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html)합니다.
4. Domino 관리자를 닫고 Domino 콘솔 toorestart hello LDAP 서비스를 열고 tooReload hello LDAP 스키마:
   * Domino 콘솔에서에서 hello 명령을 삽입 **Domino 명령** toorestart hello LDAP 서비스-필드 텍스트 [다시 시작 작업 LDAP](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html)합니다.
   * tooreload LDAP 스키마 명령을 사용 하 여 LDAP 알-LDAP ReloadSchema 설명
5. 열기 Domino 관리자 및 사용자 및 그룹 탭 toosee 선택 특성 사람 추가 domino에 반영 되어 추가.
6. **파일** 탭에서 Schema.nsf를 열고 추가된 특성이 dominoPerson LDAP 개체 클래스에 반영된 것을 확인합니다.

**방법 2: 사용자 지정 특성을 가진는 auxClass 만들고 hello 개체 클래스와 연결**

1. Domino {PUBNAMES 디렉터리 서식 파일의 복사본 만들기. NTF} 따라 [이러한 단계](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (하지 hello 기본 IBM Lotus Domino 디렉터리 템플릿 사용자 지정):
2. 열기 hello Domino 복사 디렉터리 템플릿 {CONTOSO. Domino 디자이너에서 만든 NTF} 템플릿.
3. Hello 왼쪽된 창에서 공유 코드와 다음 하위 폼을 선택 합니다.
4. 새 하위 폼을 클릭합니다.
5. 다음 하위 hello 새 폼에 대 한 toospecify hello 속성 hello 마십시오.
   * 새 하위 폼 hello 열어 둔 설계-하위 폼 속성을 선택
   * 다음 toohello Name 속성의 예를 들어 TestSubform hello 보조 개체 클래스에 대 한 이름을 입력 합니다.
   * "포함" Insert 하위에서... 대화 상자 선택 hello Options 속성 유지
   * "렌더링 메모에 HTML을 통해 전달 됩니다." hello Options 속성을 선택 취소
   * 다른 leave hello 속성 동일 hello 및 hello 하위 폼 속성 상자를 닫습니다.
   * 저장 하 고 hello 새 폼을 닫습니다.
6. Tooadd 필드 toodefine hello 보조 개체 클래스에 다음 hello 수행:
   * 만든 hello 하위 폼을 엽니다.
   * 만들기 - 필드를 선택합니다.
   * Hello 기본 사항 탭 hello 필드 대화 상자에서 다음 tooName 이름은 원하는 대로 지정 예: {MyPersonTestAttribute}.
   * Hello 추가 된 필드 형식, 스타일, 크기, 글꼴 및 관련된 속성을 선택 하 여 해당 속성을 설정 합니다.
   * 해당 특성에 대해 지정 된 hello 이름으로 동일를 기본값 유지 hello 특성 (특성 이름이 MyPersonTestAttribute 이면 hello로 hello 기본값을 유지 예를 들어 이름이 같은).
   * 업데이트 된 값이 포함 된 hello 하위 폼을 저장 하 고 다음 hello지 않습니다.
     * Hello 왼쪽된 창에서 코드 공유를 선택한 후 폼
     * Hello 새 폼을 선택 하 고 디자인-디자인 속성을 선택 합니다.
     * Hello hello 왼쪽에서 세 번째 탭을 클릭 하 고 선택 **디자인 변경의 이러한 금지 전파**합니다.
7. (여기서 {ObjectName}는 hello 기본 구조 개체 클래스, 예를 들어 – 사용자의 hello 이름) ${ObjectName} ExtensibleSchema 하위 폼을 엽니다.
8. 리소스 삽입 hello (사용자가 만든 예 – TestSubform) 하위 폼을 선택 하 고 hello ${ObjectName} ExtensibleSchema 하위 폼을 저장 합니다.
9. Hello Domino 디렉터리 템플릿을 {PUBNAMES 바꾸기. NTF} hello 새 사용자 지정된 템플릿을 {CONTOSO와. NTF} 따라 [이러한 단계](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html)합니다.
10. Domino 관리자를 닫고 Domino 콘솔 toorestart hello LDAP 서비스를 열고 tooReload hello LDAP 스키마:
    * Domino 콘솔에서에서 hello 명령을 삽입 **Domino 명령** toorestart hello LDAP 서비스-필드 텍스트 [다시 시작 작업 LDAP](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html)합니다.
    * tooreload LDAP 스키마 알 LDAP 명령을 사용 하 여 **LDAP ReloadSchema 알**합니다.
11. 열기 Domino 관리자 및 사용자 및 그룹 탭 toosee 선택 추가 특성 사람 추가 domino에 반영 됩니다 (아래 다른 탭).
12. **파일** 탭에서 Schema.nsf를 열고 추가된 특성이 TestSubform LDAP 보조 개체 클래스에 반영된 것을 확인합니다.

**방법 3: hello 사용자 지정 특성 toohello ExtensibleObject 클래스 추가**

1. Hello 루트 디렉터리에 배치 하는 {Schema.nsf} 파일 열기
2. LDAP 개체 클래스 아래 hello 왼쪽된 메뉴에서 선택 **모든 스키마 문서** 클릭 **개체 추가 클래스** 단추:
3. Hello 형태의 {zzzExtensibleSchema} (여기서 zzz는 hello 기본 구조 개체 클래스, 예를 들어 사용자의 hello 이름)에 대 한 LDAP 이름을 제공 합니다. 예를 들어 Person 개체 클래스에 대 한 tooextend hello 스키마 LDAP 이름 {PersonExtensibleSchema}를 제공 합니다.
4. 보려는 tooextend hello 스키마를 상위 개체 클래스 이름을 제공 합니다. 예를 들어 Person 개체 클래스에 대 한 tooextend hello 스키마 상위 개체 클래스 이름 {dominoPerson}를 제공 합니다.
5. 유효한 OID 해당 toohello 개체 클래스를 제공 합니다.
6. 확장/사용자 지정 특성 hello 요구 사항에 따라 필수 또는 선택적 특성 유형 필드에서 선택 합니다.
7. 필요한 추가 toohello ExtensibleObjectClass 특성이 있는 경우 클릭 **저장 후 닫기**합니다.
8. ExtensibleObjectClass는 확장된 특성이 있는 각 기본 개체 클래스에 대해 생성됩니다.

## <a name="troubleshooting"></a>문제 해결
* 참조 hello tooenable 로깅 tootroubleshoot 커넥터 hello 하는 방법에 대 한 내용은 [어떻게 커넥터에 대 한 ETW 추적 tooEnable](http://go.microsoft.com/fwlink/?LinkId=335731)합니다.

---
title: "Azure Multi-factor Authentication 및 Active Directory 간의 aaaDirectory 통합"
description: "Hello 디렉터리를 동기화 할 수 있도록 Active Directory와 Azure Multi-factor Authentication 서버 toointegrate hello 하는 방법을 설명 하는 hello Azure multi-factor authentication 페이지입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: def7a534-cfb2-492a-9124-87fb1148ab1f
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fbff518b4641010d5f7745096e0ff658864d0805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="directory-integration-between-azure-mfa-server-and-active-directory"></a>Azure MFA 서버와 Active Directory 간의 디렉터리 통합
Active Directory 또는 다른 LDAP 디렉터리와 Azure MFA 서버 toointegrate hello의 hello 디렉터리 통합 섹션을 사용 합니다. 특성 toomatch hello directory 스키마를 구성 하 고 자동 사용자 동기화를 설정할 수 있습니다.

## <a name="settings"></a>설정
기본적으로 Azure Multi-factor Authentication (MFA) 서버 hello 구성된 tooimport 되었거나 Active Directory에서 사용자를 동기화 합니다.  hello 디렉터리 통합 탭 하면 toooverride hello 기본 동작 및 toobind tooa 다른 LDAP 디렉터리, ADAM 디렉터리 또는 특정 Active Directory 도메인 컨트롤러에 있습니다.  또한 IIS 인증 또는 사용자 포털에 대 한 기본 인증을 위한 사전 인증 RADIUS 대상으로 LDAP 바인딩 또는 LDAP 인증 tooproxy LDAP의 hello로 제공합니다.  다음 표에서 hello hello 개별 설정에 설명 합니다.

![설정](./media/multi-factor-authentication-get-started-server-dirint/dirint.png)

| 기능 | 설명 |
| --- | --- |
| Active Directory 사용 |가져오기 및 동기화에 대 한 hello 사용 하 여 Active Directory 옵션 toouse Active Directory를 선택 합니다.  Hello 기본 설정입니다. <br>참고: 위해 Active Directory 통합 toowork 제대로 조인 hello 컴퓨터 tooa 도메인 및 도메인 계정으로 로그인 합니다. |
| 트러스트된 도메인 포함 |확인 **신뢰할 수 있는 도메인 포함** toohave hello 에이전트 시도 tooconnect toodomains hello 현재 도메인, 다른 hello 포리스트에 있는 도메인 또는 포리스트 트러스트에 관련 된 도메인에서 신뢰 합니다.  가져오거나 있는 hello에서 사용자를 동기화 하지 않으면 트러스트 된 도메인, hello 확인란 tooimprove 성능 선택 취소 합니다.  hello 기본적으로 선택 되어 있습니다. |
| 특정 LDAP 구성 사용 |Hello LDAP 사용 옵션 toouse hello LDAP 설정을 가져오기와 동기화에 대해 지정 된 선택 합니다. 참고: LDAP 사용 옵션을 선택 하면 hello 사용자 인터페이스 참조에서에서 변경 Active Directory tooLDAP 합니다. |
| 편집 단추 |hello 편집 단추 hello 현재 LDAP 구성 설정을 toomodified를 사용 합니다. |
| 특성 범위 쿼리 사용 |특성 범위 쿼리 사용 여부를 나타냅니다.  특성 범위 쿼리 조건에 맞는 레코드 hello 항목 다른 레코드의 특성에 기반한 효율적인 디렉터리 검색을 허용 합니다.  hello Azure Multi-factor Authentication 서버에서는 특성 범위 쿼리 tooefficiently 쿼리 hello 된 사용자 보안 그룹의 구성원을 사용 합니다.   <br>참고: 특성 범위 쿼리가 지원되지만 사용하지 말아야 하는 몇 가지 경우가 있습니다.  예를 들어 Active Directory는 보안 그룹에 둘 이상의 도메인에 속한 구성원이 포함되어 있는 경우 특성 범위 쿼리에 문제가 있을 수 있습니다. 이 경우 hello 확인란 선택을 취소 합니다. |

다음 표에서 hello hello LDAP 구성 설정을 설명 합니다.

| 기능 | 설명 |
| --- | --- |
| 서버 |Hello 호스트 이름 또는 hello LDAP 디렉터리를 실행 하는 hello 서버의 IP 주소를 입력 합니다.  세미콜론으로 구분하여 백업 서버를 지정할 수도 있습니다. <br>참고: 바인딩 종류가 SSL일 때 정규화된 호스트 이름이 필요합니다. |
| 기본 DN |Hello 모든 디렉터리 쿼리 시작할 hello 기본 디렉터리 개체의 고유 이름을 입력 합니다.  예를 들어 dc=abc,dc=com입니다. |
| 바인딩 종류 - 쿼리 |Toosearch hello LDAP 디렉터리에 바인딩할 때 사용 하기 위해 hello 적절 한 바인딩 종류를 선택 합니다.  이 방식은 가져오기, 동기화 및 사용자 이름 확인에 사용됩니다. <br><br>  익명 - 익명 바인딩이 수행됩니다.  바인딩 DN과 바인딩 암호는 사용되지 않습니다.  Hello LDAP 디렉터리가 익명 바인딩을 허용 권한 hello hello 적절 한 레코드와 특성을 쿼리할 수 있는 경우에 작동 합니다.  <br><br> 단순-바인딩 DN 및 바인딩 암호가 일반 텍스트로 toobind toohello LDAP 디렉터리로 전달 됩니다.  이 테스트 목적으로 서버 hello tooverify에 연결할 수 있고, 해당 hello 바인딩 계정에 hello 적절 한 액세스. Hello 적절 한 인증서를 설치한 후 SSL을 대신 사용 합니다.  <br><br> SSL-바인딩 DN 및 바인딩 암호가 SSL toobind toohello LDAP 디렉터리를 사용 하 여 암호화 됩니다.  LDAP 디렉터리 트러스트 hello 하는 인증서를 로컬로 설치 합니다.  <br><br> Windows-바인딩 사용자 이름과 바인딩 암호 tooan Active Directory 도메인 컨트롤러 또는 ADAM 디렉터리 사용 되는 toosecurely 연결 됩니다.  바인딩 사용자 이름을 비워 두면 hello 로그온 한 사용자의 계정은 사용된 toobind입니다. |
| 바인딩 종류 - 인증 |LDAP 바인딩 인증을 수행할 때 사용 하기 위해 hello 적절 한 바인딩 종류를 선택 합니다.  바인딩 유형-쿼리 아래의 hello 바인딩 종류 설명을 참조 하십시오.  예를 들어 이렇게 하면 SSL 바인딩은 LDAP 바인딩 인증을 사용 하는 toosecure는 쿼리에 사용 되는 익명 바인딩 toobe 있습니다. |
| 바인딩 DN 또는 바인딩 사용자 이름 |Toohello LDAP 디렉터리에 바인딩할 때 계정 toouse hello에 대 한 hello 사용자 레코드의 hello 고유 이름을 입력 합니다.<br><br>hello 바인딩 고유 이름은 바인딩 유형이 단순 또는 SSL 일 때만 사용 됩니다.  <br><br>바인딩 종류가 Windows 일 때 toohello LDAP 디렉터리에 바인딩할 때 hello Windows 계정 toouse의 hello 사용자 이름을 입력 합니다.  비워두는 경우 hello 로그온 한 사용자의 계정은 사용된 toobind입니다. |
| 바인딩 암호 |바인딩 DN hello에 대 한 hello 바인딩 암호 또는 사용자 이름을 사용 하는 toobind toohello LDAP 디렉터리 되 고를 입력 합니다.  Multi-factor Auth 서버 AdSync 서비스 hello에 대 한 tooconfigure hello 암호 동기화를 사용 하도록 설정 하 고 hello 서비스 hello 로컬 컴퓨터에서 실행 되 고 있는지 확인 합니다.  hello 암호 Multi-factor Auth 서버 AdSync 서비스는으로 실행 되는 hello 계정 hello hello Windows 저장 된 사용자 이름 및 암호에 저장 됩니다.  Multi-factor Auth 서버 사용자 인터페이스에서 hello 계정 hello Multi-factor Auth 서버 서비스 및 권한으로 실행으로 실행 되 고 hello 계정 hello hello 암호도 저장 됩니다.  <br><br>Hello 암호는 hello 로컬 서버의 Windows 저장 된 사용자 이름 및 암호에 저장 됩니다, 되므로 액세스 toohello 암호를 필요로 하는 각 Multi-factor Auth 서버에서이 단계를 반복 합니다. |
| 쿼리 크기 제한 |Hello 디렉터리 검색에서 반환 하는 사용자의 최대 수에 대 한 hello 크기 제한을 지정 합니다.  이 제한은 hello LDAP 디렉터리의 hello 구성과 일치 해야 합니다.  페이징이 지원 되지 않는 대규모 검색, 가져오기 및 동기화 tooretrieve 일괄로 사용자를에서 시도 합니다.  여기에 지정 된 hello 크기 제한을 hello LDAP 디렉터리에 구성 된 hello 제한 보다 큰, 일부 사용자가 놓칠 수 있습니다. |
| 테스트 단추 |클릭 **테스트** tootest 바인딩 toohello LDAP 서버.  <br><br>Tooselect hello 않아도 **LDAP 사용** tootest 바인딩 옵션. 따라서 hello 바인딩 toobe를 hello LDAP 구성을 사용 하기 전에 테스트할 수 있습니다. |

## <a name="filters"></a>필터
필터를 사용 하면 tooset 조건 tooqualify 레코드 디렉터리 검색을 수행 하는 경우.  Hello 필터를 설정 하 여 범위를 지정 하면 hello toosynchronize를 원하는 개체입니다.  

![필터](./media/multi-factor-authentication-get-started-server-dirint/dirint2.png)

Azure Multi-factor Authentication에는 다음 3 개의 필터 옵션 hello에 있습니다.

* **컨테이너 필터** -hello 필터 기준을 디렉터리 검색을 수행할 때 컨테이너 레코드 tooqualify 사용을 지정 합니다.  Active Directory 및 ADAM의 경우 (|(objectClass=organizationalUnit)(objectClass=container))가 일반적으로 사용됩니다.  다른 LDAP 디렉터리에 대 한 필터 조건에 각 유형의 hello 디렉터리 스키마에 따라 컨테이너 개체를 사용 합니다.  <br>참고: 비워 둔 경우 ((objectClass=organizationalUnit)(objectClass=container))가 기본적으로 사용됩니다.
* **보안 그룹 필터** -디렉터리 검색을 수행할 때 hello 필터 기준을 사용 tooqualify 보안 그룹 레코드를 지정 합니다.  Active Directory 및 ADAM의 경우 (&(objectCategory=group) (groupType:1.2.840.113556.1.4.804:=-2147483648))이 일반적으로 사용됩니다.  다른 LDAP 디렉터리에 대 한 필터 조건에 각 유형의 hello 디렉터리 스키마에 따라 보안 그룹 개체를 사용 합니다.  <br>참고: 비워 둔 경우 (&(objectCategory=group) (groupType:1.2.840.113556.1.4.804:=-2147483648))이 기본적으로 사용됩니다.
* **사용자 필터** -디렉터리 검색을 수행할 때 hello 필터 기준을 사용 tooqualify 사용자 레코드를 지정 합니다.  Active Directory 및 ADAM의 경우 (& (objectClass=user)(objectCategory=person))이 일반적으로 사용됩니다.  다른 LDAP 디렉터리에 대 한 사용 (objectClass = inetOrgPerson) 또는 이와 유사한 hello 디렉터리 스키마에 따라 합니다. <br>참고: 비워 둔 경우 (&(objectCategory=person)(objectClass=user))가 기본적으로 사용됩니다.

## <a name="attributes"></a>특성
필요에 따라 특성을 특정 디렉터리에 사용자 지정할 수 있습니다.  이 사용자 지정 특성 tooadd 있으며 hello 동기화 tooonly hello 필요한 특성을 미세 조정 합니다. 각 특성 필드의 값이 hello hello 디렉터리 스키마에 정의 된 hello attricute의 hello 이름을 사용 합니다. hello 다음 표에서 각 기능에 대 한 추가 정보.

특성 수동으로 입력할 수 및 필요한 toomatch hello 특성 목록의 특성과 하지 않습니다.

![특성](./media/multi-factor-authentication-get-started-server-dirint/dirint3.png)

| 기능 | 설명 |
| --- | --- |
| 고유 식별자 |Hello 컨테이너, 보안 그룹 및 사용자 레코드의 고유 식별자로 사용할 hello 특성의 hello 특성 이름을 입력 합니다.  Active Directory에서는 일반적으로 objectGUID입니다. 다른 LDAP 구현은 entryUUID 또는 이와 유사한 이름을 사용할 수 있습니다.  hello 기본값은 objectGUID입니다. |
| 고유 식별자 형식 |Hello hello 고유 식별자 특성 유형을 선택 합니다.  Active Directory에서 hello objectGUID 특성이 GUID 형식입니다. 다른 LDAP 구현은 ASCII 바이트 배열 또는 문자열 형식을 사용할 수 있습니다.  hello 기본값은 GUID입니다. <br><br>것이 중요 한 tooset 올바르게 동기화 항목 때문에이 형식 고유 식별자로 참조 됩니다. 고유 식별자 형식을 hello는 hello 디렉터리에 사용 되는 toodirectly 찾기 hello 개체입니다.  실제로 hello 디렉터리 ASCII 문자의 바이트 배열로 hello 값을 저장 하는 경우이 형식 tooString를 설정 동기화를가 제대로 작동 되지 않습니다. |
| 고유 이름 |각 레코드에 대 한 hello 고유 이름이 포함 된 hello 특성의 hello 특성 이름을 입력 합니다.  Active Directory에서는 일반적으로 distinguishedName입니다. 다른 LDAP 구현은 entryDN 또는 이와 유사한 이름을 사용할 수 있습니다.  hello 기본값은 distinguishedName입니다. <br><br>Hello 고유 이름만 포함 하는 특성이 없으면 adspath 특성 hello를 사용할 수 있습니다.  hello "LDAP: / /\<서버\>/" 부분은 hello 경로 자동으로 제거 되어, hello 고유 이름만 남게 hello 개체의 합니다. |
| 컨테이너 이름 |컨테이너 레코드에 hello 이름이 포함 된 hello 특성의 hello 특성 이름을 입력 합니다.  Active Directory에서 가져올 때이 특성의 hello 값 hello 컨테이너 계층 구조에에서 표시 됩니다 또는 동기화 항목 추가 합니다.  hello 기본값은 name입니다. <br><br>여러 컨테이너가 이름에 대 한 서로 다른 특성에 사용 하는 경우 여러 컨테이너 이름 특성 세미콜론 tooseparate 사용 합니다.  컨테이너 개체에 hello 첫 번째 컨테이너 이름 특성을 찾을 toodisplay 사용 되는 이름입니다. |
| 보안 그룹 이름 |보안 그룹 레코드에 hello 이름이 포함 된 hello 특성의 hello 특성 이름을 입력 합니다.  Active Directory에서 가져올 때이 특성의 hello 값 hello 보안 그룹 목록에 표시 됩니다 또는 동기화 항목 추가 합니다.  hello 기본값은 name입니다. |
| 사용자 이름 |사용자 레코드에 hello 사용자 이름이 포함 된 hello 특성의 hello 특성 이름을 입력 합니다.  이 특성의 hello 값 hello Multi-factor Auth 서버 사용자 이름으로 사용 됩니다.  두 번째 특성으로 백업 toohello 먼저 지정할 수 있습니다.  hello 두 번째 특성은 첫 번째 특성 hello hello 사용자에 대 한 값이 포함 되지 않는 경우에 사용 됩니다.  hello 기본값은 userPrincipalName 및 sAMAccountName입니다. |
| 이름 |사용자 레코드에 hello 이름이 포함 된 hello 특성의 hello 특성 이름을 입력 합니다.  hello 기본값은 givenName입니다. |
| 성 |Hello 사용자 레코드에 성이 포함 된 hello 특성의 hello 특성 이름을 입력 합니다.  hello 기본값은 sn입니다. |
| 메일 주소 |사용자 레코드에 hello 전자 메일 주소를 포함 하는 hello 특성의 hello 특성 이름을 입력 합니다.  전자 메일 주소를 사용 하는 toosend 시작 및 update toohello 사용자 전자 메일입니다.  hello 기본값은 mail입니다. |
| 사용자 그룹 |사용자 레코드에 hello 사용자 그룹이 포함 된 hello 특성의 hello 특성 이름을 입력 합니다.  사용자 그룹에는 hello Multi-factor Auth 서버 관리 포털에서에서 보고서와 hello 에이전트에서 사용 되는 toofilter 사용자 수 있습니다. |
| 설명 |사용자 레코드에 대 한 hello 설명을 포함 하는 hello 특성의 hello 특성 이름을 입력 합니다.  설명은 검색을 위해서만 사용됩니다.  hello 기본값은 description입니다. |
| 전화 통화 언어 |Hello 사용자에 대 한 음성 통화에 대 한 hello 언어 toouse의 hello 짧은 이름이 포함 된 hello 특성의 hello 특성 이름을 입력 합니다. |
| 문자 메시지 언어 |Hello 사용자에 대 한 SMS 문자 메시지에 대 한 hello 언어 toouse의 hello 짧은 이름이 포함 된 hello 특성의 hello 특성 이름을 입력 합니다. |
| 모바일 앱 언어 |Hello 사용자에 대 한 휴대폰 앱 문자 메시지에 대 한 hello 언어 toouse의 hello 짧은 이름이 포함 된 hello 특성의 hello 특성 이름을 입력 합니다. |
| OATH 토큰 언어 |Hello 사용자에 대 한 OATH 토큰 문자 메시지에 대 한 hello 언어 toouse의 hello 짧은 이름이 포함 된 hello 특성의 hello 특성 이름을 입력 합니다. |
| 회사 전화 |사용자 레코드에 hello 회사 전화 번호가 포함 된 hello 특성의 hello 특성 이름을 입력 합니다.  hello 기본값은 telephoneNumber입니다. |
| 집 전화 |사용자 레코드에 집 전화 번호가 hello 포함 된 hello 특성의 hello 특성 이름을 입력 합니다.  hello 기본값은 homePhone입니다. |
| 호출기 |사용자 레코드에 호출기 번호가 hello 포함 된 hello 특성의 hello 특성 이름을 입력 합니다.  hello 기본값은 pager입니다. |
| 휴대폰 |사용자 레코드에 hello 휴대 전화 번호를 포함 하는 hello 특성의 hello 특성 이름을 입력 합니다.  hello 기본값은 mobile입니다. |
| 팩스 |사용자 레코드에 hello 팩스 번호가 포함 된 hello 특성의 hello 특성 이름을 입력 합니다.  hello 기본값은 facsimileTelephoneNumber입니다. |
| IP 전화 |사용자 레코드에 hello IP 전화 번호가 포함 된 hello 특성의 hello 특성 이름을 입력 합니다.  hello 기본값은 ipphone입니다. |
| 사용자 지정 |사용자 레코드에 사용자 지정 전화 번호가 포함 된 hello 특성의 hello 특성 이름을 입력 합니다.  hello 기본값은 blank입니다. |
| 내선 번호 |Hello 전화 번호 내선 번호가 사용자 레코드에 포함 된 hello 특성의 hello 특성 이름을 입력 합니다.  hello 확장 필드의 hello 값 hello 확장 toohello 기본 전화 번호로으로 사용 됩니다.  hello 기본값은 blank입니다. <br><br>Hello 확장 특성을 지정 하지 않으면 확장 hello 전화 특성의 일부로 포함할 수 있습니다. 이 경우에 'x'를 hello 확장명을 앞에 가져옵니다 올바르게 구문 분석할 수 있도록 합니다.  예를 들어 555-123-4567 x890 hello 전화 번호로 555-123-4567 되 고 890 hello 확장 초래 합니다. |
| 기본값 복원 단추 |클릭 **기본값 복원** tooreturn 모든 특성 tootheir 기본값을 백업 합니다.  hello 기본값 hello 일반 Active Directory 또는 ADAM 스키마에서 제대로 작동 해야 합니다. |

tooedit 특성 클릭 **편집** hello 특성 탭 합니다.  이 hello 특성을 편집할 수 있는 창이 나타납니다. 선택 hello **...**  다음 tooany 특성 tooopen 어떤 특성 toodisplay를 선택할 수 있는 창입니다.

![특성 편집](./media/multi-factor-authentication-get-started-server-dirint/dirint4.png)

## <a name="synchronization"></a>동기화
동기화는 Active Directory 또는 다른 LDAP Lightweight Directory Access Protocol () 디렉터리에 hello 사용자와 동기화 하는 hello Azure MFA 사용자 데이터베이스를 유지 합니다. hello 프로세스는 Active Directory에서 수동으로 비슷한 tooimporting 사용자 하지만 Active Directory 사용자를 주기적으로 폴링한다 및 보안 그룹 tooprocess 변경 합니다.  또한 컨테이너, 보안 그룹 또는 Active Directory에서 제거된 사용자를 비활성화하거나 제거합니다.

hello Multi-factor Auth ADSync 서비스는 hello Active Directory의 폴링 주기를 수행 하는 Windows 서비스입니다.  Azure AD Sync 또는 Azure AD Connect와 혼동된 toobe 아닙니다.  hello Multi-factor Auth ADSync는 비슷한 코드 베이스에서 작성 하는 있지만 특정 toohello Azure Multi-factor Authentication 서버입니다.  중지 됨 상태에 설치 하 고 hello Multi-factor Auth 서버 서비스 구성에 의해 시작 toorun 합니다.  다중 서버 Multi-factor Auth 서버 구성이 있는 경우 hello Multi-factor Auth ADSync는 단일 서버에서 실행할 수만 있습니다.

hello Multi-factor Auth ADSync 서비스는 hello 변경에 대 한 Microsoft tooefficiently 설문 조사에서 제공 하는 DirSync LDAP 서버 확장을 사용 합니다.  이 DirSync 컨트롤 호출자 hello "디렉터리는 변경 내용 가져오기" 오른쪽 및 DS-복제-Get-changes 확장된 컨트롤 액세스 권한이 있어야 합니다.  기본적으로 이러한 권한은 도메인 컨트롤러에서 toohello 관리자 및 LocalSystem 계정 할당 됩니다.  hello Multi-factor Auth AdSync 서비스는 기본적으로 LocalSystem으로 구성 된 toorun.  그러므로 도메인 컨트롤러의 가장 간단한 toorun hello 서비스입니다.  구성 하는 경우 전체 동기화를 수행 하는 hello 서비스 tooalways, 권한이 낮은 계정으로 실행할 수 있습니다.  효율성이 떨어지기는 하지만 더 적은 계정 권한만 있어도 됩니다.

Hello LDAP 디렉터리에 지원 하며 경우에 대해 디렉터리 동기화 구성 다음 폴링 사용자 및 보안 그룹 변경 내용을 작동할지에 대 한 hello 동일한 Active Directory에서와 마찬가지로 합니다.  Hello LDAP 디렉터리가 DirSync 컨트롤 hello를 지원 하지 않는 경우에 각 주기 중 전체 동기화가 수행 됩니다.

![동기화](./media/multi-factor-authentication-get-started-server-dirint/dirint5.png)

hello 다음 표에서 각 hello 동기화 탭 설정에 대 한 추가 정보.

| 기능 | 설명 |
| --- | --- |
| Active Directory와 동기화 사용 |옵션을 선택 하면 hello Multi-factor Auth 서버 서비스 변경에 대 한 Active Directory를 정기적으로 폴링합니다. <br><br>참고: 동기화 항목을 하나 이상 추가 해야 하 고 지금 동기화 hello Multi-factor Auth 서버 서비스는 변경 내용 처리를 시작 하기 전에 수행 되어야 합니다. |
| 동기화 간격 |Hello 시간 간격 hello Multi-factor Auth 서버 서비스는 폴링 및 변경 내용 처리 간에 대기를 지정 합니다. <br><br> 참고: hello 지정 된 간격은 각 주기 시작 hello 사이의 hello 시간입니다.  Hello 간격을 초과 하는 hello 시간 처리 변경 내용, hello 서비스가 즉시 폴링을 다시 수행 합니다. |
| Active Directory에 더 이상 존재하지 않는 사용자 제거 |이 옵션을 선택 하는 경우 hello Multi-factor Auth 서버 서비스는 Active Directory의 삭제 된 사용자 삭제 표식을 처리 하 고 제거 hello 관련 Multi-factor Auth 서버 사용자입니다. |
| 항상 전체 동기화 실행 |옵션을 선택 하면 hello Multi-factor Auth 서버 서비스가 항상 전체 동기화를 수행 합니다.  옵션을 선택 취소 hello Multi-factor Auth 서버 서비스가 변경 된 사용자만 쿼리하여 증분 동기화를 수행 합니다.  hello 기본적으로 선택 취소 합니다. <br><br>옵션을 선택 취소 하는 경우 Azure MFA 서버 hello 디렉터리 hello DirSync 컨트롤을 지원 하 고 hello 계정 바인딩 toohello 디렉터리에 사용 권한을 tooperform DirSync 증분 쿼리를 포함 하는 경우에 증분 동기화를 수행 합니다.  Hello 동기화에 여러 도메인이 관련 된 hello 계정 hello 적절 한 권한이 없을 경우 Azure MFA 서버 전체 동기화를 수행 합니다. |
| 사용하지 않도록 설정하거나 제거할 사용자가 X명을 초과하는 경우 관리자 승인이 필요합니다. |동기화 항목은 더 이상 hello 항목의 컨테이너 또는 보안 그룹의 구성원 인 사용자를 제거 또는 구성 된 toodisable 수 없습니다.  안전 조치로, 사용자 toodisable / 제거를 hello 수가 임계값을 초과 하는 경우 관리자 승인이 필요할 수 있습니다.  선택하면 지정된 임계값에 대해 승인이 필요합니다.  hello 기본값은 5이 고 hello 범위는 1 too999 합니다. <br><br> 승인 첫 번째 전자 메일 알림 tooadministrators 전송 하 여 촉진 됩니다. hello 전자 메일 알림을 검토 하 고 사용자 제거 및 hello 비활성화 승인에 대 한 지침을 제공 합니다.  Hello Multi-factor Auth 서버 사용자 인터페이스를 시작 하는 경우 승인을 위해 묻습니다. |

hello **지금 동기화** 단추 있습니다 toorun hello 동기화에 대 한 전체 동기화가 지정 된 항목입니다.  동기화 항목이 추가, 수정, 제거 또는 그 순서가 변경할 때마다 전체 동기화가 필요합니다.  이기도 하기 전에 필요한 hello Multi-factor Auth AdSync 서비스는 hello 증분 변경 내용에 대 한 hello 서비스를 폴링하는 시작점이 설정 하므로 작동 합니다.  변경 사항이 toosynchronization 항목 표시 되지만 전체 동기화를 수행 하지 않았습니다 됩니다 증명된 tooSynchronize 이제 합니다.

hello **제거** 단추를 사용 하면 hello 관리자 toodelete hello Multi-factor Auth 서버 동기화 항목 목록에서 하나 이상의 동기화 항목입니다.

> [!WARNING]
> 동기화 항목 레코드가 제거된 후에는 복구할 수 없습니다. 해야 tooadd hello 동기화 항목 레코드 다시 실수로 삭제 한 경우.

hello 동기화 항목 또는 동기화 항목이 Multi-factor Auth 서버에서 제거 되었습니다.  hello Multi-factor Auth 서버 서비스에서 더 이상 hello 동기화 항목을 처리 합니다.

hello 위로 이동 및 아래로 이동 단추 관리자에 게 hello 동기화 항목의 toochange hello 순서를 사용 합니다.  hello 순서는 중요 hello 동일한 사용자 일 수 있으므로 여러 개의 동기화 항목 (예: 컨테이너 및 보안 그룹)의 구성원.  연결 된 hello 설정을 동기화 하는 동안 적용 된 toohello 사용자 hello hello 목록 toowhich hello 사용자 첫 번째 동기화 항목에서 옵니다.  따라서 hello 동기화 항목 우선 순위에 따라 넣어야 합니다.

> [!TIP]
> 동기화 항목을 제거한 후에는 전체 동기화를 실행해야 합니다.  동기화 항목의 순서를 지정한 후에는 전체 동기화를 실행해야 합니다.  클릭 **지금 동기화** tooperform 전체 동기화 합니다.

## <a name="multi-factor-auth-servers"></a>Multi-Factor Auth 서버
백업 RADIUS 프록시나 LDAP 프록시로 또는 IIS 인증을 위해 추가 Multi-factor Auth 서버 tooserve를 설정할 수 있습니다. hello 동기화 구성은 모든 hello 에이전트 간에 공유 됩니다. 그러나 이러한 에이전트 중 하나에만 hello Multi-factor Auth 서버 서비스가 실행 되 고 있을 수 있습니다. 이 탭에서는 tooselect hello를 Multi-factor Auth 서버 동기화를 설정 해야 하는 있습니다.

![Multi-Factor-Auth 서버](./media/multi-factor-authentication-get-started-server-dirint/dirint6.png)

---
title: "aaaConnector 버전 릴리스 기록 | Microsoft Docs"
description: "이 항목에서는 Forefront Identity Manager (FIM) 및 MIM Microsoft Identity Manager ()에 대 한 모든 버전의 hello 커넥터를 보여 줍니다."
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 3522f17c30e46542eaa367ecdefdfd2fc47f71a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connector-version-release-history"></a>커넥터 버전 릴리스 내역
Forefront Identity Manager (FIM) 및 MIM Microsoft Identity Manager ()에 대 한 hello 커넥터 지속적으로 업데이트 됩니다.

> [!NOTE]
> 이 항목은 FIM 및 MIM에만 있습니다. 이러한 커넥터는 Azure AD Connect에서 설치하도록 지원되지 않습니다. 출시 된 커넥터 toospecified 빌드를 업그레이드 하는 경우 AADConnect에 미리 설치 됩니다.

이 항목의 hello 출시 된 커넥터의 모든 버전을 나열 합니다.

관련 링크:

* [최신 커넥터 다운로드](http://go.microsoft.com/fwlink/?LinkId=717495)
* [일반 LDAP 커넥터](active-directory-aadconnectsync-connector-genericldap.md) 참조 설명서
* [일반 SQL 커넥터](active-directory-aadconnectsync-connector-genericsql.md) 참조 설명서
* [웹 서비스 커넥터](http://go.microsoft.com/fwlink/?LinkID=226245) 참조 설명서
* [PowerShell 커넥터](active-directory-aadconnectsync-connector-powershell.md) 참조 설명서
* [Lotus Domino 커넥터](active-directory-aadconnectsync-connector-domino.md) 참조 설명서


## <a name="116040-aadconnect-pending-release"></a>1.1.604.0(AADConnect 보류 중 릴리스)


### <a name="fixed-issues"></a>수정된 문제:

* 일반 웹 서비스:
  * 두 개 이상의 끝점이 있을 때 SOAP 프로젝트가 만들어지지 않도록 방지하는 문제를 해결했습니다.
* 일반 SQL:
  * Hello 가져오기 작업에서 hello GSQL가 변환 되지 않으면 시간 올바르게 저장 될 때 tooconnector 공간입니다. hello hello GSQL의 커넥터 공간에 대 한 기본 날짜 및 시간 형식에서에서 변경 되었습니다. 'yyyy-월-일 hh:mm:ssZ' too'yyyy-월-일 HH:mm:ssZ'.

## <a name="115510-aadconnect-115530"></a>1.1.551.0(AADConnect 1.1.553.0)

### <a name="fixed-issues"></a>수정된 문제:

* 일반 웹 서비스:
  * hello Wsconfig 도구 않았습니다 hello REST 서비스 메서드에 대 한 "예제 요청"에서 Json 배열 hello를 올바르게 변환 하지 않습니다. 이 문제가 발생 하 serialization hello REST 요청에 대 한이 Json 배열입니다.
  * 웹 서비스 커넥터 구성 도구는 JSON 속성 이름에 공백 기호를 사용하는 것을 지원하지 않습니다. 
    * 대체 패턴을 수동으로 추가할 수 있습니다 toohello WSConfigTool.exe.config 파일 예:```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```

* Lotus Notes:
  * 경우 옵션을 hello **조직/조직 구성 단위에 대 한 사용자 지정 certifiers 허용** hello 커넥터 없음 내보내는 hello 내보내기는 모든 특성 흐름이 후 (업데이트) 중 내보낸된 tooDomino 권한은 있지만 hello 시점에 사용할 수 없습니다 내보내기는 KeyNotFoundException tooSync 반환 됩니다. 
    * 이 다음 hello 특성 중 하나를 변경 하 여 hello toochange DN (사용자 이름 특성)를 읽으려고 할 때 작업이 실패 하면 이름 바꾸기 때문에 발생 합니다.  
      - LastName
      - FirstName
      - MiddleInitial
      - AltFullName
      - AltFullNameLanguage
      - ou
      - altcommonname

  * **조직/조직 구성 단위에 대한 사용자 지정 인증자 허용** 옵션이 설정되었지만 필수 인증자가 여전히 비어 있으면 KeyNotFoundException이 발생합니다.

### <a name="enhancements"></a>향상된 기능:

* 일반 SQL:
  * **시나리오: 다시 설계되고 구현됨:** "*" 기능
  * **솔루션 설명:** [다중 값 참조 특성 처리](active-directory-aadconnectsync-connector-genericsql.md) 접근 방식이 변경되었습니다.


### <a name="fixed-issues"></a>수정된 문제:

* 일반 웹 서비스:
  * 웹 서비스 커넥터가 있는 데도 서버 구성을 가져올 수 없습니다.
  * 웹 서비스 커넥터는 여러 웹 서비스에 작동하지 않습니다.

* 일반 SQL:
  * 단일 값 참조 특성에 대해 나열되는 개체 형식이 없습니다.
  * 변경 추적 전략에 대한 델타 가져오기는 다중 값 테이블에서 값이 제거될 때 개체를 삭제합니다.
  * AS/400의 DB2에서 GSQL 커넥터의 OverflowException

Lotus:
  * 추가 옵션 tooenable\disable Ou GlobalParameters 페이지 열기 전에 검색

## <a name="114430"></a>1.1.443.0

출시 날짜: 2017년 3월

### <a name="enhancements"></a>향상된 기능

* 일반 SQL:</br>
  **시나리오 증상:** 는 잘 알려진 제한 사항으로 hello SQL 커넥터 여기서 म만 참조 tooone 개체 유형을 허용 하 고 멤버와 교차 참조 해야 합니다. </br>
  **솔루션 설명:** 된 참조에 대 한 hello 처리 단계에서 "*" 옵션이 선택 된 경우 백 toohello 동기화 엔진 개체 유형의 모든 조합을 반환 됩니다.

>[!Important]
- 그러면 자리 표시자가 많이 생성됩니다.
- 것이 필수 toomake hello 명명 고유한 지 개체 유형을 교차 합니다.


* 일반 LDAP:</br>
 **시나리오:** 몇 컨테이너만 특정 파티션에 선택 되 면 다음 hello 검색 여전히에서 수행 됩니다 전체 파티션 합니다. 특정 파티션은 성능 저하로 이어질 수 있는 MA가 아닌 Synchronization Service에서 필터링됩니다. </br>

 **솔루션 설명:** 변경 GLDAP 커넥터의 코드 toomake 수 모든 컨테이너를 모두 이동해 고 hello 전체 파티션에서 검색 하는 대신 각 개체를 검색 합니다.


* Lotus Domino:

  **시나리오:** 내보내기를 수행하는 동안 사용자 제거를 위한 Domino 메일 삭제 지원입니다. </br>
  **해결 방법:** 내보내기를 수행하는 동안 사용자 제거를 위한 구성 가능한 메일 삭제 지원입니다.

### <a name="fixed-issues"></a>수정된 문제:
* 일반 웹 서비스:
 * Hello 다음 오류가 발생 한 후 웹 서비스 구성 도구를 통해 SAP wsconfig 프로젝트 기본 hello 서비스 URL을 변경 하는 경우: hello 경로의 일부를 찾을 수 없습니다

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* 일반 LDAP:
 * GLDAP 커넥터에서 AD LDS의 모든 특성을 확인할 수 없음
 * 마법사 나누기 hello LDAP 디렉터리 스키마에서 검색 되는 UPN 특성이 없는 경우
 * "objectclass" 특성이 선택되지 않은 경우 전체 가져오기를 수행하는 동안 검색 오류가 발생하지 않으면 델타 가져오기 실패
 * "파티션 및 계층 구성" 구성 페이지에서 모든 개체는 같은 toohello 파티션 Novel 서버 hello 제네릭에에서 대 한 유형을 표시 되지 않습니다.  
LDAP MA의 Novel 서버에 대한 파티션과 형식이 비슷한 개체가 표시되지 않습니다. RootDSE 파티션의 개체만 표시됩니다.


* 일반 SQL:
 * 일반 SQL 워터마크 델타 가져오기 다중값 특성이 버그를 가져오지 않는 문제 해결
 * 다중값 특성의 삭제/추가된 값을 내보낼 때 데이터 원본에서 삭제/추가되지 않음.  


* Lotus Notes:
 * 그러나 특정 필드 "전체" 상응 이름은 hello 메타 버스 올바르게 때 내보내기 tooNotes hello에 대 한 값 hello 특성은 Null 이거나 비어 있습니다.
 * 중복 인증자 오류 해결
 * 다른 개체와 hello Lotus Domino 커넥터에서 데이터 없이도 hello 개체를 선택한 경우 다음 म 오류가 hello 검색 전체 가져오기를 수행 하는 동안 합니다.
 * 델타 가져오기는 되 고 서비스를 실행 hello Lotus Domino 커넥터에서 해당 실행된을 hello hello 끝나기 전에 Microsoft.IdentityManagement.MA.LotusDomino.Service.exe 경우에 따라 응용 프로그램 오류를 반환 합니다.
 * 전체 그룹 멤버 자격에서 제대로 작동 하 고 hello 내보내기 tootry tooremove 사용자를 실행 하는 경우 멤버 자격에서 업데이트를 성공으로 표시 되지만 hello 사용자 Lotus Notes의 멤버 자격에서 실제로 제거 하지 않는 점을 제외 하 고 유지 관리 됩니다.
 * "추가 항목 맨 아래에"으로 내보내기의 기회 toochoose 모드는에서 추가 되었습니다 구성 Lotus GUI MA tooappend 새 항목 맨 아래에 다중 값된 특성에 대 한 hello 내보내기 중.
 * 커넥터는 hello 필요한 hello 메일 폴더에서에서 논리 toodelete hello 파일 및 ID 자격 증명 모음을 추가 합니다.
 * 멤버 자격 삭제는 NAB 멤버 간에 작동하지 않습니다.
 * 값은 다중값 특성에서 성공적으로 삭제되어야 합니다.

## <a name="111170"></a>1.1.117.0
출시 날짜: 2016년 3월

**일반 SQL 커넥터**  
초기 버전의 hello [제네릭 SQL 커넥터](active-directory-aadconnectsync-connector-genericsql.md)합니다.

**새로운 기능:**

* 일반 LDAP 커넥터:
  * Isode에서 델타 가져오기에 대한 지원을 추가했습니다.
* 웹 서비스 커넥터:
  * 업데이트 된 hello csEntryChangeResult 활동과 setImportErrorCode 활동 tooallow 개체 수준 오류 toobe 반환 된 뒤로 toohello 동기화 엔진입니다.
  * 업데이트 된 hello SAP6 및 SAP6User 템플릿 toouse hello 새 개체 수준의 오류 기능입니다.
* Lotus Domino 커넥터:
  * 내보내는 경우 주소록당 하나의 인증자가 있어야 합니다. 사용 하 여 hello 동일 이제 수 모든 certifiers hello 관리 toomake 템플릿 쉽게에 대 한 암호입니다.

**수정된 문제:**

* 일반 LDAP 커넥터:
  * IBM Tivoli DS의 경우 일부 참조 특성이 제대로 검색되지 않았습니다.
  * 델타 가져오기 중 Open LDAP에 대 한 문자열의 hello 시작 및 끝에 있는 공백은 잘리지 않았습니다.
  * Novell 및 NetIQ에 대 한 hello 및 Ou/컨테이너 간에 개체를 이동 하는 내보내기 시간이 이름이 바뀐된 hello 개체 실패 합니다.
* 웹 서비스 커넥터:
  * Hello 웹 서비스에 여러 개의 끝점이 모두 동일한 바인딩에 대 한이 있으면 다음 hello 커넥터 않았습니다 올바르게 검색 하지 이러한 끝점.
* Lotus Domino 커넥터:
  * 데이터베이스 메일에서 hello fullName 특성 tooa의 내보내기를 작동 하지 않습니다.
  * 그룹에서 추가 및 제거 멤버만 hello를 내보낼 내보내기 구성원을 추가 합니다.
  * 정보 문서에 유효 하지 않을 경우 (특성 isValid hello toofalse 설정), 다음 커넥터 없음 hello 합니다.

## <a name="older-releases"></a>이전 릴리스
2016 년 3 월 하기 전에 hello 커넥터 지원 항목으로 릴리스 되었습니다.

**일반 LDAP**

* [KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015년 9월
* [KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015년 3월
* [KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015년 1월
* [KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014년 9월
* [KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014년 3월

**WebServices**

* [KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014년 9월

**PowerShell**

* [KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014년 9월

**Lotus Domino**

* [KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015년 9월
* [KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015년 3월
* [KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014년 8월
* [KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014년 2월  
* [KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013년 10월
* [KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013년 8월

## <a name="next-steps"></a>다음 단계
Hello에 대 한 자세한 [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성 합니다.

[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.

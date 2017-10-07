---
title: "Azure AD 동기화 연결: 함수 참조 | Microsoft Docs"
description: "Azure AD Connect 동기화의 선언적 프로비전 식을 참조하세요."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a>Azure AD 동기화 연결: 함수 참조
Azure AD Connect의 기능은 동기화 하는 동안 사용 되는 toomanipulate 특성 값에 연결 합니다.  
hello hello 함수의 구문 형식에 따라 hello를 사용 하 여 표현 됩니다.  
`<output type> FunctionName(<input type> <position name>, ..)`

함수가 과부하되거나 여러 구문을 허용한 경우, 모든 사용한 구문의 목록이 나타납니다.  
hello 함수는 강력한 형식이 지정 하 고 일치 하는 항목 hello 설명 형식에 전달 된 hello 형식 확인 합니다.  
Hello 형식이 일치 하지 않는 경우 오류가 throw 됩니다.

hello 형식이 구문 다음 hello로 표현 됩니다.

* **bin** -이진
* **bool** -부울
* **dt** – UTC 날짜/시간
* **enum** – 알려진 상수의 열거형
* **exp** – 식을 tooevaluate tooa 부울 필요 합니다.
* **mvbin** – 다중값의 이진
* **mvstr** – 다중 값 문자열
* **mvref** – 다중 값 참조
* **num** – 숫자
* **ref** – 참조
* **str** - 문자열
* **var** – 거의 모든 다른 형식의 변수
* **void** – 값을 반환하지 않습니다.

hello 형식과 함수 hello **mvbin**, **mvstr**, 및 **mvref** 다중 값된 특성에서 작동할 수 있습니다. **bin**, **str** 및 **ref**를 포함한 함수는 단일값 및 다중값 특성에서 작동합니다.

## <a name="functions-reference"></a>함수 참조
| 함수 목록 |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| **인증서** | | | | |
| [CertExtensionOids](#certextensionoids) |[CertFormat](#certformat) |[CertFriendlyName](#certfriendlyname) |[CertHashString](#certhashstring) | |
| [CertIssuer](#certissuer) |[CertIssuerDN](#certissuerdn) |[CertIssuerOid](#certissueroid) |[CertKeyAlgorithm](#certkeyalgorithm) | |
| [CertKeyAlgorithmParams](#certkeyalgorithmparams) |[CertNameInfo](#certnameinfo) |[CertNotAfter](#certnotafter) |[CertNotBefore](#certnotbefore) | |
| [CertPublicKeyOid](#certpublickeyoid) |[CertPublicKeyParametersOid](#certpublickeyparametersoid) |[CertSerialNumber](#certserialnumber) |[CertSignatureAlgorithmOid](#certsignaturealgorithmoid) | |
| [CertSubject](#certsubject) |[CertSubjectNameDN](#certsubjectnamedn) |[CertSubjectNameOid](#certsubjectnameoid) |[CertThumbprint](#certthumbprint) | |
[CertVersion](#certversion) |[IsCert](#iscert) | | | |
| **변환** | | | | |
| [CBool](#cbool) |[CDate](#cdate) |[CGuid](#cguid) |[ConvertFromBase64](#convertfrombase64) | |
| [ConvertToBase64](#converttobase64) |[ConvertFromUTF8Hex](#convertfromutf8hex) |[ConvertToUTF8Hex](#converttoutf8hex) |[CNum](#cnum) | |
| [CRef](#cref) |[CStr](#cstr) |[StringFromGuid](#StringFromGuid) |[StringFromSid](#stringfromsid) | |
| **Date / Time** | | | | |
| [DateAdd](#dateadd) |[DateFromNum](#datefromnum) |[FormatDateTime](#formatdatetime) |[Now](#now) | |
| [NumFromDate](#numfromdate) | | | | |
| **디렉터리** | | | | |
| [DNComponent](#dncomponent) |[DNComponentRev](#dncomponentrev) |[EscapeDNComponent](#escapedncomponent) | | |
| **평가** | | | | |
| [IsBitSet](#isbitset) |[IsDate](#isdate) |[IsEmpty](#isempty) |[IsGuid](#isguid) | |
| [IsNull](#isnull) |[IsNullOrEmpty](#isnullorempty) |[IsNumeric](#isnumeric) |[IsPresent](#ispresent) | |
| [IsString](#isstring) | | | | |
| **Math** | | | | |
| [BitAnd](#bitand) |[BitOr](#bitor) |[RandomNum](#randomnum) | | |
| **다중값** | | | | |
| [포함](#contains) |[개수](#count) |[항목](#item) |[ItemOrNull](#itemornull) | |
| [Join](#join) |[RemoveDuplicates](#removeduplicates) |[분할](#split) | | |
| **Program Flow** | | | | |
| [오류](#error) |[IIF](#iif) |[선택](#select) |[Switch](#switch) | |
| [Where](#where) |[With](#with) | | | |
| **Text** | | | | |
| [GUID](#guid) |[InStr](#instr) |[InStrRev](#instrrev) |[LCase](#lcase) | |
| [Left](#left) |[Len](#len) |[LTrim.](#ltrim) |[Mid](#mid) | |
| [padLeft](#padleft) |[PadRight](#padright) |[PCase](#pcase) |[Replace](#replace) | |
| [ReplaceChars](#replacechars) |[Right](#right) |[RTrim](#rtrim) |[Trim](#trim) | |
| [UCase](#ucase) |[Word](#word) | | | |

- - -
### <a name="bitand"></a>BitAnd
**설명:**  
hello BitAnd 함수는 값에 지정 된 비트를 설정 합니다.

**구문:**  
`num BitAnd(num value1, num value2)`

* value1, value2: 숫자 값은 AND와 함께 사용해야 합니다.

**설명**  
이 함수는 두 매개 변수 toohello 이진 표현을 변환 하 고 비트를 설정:

* 0-하나 또는 둘 다의 해당 비트 hello *마스크* 및 *플래그* 0
* 1-경우 hello 해당 비트가 모두 1입니다.

즉, 두 매개 변수의 해당 비트가 hello 1 경우를 제외 하 고 모든 경우에 0을 반환 합니다.

**예제:**  
`BitAnd(&HF, &HF7)`  
16 진수 "F"와 "F7" toothis 값을 계산 하기 때문에 7을 반환 합니다.

- - -
### <a name="bitor"></a>BitOr
**설명:**  
hello BitOr 함수는 값에 지정 된 비트를 설정 합니다.

**구문:**  
`num BitOr(num value1, num value2)`

* value1, value2: 숫자 값은 OR과 함께 사용해야 합니다.

**설명**  
이 함수는 두 매개 변수 toohello 이진 표현으로 변환 하며 하나 이상이 포인터인 경우 hello 마스크 및 플래그의 해당 비트의 1 세대 및 too0 hello 해당 비트의 둘 다 0 인 경우 비트 too1를 설정 합니다. 즉, 두 매개 변수의 해당 비트가 hello는 0을 제외한 모든 경우에 1을 반환 합니다.

- - -
### <a name="cbool"></a>CBool
**설명:**  
CBool 함수 hello hello 평가 식을 기반으로 하는 부울을 반환

**구문:**  
`bool CBool(exp Expression)`

**설명**  
Hello 식이 계산 되 면 tooa 0이 아닌 값을 다음 CBool 반환 True, 그렇지 않으면 False를 반환 합니다.

**예제:**  
`CBool([attrib1] = [attrib2])`  

True 이면 두 특성에는 반환 hello 동일한 값입니다.

- - -
### <a name="cdate"></a>CDate
**설명:**  
hello CDate 함수는 문자열에서 UTC 날짜 및 시간을 반환합니다. 날짜/시간은 동기화 내의 네이티브 특성 형식이 아니지만 일부 함수에서 사용됩니다.

**구문:**  
`dt CDate(str value)`

* 값: 날짜, 시간 및 임의적 시간대 문자열

**설명**  
hello 반환 문자열은 항상 utc에서입니다.

**예제:**  
`CDate([employeeStartTime])`  
Hello 직원의 시작 시간을 기반으로 날짜/시간을 반환 합니다.

`CDate("2013-01-10 4:00 PM -8")`  
"2013-01-11 12:00 AM"을 나타내는 날짜/시간을 반환합니다.








- - -
### <a name="certextensionoids"></a>CertExtensionOids
**설명:**  
반환 hello 인증서 개체의 모든 hello 중요 한 확장의 Oid 값입니다.

**구문:**  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certformat"></a>CertFormat
**설명:**  
반환 hello hello 형식이 X.509v3 인증서의 이름입니다.

**구문:**  
`str CertFormat(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certfriendlyname"></a>CertFriendlyName
**설명:**  
인증서에 대 한 별칭에 연결 하는 hello를 반환 합니다.

**구문:**  
`str CertFriendlyName(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certhashstring"></a>CertHashString
**설명:**  
Hello X.509v3 인증서에 대 한 SHA1 해시 값을 16 진 문자열로 hello 하는 반환 합니다.

**구문:**  
`str CertHashString(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certissuer"></a>CertIssuer
**설명:**  
반환 hello hello X.509v3 인증서를 발급 한 hello 인증 기관의 이름입니다.

**구문:**  
`str CertIssuer(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certissuerdn"></a>CertIssuerDN
**설명:**  
반환 hello hello 인증서 발급자의 고유 이름입니다.

**구문:**  
`str CertIssuerDN(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certissueroid"></a>CertIssuerOid
**설명:**  
반환 hello hello 인증서 발급자의 Oid 합니다.

**구문:**  
`str CertIssuerOid(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certkeyalgorithm"></a>CertKeyAlgorithm
**설명:**  
이 X.509v3 인증서에 대 한 문자열 hello 키 알고리즘 정보를 반환합니다.

**구문:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certkeyalgorithmparams"></a>CertKeyAlgorithmParams
**설명:**  
16 진 문자열 hello X.509v3 인증서에 대 한 hello 키 알고리즘 매개 변수를 반환합니다.

**구문:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certnameinfo"></a>CertNameInfo
**설명:**  
Hello 제목과 발급자 이름을 반환 인증서에서 합니다.

**구문:**  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.
*   X509NameType: hello hello 주체에 대 한 X509NameType 값입니다.
*   includesIssuerName: true tooinclude hello 발급자 이름입니다. 그렇지 않으면 false입니다.

- - -
### <a name="certnotafter"></a>CertNotAfter
**설명:**  
Hello 날짜 이후에 인증서가 더 이상 유효 현지 시간으로 반환 합니다.

**구문:**  
`dt CertNotAfter(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certnotbefore"></a>CertNotBefore
**설명:**  
인증서가 유효 하는 현지 시간으로 hello 날짜를 반환 합니다.

**구문:**  
`dt CertNotBefore(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certpublickeyoid"></a>CertPublicKeyOid
**설명:**  
반환 hello hello hello X.509v3 인증서에 대 한 공개 키의 Oid 합니다.

**구문:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certpublickeyparametersoid"></a>CertPublicKeyParametersOid
**설명:**  
반환 hello hello 공개 키 매개 변수 hello X.509v3 인증서에 대 한 Oid 합니다.

**구문:**  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certserialnumber"></a>CertSerialNumber
**설명:**  
Hello X.509v3 인증서의 hello 일련 번호를 반환합니다.

**구문:**  
`str CertSerialNumber(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certsignaturealgorithmoid"></a>CertSignatureAlgorithmOid
**설명:**  
반환 hello hello 알고리즘의 Oid는 인증서의 toocreate hello 서명을 사용 합니다.

**구문:**  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certsubject"></a>CertSubject
**설명:**  
가져옵니다 hello 인증서에서 주체 고유 이름입니다.

**구문:**  
`str CertSubject(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certsubjectnamedn"></a>CertSubjectNameDN
**설명:**  
반환 hello 인증서에서 주체 고유 이름입니다.

**구문:**  
`str CertSubjectNameDN(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certsubjectnameoid"></a>CertSubjectNameOid
**설명:**  
반환 hello Oid hello 인증서 주체 이름입니다.

**구문:**  
`str CertSubjectNameOid(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certthumbprint"></a>CertThumbprint
**설명:**  
인증서의 hello 지문을 반환 합니다.

**구문:**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="certversion"></a>CertVersion
**설명:**  
반환 되는 인증서의 X.509 형식 버전을 hello 합니다.

**구문:**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.

- - -
### <a name="cguid"></a>CGuid
**설명:**  
CGuid 함수 hello tooits 이진 표현 GUID의 hello 문자열 표현으로 변환합니다.

**구문:**  
`bin CGuid(str GUID)`

* 이 패턴에서 문자열 서식: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 또는 {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}

- - -
### <a name="contains"></a>포함
**설명:**  
hello Contains 함수는 다중값된 특성 안에서 문자열을 찾습니다.

**구문:**  
`num Contains (mvstring attribute, str search)` - 대/소문자 구분  
`num Contains (mvstring attribute, str search, enum Casetype)`  
`num Contains (mvref attribute, str search)` - 대/소문자 구분

* 특성: hello 다중값된 특성 toosearch 합니다.
* 검색: toofind hello 특성에는 문자열입니다.
* 대소문자 유형: 대소문자를 구분하거나 구분하지 않습니다.

Hello 문자열을 찾을 수 hello 다중값된 특성의 인덱스를 반환 합니다. hello 문자열을 찾을 수 없는 경우 0이 반환 됩니다.

**설명**  
다중값된 문자열 특성에 대 한 hello 검색 hello 값에서 부분 문자열을 찾습니다.  
참조 특성에 대 한 hello 검색된 되는 문자열 정확히 일치 해야 hello 값 toobe 일치로 간주 합니다.

**예제:**  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
Hello / / proxyAddresses 특성에 기본 전자 메일 주소가 있는 경우 (가리키는 대문자 "SMTP:"), 돌아 오세요 hello / / proxyAddress 특성, 그렇지 않으면 오류를 반환 합니다.

- - -
### <a name="convertfrombase64"></a>ConvertFromBase64
**설명:**  
hello ConvertFromBase64 함수 변환 hello는 base64 인코딩 값 tooa 일반 문자열을 지정 합니다.

**구문:**  
`str ConvertFromBase64(str source)` - 인코딩에 유니코드 가정  
`str ConvertFromBase64(str source, enum Encoding)`

* 원본: Base64 인코딩된 문자열  
* 인코딩: 유니코드, ASCII, UTF8

**예제**  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

두 예제 모두 "*Hello world!*"를 반환합니다.

- - -
### <a name="convertfromutf8hex"></a>ConvertFromUTF8Hex
**설명:**  
hello ConvertFromUTF8Hex 함수 변환 hello는 UTF8 16 진수 인코딩 값 tooa 문자열을 지정 합니다.

**구문:**  
`str ConvertFromUTF8Hex(str source)`

* 원본: UTF8 2-바이트 인코딩된 문자열

**설명**  
해당 hello 결과에서이 함수와 ConvertFromBase64([],UTF8) hello 차이점은 hello DN 특성에 대 한 친숙 한입니다.  
이 형식은 DN으로 Azure Active Directory에서 사용됩니다.

**예제:**  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
"*Hello world!*"를 반환합니다.

- - -
### <a name="converttobase64"></a>ConvertToBase64
**설명:**  
ConvertToBase64 함수 hello 문자열 tooa 유니코드 base64 문자열로 변환합니다.  
Hello 값 배열 base-64 숫자로 인코딩된 정수 tooits 문자열 표현으로 변환 합니다.

**구문:**  
`str ConvertToBase64(str source)`

**예제:**  
`ConvertToBase64("Hello world!")`  
"SABlAGwAbABvACAAdwBvAHIAbABkACEA"를 반환합니다.

- - -
### <a name="converttoutf8hex"></a>ConvertToUTF8Hex
**설명:**  
ConvertToUTF8Hex 함수 hello 문자열 tooa UTF8 16 진수 인코딩 값으로 변환합니다.

**구문:**  
`str ConvertToUTF8Hex(str source)`

**설명**  
이 함수의 hello 출력 형식은 DN 특성 형식으로 Azure Active Directory에서 사용 됩니다.

**예제:**  
`ConvertToUTF8Hex("Hello world!")`  
48656C6C6F20776F726C6421을 반환합니다.

- - -
### <a name="count"></a>개수
**설명:**  
Count 함수 hello 다중 값된 특성에 hello 수의 요소를 반환

**구문:**  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a>CNum
**설명:**  
hello CNum 함수는 문자열을 숫자 데이터 형식을 반환 합니다.

**구문:**  
`num CNum(str value)`

- - -
### <a name="cref"></a>CRef
**설명:**  
문자열 tooa 참조 특성으로 변환

**구문:**  
`ref CRef(str value)`

**예제:**  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a>CStr
**설명:**  
CStr 함수 hello tooa 문자열 데이터 형식으로 변환합니다.

**구문:**  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* 값: 숫자 값, 참조 특성 또는 부울입니다.

**예제:**  
`CStr([dn])`  
"cn=Joe,dc=contoso,dc=com"을 반환할 수 있습니다.

- - -
### <a name="dateadd"></a>DateAdd
**설명:**  
지정 된 시간 간격이 추가 된 날짜 toowhich를 포함 하는 날짜를 반환 합니다.

**구문:**  
`dt DateAdd(str interval, num value, dt date)`

* 간격: hello 간격 tooadd 시간에 해당 하는 문자열 식입니다. hello 문자열 hello를 다음 값 중 하나에 있어야 합니다.
  * yyyy 년
  * q 분기
  * m 월
  * y 연간 일자
  * d 일
  * w 요일
  * ww 주
  * h 시간
  * n 분
  * s 초
* 값: 수 hello 원하는 tooadd 단위입니다. 양수 수 있습니다 (tooget 날짜 이후 hello) 또는 음수 (과거 hello tooget 날짜).
* 날짜: 날짜/시간을 나타내는 날짜 toowhich hello 간격은 추가 됩니다.

**예제:**  
`DateAdd("m", 3, CDate("2001-01-01"))`  
3개월을 추가하고 "2001-04-01"을 나타내는 날짜/시간을 반환합니다.

- - -
### <a name="datefromnum"></a>DateFromNum
**설명:**  
DateFromNum 함수 hello AD의 날짜 형식 tooa DateTime 형식 값으로 변환합니다.

**구문:**  
`dt DateFromNum(num value)`

**예제:**  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
2012-01-01 23:00:00을 나타내는 날짜/시간을 반환합니다.

- - -
### <a name="dncomponent"></a>DNComponent
**설명:**  
hello DNComponent 함수는 지정된 된 DN 구성 왼쪽에서의 hello 값을 반환 합니다.

**구문:**  
`str DNComponent(ref dn, num ComponentNumber)`

* dn: hello 참조 특성 toointerpret
* Hello DN tooreturn ComponentNumber: hello 구성 요소

**예제:**  
`DNComponent([dn],1)`  
dn이 "cn=Joe,ou=…"인 경우 Joe를 반환합니다.

- - -
### <a name="dncomponentrev"></a>DNComponentRev
**설명:**  
hello DNComponentRev 함수는 지정된 된 DN 구성 오른쪽 (끝 hello)에서 hello 값을 반환 합니다.

**구문:**  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* dn: hello 참조 특성 toointerpret
* ComponentNumber-hello DN tooreturn의 hello 구성 요소
* 옵션: DC –"dc ="가 있는 모든 구성 요소를 무시합니다.

**예제:**  
dn이 "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com"인 경우  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
모두 US를 반환합니다.

- - -
### <a name="error"></a>오류
**설명:**  
hello 오차 함수는 사용 되는 tooreturn 사용자 지정 오류입니다.

**구문:**  
`void Error(str ErrorMessage)`

**예제:**  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
Hello / / accountName 특성이 없는 경우 hello 개체에서 오류를 throw 합니다.

- - -
### <a name="escapedncomponent"></a>EscapeDNComponent
**설명:**  
hello EscapeDNComponent 함수는 DN 중 하나의 구성 요소를 받아서 LDAP에 나타낼 수 있도록 이스케이프 합니다.

**구문:**  
`str EscapeDNComponent(str value)`

**예제:**  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
실행 하면 hello / / displayName 특성에 문자가 LDAP에서 이스케이프 해야 하는 경우에 LDAP 디렉터리에서 hello 개체를 만들 수 있습니다.

- - -
### <a name="formatdatetime"></a>FormatDateTime
**설명:**  
hello FormatDateTime 함수는 사용 되는 tooformat 지정 된 형식으로 DateTime tooa 문자열

**구문:**  
`str FormatDateTime(dt value, str format)`

* 값: hello 날짜/시간 형식의 값을
* 형식: hello 형식 tooconvert를 나타내는 문자열입니다.

**설명**  
hello 형식을 확인할 수 있습니다에 대 한 가능한 값을 hello: [사용자 정의 날짜/시간 형식 (Format 함수)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)

**예제:**  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
"2007-12-25"를 반환합니다.

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
"20140905081453.0Z"를 반환할 수 있습니다.

- - -
### <a name="guid"></a>GUID
**설명:**  
새로운 임의 GUID를 생성 하는 hello 함수 GUID

**구문:**  
`str GUID()`

- - -
### <a name="iif"></a>IIF
**설명:**  
IIF 함수 hello 지정된 된 조건에 따라 가능한 값의 집합 중 하나를 반환 합니다.

**구문:**  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* 조건: tootrue 또는 false 값 이나 일 수 있는 식을 평가 합니다.
* valueIfTrue: hello hello 조건이 tootrue, 값을 반환 합니다.
* valueIfFalse: hello hello 조건이 toofalse, 값을 반환 합니다.

**예제:**  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 Hello 사용자가 intern 인 경우 hello 별칭 "t-"로 사용자의 추가 toohello의 시작 부분을 다른 반환 hello 사용자의 별칭을 있는 그대로 반환 합니다.

- - -
### <a name="instr"></a>InStr
**설명:**  
hello InStr 함수는 문자열에서 부분 문자열의 첫 번째를 hello 찾습니다.

**구문:**  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* stringcheck: toobe 검색 문자열
* stringmatch: toobe 찾을 문자열
* 시작: 위치 toofind hello 부분 문자열 시작
* compare: vbTextCompare 또는 vbBinaryCompare

**설명**  
Hello 부분 문자열이 있는 반환 hello 위치 또는 인 경우 0 찾을 수 없습니다.

**예제:**  
`InStr("hello quick brown fox","quick")`  
Evalues too5

`InStr("repEated","e",3,vbBinaryCompare)`  
Too7 평가

- - -
### <a name="instrrev"></a>InStrRev
**설명:**  
hello InStrRev 함수는 문자열에서 하위 문자열의 마지막 항목과를 hello 찾습니다.

**구문:**  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* stringcheck: toobe 검색 문자열
* stringmatch: toobe 찾을 문자열
* 시작: 위치 toofind hello 부분 문자열 시작
* compare: vbTextCompare 또는 vbBinaryCompare

**설명**  
Hello 부분 문자열이 있는 반환 hello 위치 또는 인 경우 0 찾을 수 없습니다.

**예제:**  
`InStrRev("abbcdbbbef","bb")`  
7을 반환합니다.

- - -
### <a name="isbitset"></a>IsBitSet
**설명:**  
hello 약간 설정 되었는지 아닌지를 테스트 IsBitSet 함수

**구문:**  
`bool IsBitSet(num value, num flag)`

* 값: flag 하는 숫자 값: hello 있는 숫자 값을 비트 toobe 평가

**예제:**  
`IsBitSet(&HF,4)`  
"4" 비트가 16 진수 값 hello "F"으로 설정 되어 있으므로 True를 반환

- - -
### <a name="isdate"></a>IsDate
**설명:**  
Hello 식 수 있으면 hello IsDate 함수 평가 tooTrue 날짜/시간 형식으로 평가 합니다.

**구문:**  
`bool IsDate(var Expression)`

**설명**  
Cdate ()이 성공 될 수 있도록 toodetermine를 사용 합니다.

- - -
### <a name="iscert"></a>IsCert
**설명:**  
.NET X509Certificate2 인증서 개체에 hello 원시 데이터를 serialize 할 수 있으면 true를 반환 합니다.

**구문:**  
`bool CertThumbprint(binary certificateRawData)`  
*   certificateRawData: X.509 인증서의 바이트 배열 표현입니다. 인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.
- - -
### <a name="isempty"></a>IsEmpty
**설명:**  
Hello 특성은 hello CS 또는 MV에에서 존재 하지만 tooan 빈 문자열을 계산을 hello IsEmpty 함수 tooTrue를 계산 합니다.

**구문:**  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a>IsGuid
**설명:**  
Hello 문자열 변환된 tooa GUID 수을 hello IsGuid 함수 tootrue를 계산 합니다.

**구문:**  
`bool IsGuid(str GUID)`

**설명**  
GUID는 다음 패턴 중 하나로 정의됩니다. xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 또는 {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}

CGuid() 성공 수 있으면 toodetermine를 사용 합니다.

**예제:**  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
Hello StrAttribute GUID 형식이 있으면 이진 표현을 반환, 그렇지 않으면 Null을 반환 합니다.

- - -
### <a name="isnull"></a>IsNull
**설명:**  
Hello 식이 tooNull 이면 hello IsNull 함수는 true을 반환 합니다.

**구문:**  
`bool IsNull(var Expression)`

**설명**  
특성에 대 한 Null hello 없을 경우 hello 특성으로 표시 됩니다.

**예제:**  
`IsNull([displayName])`  
Hello CS 또는 MV에 hello 특성이 없을 경우 True를 반환 합니다.

- - -
### <a name="isnullorempty"></a>IsNullOrEmpty
**설명:**  
Hello 식이 null 또는 빈 문자열이 면 hello IsNullOrEmpty 함수 true 반환 합니다.

**구문:**  
`bool IsNullOrEmpty(var Expression)`

**설명**  
특성의 경우이 평가 tooTrue hello 특성이 없는 없거나 있지만 빈 문자열인 경우 됩니다.  
이 함수의 hello 역은 ispresent 라고 합니다.

**예제:**  
`IsNullOrEmpty([displayName])`  
Hello 특성이 없거나 hello CS 또는 MV에서 빈 문자열인 경우 True를 반환 합니다.

- - -
### <a name="isnumeric"></a>IsNumeric
**설명:**  
IsNumeric 함수 hello 숫자 형식으로 식이 계산 될 수 있는지 여부를 나타내는 부울 값을 반환 합니다.

**구문:**  
`bool IsNumeric(var Expression)`

**설명**  
CNum() 성공 tooparse hello 식 수 있으면 toodetermine를 사용 합니다.

- - -
### <a name="isstring"></a>IsString
**설명:**  
Hello 식 수 있는 경우 수 계산된 tooa 문자열 형식, tooTrue을 평가 하는 hello IsString 함수입니다.

**구문:**  
`bool IsString(var expression)`

**설명**  
있을지를 성공 tooparse hello 식 수 있으면 toodetermine를 사용 합니다.

- - -
### <a name="ispresent"></a>IsPresent
**설명:**  
Hello 식이 tooa 문자열을 Null이 아니고 비어 있지 않은 이면 IsPresent 함수는 true를 반환 hello 합니다.

**구문:**  
`bool IsPresent(var expression)`

**설명**  
이 함수의 hello 역은 isnullorempty 라고 합니다.

**예제:**  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a>항목
**설명:**  
hello Item 함수는 다중값된 문자열/특성에서 하나의 항목을 반환 합니다.

**구문:**  
`var Item(mvstr attribute, num index)`

* attribute: 다중값 특성
* 인덱스: hello 다중값된 문자열의 인덱스 tooan 항목입니다.

**설명**  
hello Item 함수는 두 함수 hello hello 다중 값된 특성에 hello 인덱스 tooan 항목을 반환 하므로 hello Contains 함수와 함께 사용 하면 유용 합니다.

인덱스가 범위를 초과하는 경우 오류가 나타납니다.

**예제:**  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
반환 hello 기본 전자 메일 주소입니다.

- - -
### <a name="itemornull"></a>ItemOrNull
**설명:**  
hello ItemOrNull 함수는 다중값된 문자열/특성에서 하나의 항목을 반환 합니다.

**구문:**  
`var ItemOrNull(mvstr attribute, num index)`

* attribute: 다중값 특성
* 인덱스: hello 다중값된 문자열의 인덱스 tooan 항목입니다.

**설명**  
hello ItemOrNull 함수는 두 함수 hello hello 다중 값된 특성에 hello 인덱스 tooan 항목을 반환 하므로 hello Contains 함수와 함께 사용 하면 유용 합니다.

인덱스가 범위를 초과하는 경우 Null 값을 반환합니다.

- - -
### <a name="join"></a>Join
**설명:**  
hello 조인 함수는 다중값된 문자열을 지정된 구분 기호 각 항목 사이 삽입 된 단일 값 문자열을 반환 합니다.

**구문:**  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* 특성: toobe 조인할 문자열 포함 하는 다중 값된 특성입니다.
* 구분 기호: 모든 문자열을 사용 하는 tooseparate hello 부분 문자열이 hello 문자열을 반환 했습니다. 생략 하면 hello 공백 문자 ("") 사용 됩니다. 경우 구분 기호가 빈 문자열 ("") 또는 없음으로 hello 목록의 모든 항목이 구분 기호 없이 연결 됩니다.

**설명**  
조인 hello 및 Split 함수 간에 패리티가 유지가 됩니다. hello Join 함수는 문자열의 배열을 사용 하 고 tooreturn 단일 문자열 구분 기호 문자열을 사용 하 여 연결 합니다. hello Split 함수는 문자열을 구분 기호로 구분 hello, tooreturn 문자열 배열입니다. 그러나 Join 함수는 모든 구분 기호 문자열을 사용하여 문자열을 연결할 수 있지만, Split 함수는 단일 문자 구분 기호를 사용하여 오직 문자열을 나눌 수만 있다는 것이 가장 중요한 차이점입니다.

**예제:**  
`Join([proxyAddresses],",")`  
"SMTP:john.doe@contoso.com,smtp:jd@contoso.com"을 반환할 수 있습니다.

- - -
### <a name="lcase"></a>LCase
**설명:**  
LCase 함수 hello 문자열 toolower 대/소문자의 모든 문자를 변환 합니다.

**구문:**  
`str LCase(str value)`

**예제:**  
`LCase("TeSt")`  
"test"를 반환합니다.

- - -
### <a name="left"></a>Left
**설명:**  
hello Left 함수는 문자열의 hello 왼쪽에서 지정한 개수의 문자를 반환합니다.

**구문:**  
`str Left(str string, num NumChars)`

* 문자열: 문자열 tooreturn 문자를 hello
* Hello (왼쪽) 문자열의 시작 부분에서 문자 tooreturn hello 수를 나타내는 숫자 NumChars:

**설명**  
Hello 문자열의 첫 번째 numChars 문자를 포함 하는 문자열:

* numChars = 0 인 경우, 빈 문자열을 반환합니다.
* numCahrs < 0,인 경우, 입력된 문자열을 반환합니다.
* 문자열이 null이면 빈 문자열을 반환합니다.

문자열에 numChars에서 지정한 hello 숫자 보다 적은 문자가 포함 된, 문자열 동일한 toostring (즉, 매개 변수 1의에서 모든 문자 포함)이 반환 됩니다.

**예제:**  
`Left("John Doe", 3)`  
"Joh"를 반환합니다.

- - -
### <a name="len"></a>Len
**설명:**  
hello Len 함수는 문자열의 문자 수를 반환합니다.

**구문:**  
`num Len(str value)`

**예제:**  
`Len("John Doe")`  
8을 반환합니다.

- - -
### <a name="ltrim"></a>LTrim.
**설명:**  
hello LTrim 함수는 문자열에서 선행 공백을 제거합니다.

**구문:**  
`str LTrim(str value)`

**예제:**  
`LTrim(" Test ")`  
"Test"를 반환합니다.

- - -
### <a name="mid"></a>Mid
**설명:**  
Mid hello 함수는 문자열의 지정된 된 위치에서 지정한 개수의 문자를 반환 합니다.

**구문:**  
`str Mid(str string, num start, num NumChars)`

* 문자열: 문자열 tooreturn 문자를 hello
* 시작: 위치 문자열 tooreturn 문자에서 시작 하는 hello를 식별 하는 번호
* 문자열의 위치에서 문자 tooreturn hello 수를 나타내는 숫자 NumChars:

**설명**  
문자열의 시작 위치에서 시작되는 numChars 문자를 반환합니다.  
문자열의 start 위치에서 numChars 문자를 포함하는 문자열:

* numChars = 0 인 경우, 빈 문자열을 반환합니다.
* numCahrs < 0,인 경우, 입력된 문자열을 반환합니다.
* 하는 경우 시작 > 문자열의 길이 hello, 입력된 문자열을 반환 합니다.
* start < = 0 인 경우, 입력된 문자열을 반환 합니다.
* 문자열이 null이면 빈 문자열을 반환합니다.

시작 위치에서 문자열의 numChar 문자가 남아있지 않는 경우, 가능한 많은 문자가 반환됩니다.

**예제:**  
`Mid("John Doe", 3, 5)`  
"hn Do"를 반환합니다.

`Mid("John Doe", 6, 999)`  
"Doe"를 반환합니다.

- - -
### <a name="now"></a>Now
**설명:**  
hello 이제 함수 반환 tooyour 컴퓨터의 시스템 날짜 및 시간에 따라 DateTime hello 현재 날짜와 시간을 지정 합니다.

**구문:**  
`dt Now()`

- - -
### <a name="numfromdate"></a>NumFromDate
**설명:**  
NumFromDate 함수 hello AD의 날짜 형식으로 날짜를 반환 합니다.

**구문:**  
`num NumFromDate(dt value)`

**예제:**  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
129699324000000000을 반환합니다.

- - -
### <a name="padleft"></a>padLeft
**설명:**  
hello PadLeft 함수 왼쪽 패드 지정 된 문자열 tooa 지정된 된 패드 문자를 사용 하 여 길이입니다.

**구문:**  
`str PadLeft(str string, num length, str padCharacter)`

* 문자열: 문자열 toopad hello 합니다.
* 길이: 문자열의 길이 원하는 hello를 나타내는 정수입니다.
* padCharacter:는 단일 문자 toouse hello 패드 문자로 구성 된 문자열

**설명**

* Hello 길이 문자열의 길이 보다 작은 경우, 다음 padCharacter를 반복적으로 추가 된 toohello (왼쪽) 문자열의 시작 부분 길이 같으면 toolength 포함 되어야 합니다.
* PadCharacter는 공백 문자가 될 수 있지만, null 값은 될 수 없습니다.
* 문자열의 길이 hello 같은 tooor 길이 보다 큰 경우 문자열이 변경 되지 않은 상태로 반환 됩니다.
* 문자열 길이 보다 큰 또는 같은 toolength 있으면 문자열 동일한 toostring 반환 됩니다.
* Hello 길이 문자열의 길이 보다 작은 경우 hello의 새 문자열 길이는 padCharacter로 채워진 문자열을 포함 된 원하는 다음입니다.
* 문자열이 null 인 경우 hello 함수는 빈 문자열을 반환 합니다.

**예제:**  
`PadLeft("User", 10, "0")`  
"000000User"를 반환합니다.

- - -
### <a name="padright"></a>PadRight
**설명:**  
hello PadRight 함수 오른쪽 패드 지정 된 문자열 tooa 지정된 된 패드 문자를 사용 하 여 길이입니다.

**구문:**  
`str PadRight(str string, num length, str padCharacter)`

* 문자열: 문자열 toopad hello 합니다.
* 길이: 문자열의 길이 원하는 hello를 나타내는 정수입니다.
* padCharacter:는 단일 문자 toouse hello 패드 문자로 구성 된 문자열

**설명**

* Hello 길이 문자열의 길이 보다 작은 경우 다음 padCharacter를 반복적으로 추가 된 toohello 끝 (오른쪽) 문자열 길이 같으면 toolength 포함 되어야 합니다.
* PadCharacter는 공백 문자가 될 수 있지만, null 값은 될 수 없습니다.
* 문자열의 길이 hello 같은 tooor 길이 보다 큰 경우 문자열이 변경 되지 않은 상태로 반환 됩니다.
* 문자열 길이 보다 큰 또는 같은 toolength 있으면 문자열 동일한 toostring 반환 됩니다.
* Hello 길이 문자열의 길이 보다 작은 경우 hello의 새 문자열 길이는 padCharacter로 채워진 문자열을 포함 된 원하는 다음입니다.
* 문자열이 null 인 경우 hello 함수는 빈 문자열을 반환 합니다.

**예제:**  
`PadRight("User", 10, "0")`  
"User000000"을 반환합니다.

- - -
### <a name="pcase"></a>PCase
**설명:**  
PCase 함수 hello hello 문자열 tooupper 경우에서 각 공백으로 구분 된 단어의 첫 번째 문자를 변환 하 고 다른 모든 문자를 변환할지 toolower 대/소문자입니다.

**구문:**  
`String PCase(string)`

**설명**

* 이 함수 현재 제공 하지 않습니다 적절 한 대/소문자 tooconvert 단어에는 약어와 같은 전체적으로 대문자입니다.

**예제:**  
`PCase("TEsT")`  
"test"를 반환합니다.

`PCase(LCase("TEST"))`  
"Test"를 반환합니다.

- - -
### <a name="randomnum"></a>RandomNum
**설명:**  
hello RandomNum 함수는 지정된 된 간격 사이의 난수를 반환합니다.

**구문:**  
`num RandomNum(num start, num end)`

* 시작: 숫자 식별 hello 하한값 hello 임의 값 toogenerate
* 끝:는 숫자 식별 hello의 상한값 hello 임의 값 toogenerate

**예제:**  
`Random(100,999)`  
734를 반환할 수 있습니다.

- - -
### <a name="removeduplicates"></a>RemoveDuplicates
**설명:**  
hello RemoveDuplicates 함수는 다중값된 문자열을 사용 하 고 각 값은 고유 해야 합니다.

**구문:**  
`mvstr RemoveDuplicates(mvstr attribute)`

**예제:**  
`RemoveDuplicates([proxyAddresses])`  
모든 중복 값을 제거한 삭제된 proxyAddress 특성을 반환합니다.

- - -
### <a name="replace"></a>Replace
**설명:**  
Replace 함수 hello 문자열 tooanother 문자열로 모두 바꿉니다.

**구문:**  
`str Replace(str string, str OldValue, str NewValue)`

* 문자열: 문자열 tooreplace 값입니다.
* OldValue:에 대 한 문자열 toosearch hello 및 tooreplace 합니다.
* NewValue: hello 문자열을 tooreplace 합니다.

**설명**  
hello 함수 hello 다음 특별 한 모니터를 인식 합니다.

* \n – 새로운 줄
* \r – 캐리지 반환
* \t – 탭

**예제:**  
`Replace([address],"\r\n",", ")`  
CRLF를 쉼표와 공백을로 바꾸고 너무 발생할 수 있습니다 "1 Microsoft 방식으로, Redmond, WA, USA"

- - -
### <a name="replacechars"></a>ReplaceChars
**설명:**  
ReplaceChars 함수 hello hello ReplacePattern 문자열에서에서 발견 되는 문자의 모두 바꿉니다.

**구문:**  
`str ReplaceChars(str string, str ReplacePattern)`

* 문자열: 문자열 tooreplace에 문자를 입력 합니다.
* ReplacePattern: tooreplace 문자를 사용 하 여 사전에 포함 하는 문자열입니다.

hello 형식은 {source1}: {target1}, {source2}: {target2}, {sourceN}, {targetn 이며} 여기서 소스는 hello 문자 toofind 및 대상 hello 문자열 tooreplace 사용 합니다.

**설명**

* hello 함수는 정의 된 소스의 각 항목을 사용 하 고 hello 대상이 있는 바꿉니다.
* hello 소스에는 정확히 하나의 (유니코드) 문자 여야 합니다.
* hello 소스는 비어 있거나 (구문 분석 오류)는 하나의 문자 보다 길 수 없습니다.
* hello 대상 oe, β:ss 예를 들어 여러 문자를 가질 수 있습니다.
* hello 대상 hello 문자를 제거 하도록 나타내는 비어 있을 수 있습니다.
* hello 대/소문자 구분 원본과 정확히 일치 해야 합니다.
* hello, (쉼표) 및: (콜론) 예약 된 문자 이며이 함수를 사용 하 여 바꿀 수 없습니다.
* 공백 및 hello ReplacePattern 문자열에서에서 기타 공백 문자는 무시 됩니다.

**예제:**  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
Raksmorgas를 반환합니다.

`ReplaceChars("O’Neil",%ReplaceString%)`  
/ / "ONeil", 단일 틱 hello 반환은 정의 toobe 제거 합니다.

- - -
### <a name="right"></a>Right
**설명:**  
Right 함수 hello hello 오른쪽 (끝) 문자열에서 지정한 개수의 문자를 반환합니다.

**구문:**  
`str Right(str string, num NumChars)`

* 문자열: 문자열 tooreturn 문자를 hello
* Hello 끝 (오른쪽) 문자열에서에서 문자 tooreturn hello 수를 나타내는 숫자 NumChars:

**설명**  
Hello 문자열의 마지막 위치부터 numchars 개의 문자가 반환 됩니다.

Hello 문자열의 마지막 numChars 문자를 포함 하는 문자열:

* numChars = 0 인 경우, 빈 문자열을 반환합니다.
* numCahrs < 0,인 경우, 입력된 문자열을 반환합니다.
* 문자열이 null이면 빈 문자열을 반환합니다.

문자열에 NumChars에서 지정한 숫자 hello 보다 적은 문자가 포함 된, 문자열 동일한 toostring 반환 됩니다.

**예제:**  
`Right("John Doe", 3)`  
"Doe"를 반환합니다.

- - -
### <a name="rtrim"></a>RTrim
**설명:**  
RTrim 함수 hello 문자열에서 후행 공백을 제거합니다.

**구문:**  
`str RTrim(str value)`

**예제:**  
`RTrim(" Test ")`  
"Test"를 반환합니다.

- - -
### <a name="select"></a>여기서
**설명:**  
지정된 함수에 기반하여 다중값 특성(또는 식 출력)의 모든 값을 처리합니다.

**구문:**  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* 항목: hello 다중값된 특성의 요소를 나타냅니다
* 특성: hello 다중값된 특성
* expression: 값의 컬렉션을 반환하는 식입니다.
* 조건: hello 특성에 있는 항목을 처리할 수 있는 모든 함수

**예제:**  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
Hello 다중값된 특성 otherPhone 하이픈 (-)를 제거한 후 모든 hello 값을 반환 합니다.

- - -
### <a name="split"></a>분할
**설명:**  
hello Split 함수는 구분 기호로 구분 된 문자열 다중값된 문자열을 만듭니다.

**구문:**  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* 값: 문자열 구분 기호 문자 tooseparate hello 합니다.
* 구분 기호: 단일 문자 toobe 구분 기호를 hello로 사용 합니다.
* limit: 반환될 수 있는 값의 최대 갯수입니다.

**예제:**  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
Hello / / proxyAddress 특성에 대 한 유용한 2 개의 요소가 있는 다중값된 문자열을 반환합니다.

- - -
### <a name="stringfromguid"></a>StringFromGuid
**설명:**  
hello StringFromGuid 함수는 이진 guid 및 tooa 문자열 변환

**구문:**  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a>StringFromSid
**설명:**  
StringFromSid 함수 hello 식별자 tooa 보안 문자열을 포함 하는 바이트 배열을 변환 합니다.

**구문:**  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a>Switch
**설명:**  
hello 스위치 함수는 사용 되는 tooreturn 평가 대상된 조건에 따라 단일 값입니다.

**구문:**  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* expr: tooevaluate 원하는 변형 식입니다.
* 값: 값 toobe hello 해당 식이 True 인 경우 반환 됩니다.

**설명**  
hello 스위치 함수 인수 목록 식 및 값의 쌍으로 구성 됩니다. hello 식은 왼쪽된 tooright에서 평가 됩니다 하 고 첫 번째 식 tooevaluate tooTrue hello와 연결 된 hello 값 반환 됩니다. Hello 부분 적절 하 게 쌍을 이루지 않으면 런타임 오류가 발생 합니다.

예를들어, expr1이 True면, Switch는 value1을 반환합니다. expr-1이 False이고, expr-2가 True면 Switch는 Value-2로 반환합니다.

다음의 경우 Switch는 Nothing을 반환합니다.

* Hello 식이 True가 없습니다.
* hello 첫 번째 True 식의 해당 값은 Null입니다.

그 중 하나만 반환되더라도, Switch는 모든 식을 계산합니다. 그렇기 때문에 원하지 않는 결과가 나타나지 않도록 주의해야합니다. 예를 들어 식 계산한 hello 0으로 나누기의 결과 오류가 발생 합니다.

값에는 사용자 지정 문자열을 반환 하는 hello 오류 함수를 될 수도 있습니다.

**예제:**  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
그렇지 않으면 오류가 반환, 일부 주요 도시의 통용 hello 언어를 반환 합니다.

- - -
### <a name="trim"></a>Trim
**설명:**  
hello Trim 함수는 선행 및 후행 공백이 문자열에서 제거 합니다.

**구문:**  
`str Trim(str value)`  

**예제:**  
`Trim(" Test ")`  
"test"를 반환합니다.

`Trim([proxyAddresses])`  
선행 및 후행 hello / / proxyAddress 특성의 각 값에 대 한 공백을 제거 합니다.

- - -
### <a name="ucase"></a>UCase
**설명:**  
UCase 함수 hello 문자열 tooupper 대/소문자의 모든 문자를 변환 합니다.

**구문:**  
`str UCase(str string)`

**예제:**  
`UCase("TeSt")`  
"test"를 반환합니다.

- - -
### <a name="where"></a>Where

**설명:**  
특정 조건에 기반하여 다중값 특성(또는 식 출력)의 값에 대한 하위 집합을 반환합니다.

**구문:**  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* 항목: hello 다중값된 특성의 요소를 나타냅니다
* 특성: hello 다중값된 특성
* 조건: tootrue 또는 false 일 수 있는 모든 식 평가
* expression: 값의 컬렉션을 반환하는 식입니다.

**예제:**  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
만료 되지 않습니다는 hello 다중값된 특성 userCertificate hello 인증서 값을 반환 합니다.

- - -
### <a name="with"></a>With
**설명:**  
함수로 hello 변수 toorepresent 하나 표시 되는 하위 식을 사용 하 여 또는 번 더 hello 복잡 한 식에 복잡 한 식 방식으로 toosimplify를 제공 합니다.

**구문:**
`With(var variable, exp subExpression, exp complexExpression)`  
* 변수: 나타냅니다 hello 하위 식입니다.
* subExpression: 변수로 표현되는 하위 식입니다.
* complexExpression: 복합 식입니다.

**예제:**  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
기능적으로 다음과 같습니다.  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
hello userCertificate 특성에 인증서 만료 되지 않은 값만을 반환합니다.


- - -
### <a name="word"></a>Word
**설명:**  
Word 함수 hello hello 구분 기호 toouse 및 hello 단어 번호 tooreturn 설명 하는 매개 변수를 기반 하는 문자열 내에 포함 된 단어를 반환 합니다.

**구문:**  
`str Word(str string, num WordNumber, str delimiters)`

* 문자열: 문자열 tooreturn 단어 hello 합니다.
* WordNumber: 반환해야 하는 단어 수를 식별하는 번호입니다.
* 구분 기호: 사용된 tooidentify 단어 되어야 하는 hello 구분 기호를 나타내는 문자열

**설명**  
구분 기호로 hello 문자 중 하나가 hello로 구분 된 문자열의 각 문자열은 단어로 식별 됩니다.

* 숫자가 < 1인경우 , 빈 문자열을 반환합니다.
* 문자열이 null이면, 빈 문자열을 반환합니다.

문자열이 단어 수보다 적거나, 구분 기호로 식별되는 단어를 포함할 경우, 빈 문자열이 반환됩니다.

**예제:**  
`Word("hello quick brown fox",3," ")`  
"brown"을 반환합니다.

`Word("This,string!has&many separators",3,",!&#")`  
"has"를 반환합니다.

## <a name="additional-resources"></a>추가 리소스
* [선언적 프로비전 식 이해](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [Azure AD Connect Sync: 사용자 지정 동기화 옵션](active-directory-aadconnectsync-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)

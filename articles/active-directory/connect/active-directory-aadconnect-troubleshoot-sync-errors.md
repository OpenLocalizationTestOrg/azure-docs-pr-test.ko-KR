---
title: "Azure AD Connect: 동기화 중의 오류 문제 해결 | Microsoft Docs"
description: "Azure AD Connect와 동기화 하는 동안 tootroubleshoot 오류가 발생 하는 방법에 대해 설명 합니다."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 2209d5ce-0a64-447b-be3a-6f06d47995f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: af262dfe95d686e34697454c0dfe8b4a6d8693c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-errors-during-synchronization"></a>동기화 중 오류 문제 해결
Windows Server Active Directory (AD DS) tooAzure Active Directory (Azure AD)에서 id 데이터를 동기화 할 때 오류가 발생할 수 있습니다. 이 문서에서는 이러한 방법으로 toofix hello 오류와 오류를 발생 시키는 hello 가능한 시나리오 중 일부의 동기화 오류 유형에 대 한 개요를 제공 합니다. 이 문서는 hello 일반적인 오류 유형을 포함 하 고 hello 가능한 모든 오류를 처리 하지 않을 수 있습니다.

 이 문서 hello 판독기가 hello 내부에 대해 잘 알고 있다고 가정 [디자인 개념을 Azure AD와 Azure AD Connect](active-directory-aadconnect-design-concepts.md)합니다.

Hello 최신 버전의 Azure AD Connect \(2016 이상이 년 8 월\)의 동기화 오류 보고서는 hello에서 사용할 수 있는 [Azure 포털](https://aka.ms/aadconnecthealth) 동기화에 대 한 Azure AD Connect Health의 일환으로 합니다.

2016 년 9 월 1 일 시작 [Azure Active Directory 복제 특성 복원 력](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) 모든 hello에 대해 기본적으로 기능을 사용할 수 있게 *새* Azure Active Directory 테 넌 트입니다. Hello 예정 된 월에 기존 테 넌 트에 대 한이 기능을 자동으로 사용할 수 있게 합니다.

Azure AD Connect 동기화 유지 hello 디렉터리에서 3 가지 유형의 작업 수행: 가져오기, 동기화 및 내보내기. 오류 모든 hello 작업에서 수행할 수 있습니다. 본이 문서는 주로 내보내기 tooAzure 광고 하는 동안 오류 발생 시에서는 합니다.

## <a name="errors-during-export-tooazure-ad"></a>내보내기 tooAzure AD 동안 발생 한 오류
다른 형식에 설명 섹션을 따라 동기화의 hello 내보내기 tooAzure AD 사용 하 여 작업 하는 동안 발생할 수 있는 오류 hello Azure AD 커넥터입니다. 이 커넥터는 "contoso hello 이름 형식으로 확인할 수 있습니다. *onmicrosoft.com*"입니다.
내보내기 tooAzure 광고 하는 동안 오류가 해당 hello 작업 \(추가, 업데이트, 삭제 등\) Azure AD Connect가 시도 \(동기화 엔진이\) Azure Active directory 실패 했습니다.

![내보내기 오류 개요](./media/active-directory-aadconnect-troubleshoot-sync-errors/Export_Errors_Overview_01.png)

## <a name="data-mismatch-errors"></a>데이터 불일치 오류
### <a name="invalidsoftmatch"></a>InvalidSoftMatch
#### <a name="description"></a>설명
* Azure AD 연결 하는 경우 \(동기화 엔진이\) Azure Active Directory tooadd 또는 업데이트 개체, Azure AD를 지시 일치 hello hello를 사용 하 여 들어오는 개체 **sourceAnchor** toohello 특성  **immutableId** 특성 Azure AD의 개체입니다. 이 일치를 **하드 일치**라고 합니다.
* 때 Azure AD **찾지 못하면** hello와 일치 하는 모든 개체 **immutableId** hello 사용 하 여 특성 **sourceAnchor** 프로 비전 하기 전에 hello 들어오는 개체의 특성을 새 toouse hello ProxyAddresses 대체 / UserPrincipalName 특성 toofind 일치 하는 개체입니다. 이 일치를 **소프트 일치**라고 합니다. hello 소프트 일치 디자인 된 toomatch hello 새 나타내는 개체를 동기화 하는 동안 추가/업데이트 되 고 hello를 사용 하 여 (즉 Azure AD의 출처는) Azure AD에 이미 있는 개체는 온-프레미스 동일한 엔터티 (사용자, 그룹).
* **InvalidSoftMatch** 때 오류가 발생 hello 하드 일치 항목이 일치 하는 모든 개체를 찾지 못하면 **AND** 소프트 일치 항목이 일치 하는 개체를 찾았지만 해당 개체의 다른 값은 *immutableId* 개체의 들어오는 hello 보다 *SourceAnchor*, 온-프레미스 Active Directory에서 다른 개체와 동기화 된 개체와 일치 하는 해당 hello를 제안 하는 것입니다.

즉, 소프트 일치 toowork hello에 대 한 순서로 소프트 일치 하는 hello 개체 toobe 없어야 hello에 대 한 모든 값 *immutableId*합니다. 모든 개체와 경우 *immutableId* InvalidSoftMatch 동기화 오류 hello 작업 결과, 값을 사용 하 여 집합 hello 하드 일치 하지만 만족 hello 소프트 일치 조건 실패 합니다.

특성을 azure Active Directory 스키마 두 개 이상의 개체 toohave hello hello 다음의 동일한 값을 사용 하지 못하도록 합니다. \(전체 목록은 아닙니다.\)

* ProxyAddresses
* UserPrincipalName
* onPremisesSecurityIdentifier
* ObjectId

> [!NOTE]
> [Azure AD 특성 중복 특성 복원 력](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) 기능 또한 롤아웃 될 Azure Active Directory의 hello 기본 동작으로 합니다.  이렇게 하면 하 여 Azure AD 복원 성도 뛰어납니다. 중복 된 ProxyAddresses와 UserPrincipalName 특성에 있는 온-프레미스 AD에서 처리 하는 hello 방식으로 Azure AD Connect (뿐만 아니라 다른 동기화 클라이언트)으로 표시 하는 동기화 오류 hello 수가 줄어듭니다. 환경입니다. 이 기능은 hello 중복 오류를 해결 하지 않습니다. 따라서 hello 데이터는 고정 toobe 여전히 필요 합니다. 하지만가 Azure AD에서 tooduplicated 값 인해 프로 비전 되 고, 그렇지 차단 되는 새 개체의 프로 비전 수 있습니다. 또한 hello toohello 동기화 클라이언트를 반환 하는 동기화 오류 수가 감소 합니다.
> 테 넌 트에이 기능을 사용할 경우 새 개체의 프로 비전 하는 동안 표시 하는 hello InvalidSoftMatch 동기화 오류 표시 되지 않습니다.
>
>

#### <a name="example-scenarios-for-invalidsoftmatch"></a>InvalidSoftMatch의 예제 시나리오
1. / / ProxyAddresses 특성 값이 동일한 온-프레미스 Active Directory에 존재 하는 hello로 두 개 이상의 개체. Azure AD에서는 하나만 프로비전되고 있습니다.
2. 동일한 값의 userPrincipalName이 온-프레미스 Active Directory에 존재 하는 hello로 두 개 이상의 개체. Azure AD에서는 하나만 프로비전되고 있습니다.
3. 개체가 추가 되었으면 hello에 온-프레미스 Active Directory hello로 동일한 Azure Active Directory에서 기존 개체의 유형을 / / ProxyAddresses 특성의 값입니다. Azure Active Directory의 온-프레미스에서 추가 hello 개체를 프로 비전 시작 됩니다.
4. 개체가 추가 되었으면에서 온-프레미스 Active Directory hello로 동일한 Azure Active Directory의 계정 유형을 userPrincipalName 특성의 값입니다. Azure Active Directory에 hello 개체를 프로 비전 시작 됩니다.
5. 동기화 된 계정은 2. Azure AD Connect (동기화 엔진)에서 ObjectGUID 특성 toocompute hello SourceAnchor를 사용 하는 포리스트 A tooForest에서 이동 했습니다. Hello 포리스트 이동 후의 hello SourceAnchor hello 값은 다릅니다. hello 새 개체 (포리스트 B)에서 Azure AD에서 toosync hello 기존 개체와 함께 실패 합니다.
6. 동기화 된 개체를 실수로 삭제 된에서 온-프레미스 Active Directory 및 새 개체에서에서 만든 Active Directory hello에 대 한 동일한 hello 계정을 Azure Active Directory에서 삭제 하지 않고 엔터티 (예: 사용자). 새 계정 hello toosync hello 기존 Azure AD 개체와 함께 실패합니다.
7. Azure AD Connect를 제거 후 다시 설치했습니다. Hello 다시 설치 하는 동안 서로 다른 특성은 SourceAnchor hello로 선택 되었습니다. 이전에 동기화가 hello 개체를 모두 중지 InvalidSoftMatch 오류와 함께 동기화 되었습니다.

#### <a name="example-case"></a>예제 사례:
1. **Bob Smith**는 *contoso.com*의 온-프레미스 Active Directory로부터 Azure Active Directory의 사용자와 동기화됩니다.
2. Bob Smith의 **UserPrincipalName**은어 **bobs@contoso.com**으로 설정되었습니다.
3. **"abcdefghijklmnopqrstuv = ="** 는 hello **SourceAnchor** Bob Smith를 사용 하 여 Azure AD connect 계산 **objectGUID** 에서 온-프레미스 Active Directory는는 hello **immutableId** Azure Active Directory에서 Bob Smith에 대 한 합니다.
4. 또한 Bob가지고 hello에 대 한 값을 다음 **proxyAddresses** 특성:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
5. 새 사용자, **Bob Taylor**, toohello 온-프레미스 Active Directory에 추가 됩니다.
6. Bob Taylor의 **UserPrincipalName**은 **bobt@contoso.com**으로 설정됩니다.
7. **"abcdefghijkl0123456789 = =" "** 는 hello **sourceAnchor** Bob Taylor를 사용 하 여 Azure AD connect 계산 **objectGUID** -프레미스 Active Directory에서 합니다. Bob Taylor 개체 tooAzure Active Directory를 아직 동기화 되지 않았습니다.
8. Bob Taylor가 hello 다음 hello / / proxyAddresses 특성에 대 한 값에는
   * smtp:bobt@contoso.com
   * smtp:bob.taylor@contoso.com
   * **smtp:bob@contoso.com**
9. 동기화 하는 동안 Azure AD Connect는 온-프레미스 Active Directory에서 Bob Taylor hello 추가 찾아내고 요청 Azure AD toomake hello 동일한 변경 합니다.
10. Azure AD는 먼저 하드 일치를 수행합니다. 개체가 없는 경우 모든 hello immutableId와 같은 너무 검색, 즉 "abcdefghijkl0123456789 = =". Azure AD에 이 immutableId를 갖는 다른 개체가 없으므로 하드 일치가 실패합니다.
11. Azure AD는 toosoft 일치를 시도 후 Bob Taylor 합니다. 즉, 개체가 없는 경우 모든 같은 toohello proxyAddresses와 세 개의 값을 포함 하 여 검색 합니다.smtp:bob@contoso.com
12. Azure AD는 toomatch hello 소프트 일치 조건 Bob Smith 개체 검색 됩니다. 이 개체에 hello immutableId 값 하지만 = "abcdefghijklmnopqrstuv = =". 즉 이 개체가 온-프레미스 Active Directory의 다른 개체와 동기화되었음을 나타냅니다. 따라서 Azure AD는 이 개체에 소프트 일치를 수행할 수 없고 **InvalidSoftMatch** 동기화 오류가 발생합니다.

#### <a name="how-toofix-invalidsoftmatch-error"></a>어떻게 toofix InvalidSoftMatch 오류
hello hello InvalidSoftMatch 오류에 대 한 가장 일반적인 이유는 두 개체의 다른 SourceAnchor \(immutableId\) hello hello 중에 사용 되는 hello ProxyAddresses 및/또는 UserPrincipalName 특성에 대해 같은 값이 있는 Azure AD에서 소프트 일치 프로세스입니다. 잘못 된 소프트 일치 순서 toofix hello에

1. 중복 hello proxyAddresses, userPrincipalName hello 오류가 발생 하는 다른 특성 값을 식별 합니다. 또한 두 개의 식별 \(이상의\) hello 충돌에 관련 된 개체입니다. 생성 된 보고서를 hello [동기화에 대 한 Azure AD Connect Health](https://aka.ms/aadchsyncerrors) hello 두 개체를 식별 하는 데 도움이 됩니다.
2. 개체를 계속 toohave hello 중복 값 및 개체가 없어야 식별 합니다.
3. 해당 값이 없어야 하는 hello 개체에서 hello 중복 값을 제거 합니다. Note hello 개체에서 원본으로 hello 디렉터리를 변경 하는 hello를 확인 해야 합니다. 경우에 따라 toodelete 충돌에서 hello 개체 중 하나를 할 수 있습니다.
4. Hello hello 온-프레미스 AD에서에서 변경 내용을 변경 하는 Azure AD Connect 동기화 hello를 사용 합니다.

참고 동기화에 대 한 Azure AD Connect Health 내에서 동기화 오류 보고서는 30 분 마다 업데이트 및 최신 동기화 시도 hello에서 hello 오류가 포함 됩니다.

> [!NOTE]
> ImmutableId를 기본적으로 변경 하지 않아야 hello 개체의 hello 수명에서. 부터 목록 위의 hello hello 시나리오 중 일부와 Azure AD Connect를 구성 하지 않은 경우 될 수 있습니다 Azure AD Connect의 hello SourceAnchor 나타내는 hello 동일한 엔터티는 hello AD 개체에 대 한 다른 값을 계산 하는 경우에서 (동일한 사용자 / 그룹/연락처 등) 올려진 toocontinue를 사용 하 여 원하는 기존 Azure AD 개체입니다.
>
>

#### <a name="related-articles"></a>관련 문서
* [Office 365에서 디렉터리 동기화를 방해하는 중복 또는 잘못된 특성](https://support.microsoft.com/en-us/kb/2647098)

### <a name="objecttypemismatch"></a>ObjectTypeMismatch
#### <a name="description"></a>설명
가능한는 서로 다른 두 개체가 "개체 유형" (예: 사용자, 그룹, 연락처 등)은 Azure AD가 toosoft match 두 개체를 hello tooperform hello 소프트 일치를 사용 하는 hello 특성 값이 있어야 합니다. 으로 Azure AD에서 이러한 특성의 중복 제거는 사용할 수 없습니다 "ObjectTypeMismatch" 동기화 오류 hello 작업이 발생할 수 있습니다.

#### <a name="example-scenarios-for-objecttypemismatch-error"></a>ObjectTypeMismatch 오류의 예제 시나리오
* Office 365에서 메일을 지원하는 보안 그룹이 만들어집니다. 새 사용자 또는 연락처를 추가 하는 관리자 온-프레미스 AD (즉 아직 tooAzure AD에 동기화 되지 않은) 같은 값과 같은 Office 365 hello hello / / ProxyAddresses 특성에 대 한 hello로 그룹화 합니다.

#### <a name="example-case"></a>예제 사례
1. 관리자는 새 메일 사용 가능 보안 그룹 Office 365의 hello 세금 부서에 대 한 만들고으로 전자 메일 주소를 제공 tax@contoso.com합니다. 이 할당의 hello 값으로이 그룹에 대 한 hello / / ProxyAddresses 특성**smtp:tax@contoso.com**
2. 새 사용자 Contoso.com을 조인 하 고 계정을 온-프레미스로 hello proxyAddress로 hello 사용자에 대해 만들어집니다.**smtp:tax@contoso.com**
3. Azure AD Connect에서 hello 새 사용자 계정을 동기화 하는 경우 hello "ObjectTypeMismatch" 오류를 가져오게 됩니다.

#### <a name="how-toofix-objecttypemismatch-error"></a>어떻게 toofix ObjectTypeMismatch 오류
hello ObjectTypeMismatch 오류에 대 한 hello 가장 일반적인 이유는 다른 유형 (사용자, 그룹, 연락처 등)의 두 개체는 hello 같은 hello / / ProxyAddresses 특성에 대 한 값입니다. 순서 toofix ObjectTypeMismatch를 hello:

1. 중복 hello 식별 proxyAddresses (또는 다른 특성) 값을 바꾸지 hello 오류입니다. 또한 두 개의 식별 \(이상의\) hello 충돌에 관련 된 개체입니다. 생성 된 보고서를 hello [동기화에 대 한 Azure AD Connect Health](https://aka.ms/aadchsyncerrors) hello 두 개체를 식별 하는 데 도움이 됩니다.
2. 개체를 계속 toohave hello 중복 값 및 개체가 없어야 식별 합니다.
3. 해당 값이 없어야 하는 hello 개체에서 hello 중복 값을 제거 합니다. Note hello 개체에서 원본으로 hello 디렉터리를 변경 하는 hello를 확인 해야 합니다. 경우에 따라 toodelete 충돌에서 hello 개체 중 하나를 할 수 있습니다.
4. Hello hello 온-프레미스 AD에서에서 변경 내용을 변경 하는 Azure AD Connect 동기화 hello를 사용 합니다. 동기화에 대 한 Azure AD Connect Health 내에서 동기화 오류 보고서 30 분 마다 업데이트 되 고 hello 최신 동기화 시도의 hello 오류를 포함 합니다.

## <a name="duplicate-attributes"></a>중복 특성
### <a name="attributevaluemustbeunique"></a>AttributeValueMustBeUnique
#### <a name="description"></a>설명
특성을 azure Active Directory 스키마 두 개 이상의 개체 toohave hello hello 다음의 동일한 값을 사용 하지 못하도록 합니다. 이 Azure AD에 있는 각 개체에 지정된 된 인스턴스에에서 이러한 특성의 고유한 값을 강제 toohave 합니다.

* ProxyAddresses
* UserPrincipalName

Azure AD Connect tooadd 새 개체를 시도 tooanother 개체가 Azure Active Directory에 이미 할당 되어 있는 특성 위에 hello에 대 한 값을 가진 기존 개체를 업데이트할 경우 hello 작업 hello "AttributeValueMustBeUnique" 동기화 오류가 발생 합니다.

#### <a name="possible-scenarios"></a>가능한 시나리오:
1. 중복 된 값은 다른 동기화 된 개체와 충돌 하는 할당 된 tooan 이미 동기화 된 개체입니다.

#### <a name="example-case"></a>예제 사례:
1. **Bob Smith**는 contoso.com의 온-프레미스 Active Directory로부터 Azure Active Directory의 사용자와 동기화됩니다.
2. Bob Smith의 온-프레미스 **UserPrincipalName**이 **bobs@contoso.com**으로 설정됩니다.
3. 또한 Bob가지고 hello에 대 한 값을 다음 **proxyAddresses** 특성:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
4. 새 사용자, **Bob Taylor**, toohello 온-프레미스 Active Directory에 추가 됩니다.
5. Bob Taylor의 **UserPrincipalName**은 **bobt@contoso.com**으로 설정됩니다.
6. **Bob Taylor** hello hello에 대 한 값을 뒤에 **ProxyAddresses** i 특성입니다. smtp:bobt@contoso.com ii입니다. smtp:bob.taylor@contoso.com
7. Bob Taylor의 개체가 Azure AD에 성공적으로 동기화됩니다.
8. 관리 결정 tooupdate Bob Taylor **ProxyAddresses** hello 다음 값을 사용 하 여 특성: i. **smtp:bob@contoso.com**
9. Azure AD가 값을 위에서 hello로 Azure AD에서 tooupdate Bob Taylor 개체를 시도 하지만 작업 실패 함을으로 ProxyAddresses 값 tooBob Smith, 이미 할당 되어 "AttributeValueMustBeUnique" 오류가 발생 합니다.

#### <a name="how-toofix-attributevaluemustbeunique-error"></a>어떻게 toofix AttributeValueMustBeUnique 오류
hello hello AttributeValueMustBeUnique 오류에 대 한 가장 일반적인 이유는 두 개체의 다른 SourceAnchor \(immutableId\) hello ProxyAddresses hello 및/또는 UserPrincipalName 특성 변수에 같은 값이 있어야 합니다. 순서 toofix AttributeValueMustBeUnique 오류에서

1. 중복 hello proxyAddresses, userPrincipalName hello 오류가 발생 하는 다른 특성 값을 식별 합니다. 또한 두 개의 식별 \(이상의\) hello 충돌에 관련 된 개체입니다. 생성 된 보고서를 hello [동기화에 대 한 Azure AD Connect Health](https://aka.ms/aadchsyncerrors) hello 두 개체를 식별 하는 데 도움이 됩니다.
2. 개체를 계속 toohave hello 중복 값 및 개체가 없어야 식별 합니다.
3. 해당 값이 없어야 하는 hello 개체에서 hello 중복 값을 제거 합니다. Note hello 개체에서 원본으로 hello 디렉터리를 변경 하는 hello를 확인 해야 합니다. 경우에 따라 toodelete 충돌에서 hello 개체 중 하나를 할 수 있습니다.
4. Hello hello 온-프레미스 AD에서에서 변경 내용을 Azure AD Connect 동기화 hello hello 오류 tooget 고정에 대 한 변경의 사용 수 있습니다.

#### <a name="related-articles"></a>관련 문서
-[Office 365에서 디렉터리 동기화를 방해하는 중복 또는 잘못된 특성](https://support.microsoft.com/en-us/kb/2647098)

## <a name="data-validation-failures"></a>데이터 유효성 검사 실패
### <a name="identitydatavalidationfailed"></a>IdentityDataValidationFailed
#### <a name="description"></a>설명
Azure Active Directory에 hello 데이터 자체 hello 디렉터리에 작성 된 해당 데이터 toobe 허용 하기 전에 여러 가지 제한을 적용 합니다. 이 최종 사용자가이 데이터에 의존 하는 hello 응용 프로그램을 사용 하는 동안 hello 최상의 가능한 경험을 얻는 tooensure입니다.

#### <a name="scenarios"></a>시나리오
a. hello UserPrincipalName 특성 값에 잘못 된/지원 되지 않는 문자가 있습니다.
b. hello UserPrincipalName 특성 hello 필요한 형식을 따르지 않습니다.

#### <a name="how-toofix-identitydatavalidationfailed-error"></a>어떻게 toofix IdentityDataValidationFailed 오류
a. 해당 hello userPrincipalName 특성에 지원 되는 문자 및 필요한 형식을 확인 합니다.

#### <a name="related-articles"></a>관련 문서
* [디렉터리 동기화 tooOffice 365 통해 tooprovision 사용자 준비](https://support.office.com/en-us/article/Prepare-to-provision-users-through-directory-synchronization-to-Office-365-01920974-9e6f-4331-a370-13aea4e82b3e)

### <a name="federateddomainchangeerror"></a>FederatedDomainChangeError
#### <a name="description"></a>설명
이 특정 한 경우에 발생 하는 **"FederatedDomainChangeError"** 하나의 페더레이션된 도메인 tooanother 페더레이션된 도메인에서 사용자의 UserPrincipalName의 hello 접미사 변경 될 때 오류를 동기화 합니다.

#### <a name="scenarios"></a>시나리오
동기화 된 사용자에 대 한 hello UserPrincipalName 접미사는 온-프레미스에서 하나의 페더레이션된 도메인 tooanother 페더레이션된 도메인에서 변경 되었습니다. 예를 들어 *UserPrincipalName = bob@contoso.com*  너무 변경 된*UserPrincipalName = bob@fabrikam.com* 합니다.

#### <a name="example"></a>예제
1. Bob Smith, Contoso.com에 대 한 계정을 UserPrincipalName hello로 Active Directory에 새 사용자로 추가bob@contoso.com
2. Bob 이동 tooa Fabrikam.com 및 그의 UserPrincipalName 이라는 Contoso.com의 다른 나누기 변경toobob@fabrikam.com
3. Contoso.com과 fabrikam.com 도메인은 모두 Azure Active Directory와 페더레이션된 도메인입니다.
4. Bob의 userPrincipalName이 업데이트되지 않아 “FederatedDomainChangeError” 동기화 오류가 발생합니다.

#### <a name="how-toofix"></a>어떻게 toofix
사용자의 UserPrincipalName 접미사 @ bob 으로부터 업데이트 된 경우**contoso.com** @ toobob**fabrikam.com**여기서 둘 다 **contoso.com** 및 **fabrikam.com** 는 **페더레이션 도메인**을 따라 이러한 단계 toofix hello 동기화 오류

1. Azure ad에서 hello 사용자의 UserPrincipalName 업데이트 bob@contoso.com toobob@contoso.onmicrosoft.com합니다. 다음 PowerShell 명령을 hello Azure AD PowerShell 모듈이 있는 hello를 사용할 수 있습니다.`Set-MsolUserPrincipalName -UserPrincipalName bob@contoso.com -NewUserPrincipalName bob@contoso.onmicrosoft.com`
2. Hello 다음 동기화 주기 tooattempt 동기화를 허용 합니다. 이 시간 동기화를 성공적으로 수행 됩니다. 및 Bob UserPrincipalName hello를 업데이트 합니다 toobob@fabrikam.com 예상 대로 합니다.

#### <a name="related-articles"></a>관련 문서
* [Hello 사용자 계정 toouse 다른 페더레이션된 도메인의 UPN을 변경한 후 변경 내용은 hello Azure Active Directory 동기화 도구에서 동기화 되지 않습니다.](https://support.microsoft.com/en-us/help/2669550/changes-aren-t-synced-by-the-azure-active-directory-sync-tool-after-you-change-the-upn-of-a-user-account-to-use-a-different-federated-domain)

## <a name="largeobject"></a>LargeObject
### <a name="description"></a>설명
Hello hello 동기화 작업으로 인해 특성 hello 크기 제한, 길이 제한 또는 Azure Active Directory 스키마가 설정한 개수 제한을 허용을 초과 하면 **LargeObject** 또는 **ExceededAllowedLength** 오류 동기화 합니다. 일반적으로 다음 특성 hello에 대 한이 오류 발생

* userCertificate
* userSMIMECertificate
* thumbnailPhoto
* proxyAddresses

### <a name="possible-scenarios"></a>가능한 시나리오
1. Bob의 userCertificate 특성에서 너무 많은 할당 된 인증서 tooBob를 저장 하 고 있습니다. 여기에는 오래되어 만료된 인증서가 포함될 수 있습니다. hello 하드 제한은 15 인증서입니다. UserCertificate 사용 하 여 toohandle LargeObject 오류 하십시오 특성 되는 방법에 대 한 자세한 내용은 참조 tooarticle [userCertificate 특성에 의해 발생 하는 처리 LargeObject 오류](active-directory-aadconnectsync-largeobjecterror-usercertificate.md)합니다.
2. Bob의 userSMIMECertificate 특성에서 너무 많은 할당 된 인증서 tooBob를 저장 하 고 있습니다. 여기에는 오래되어 만료된 인증서가 포함될 수 있습니다. hello 하드 제한은 15 인증서입니다.
3. Active Directory에 설정 하는 Bob의 thumbnailPhoto 너무 커서 toobe Azure AD에서 동기화입니다.
4. Active Directory에 hello / / ProxyAddresses 특성의 자동 채우기 동안 개체는 너무 많은 ProxyAddresses 할당을 갖습니다.

### <a name="how-toofix"></a>어떻게 toofix
1. Hello 오류를 발생 시키는 해당 hello 특성 제한이 허용 하는 hello 내 확인 하십시오.

## <a name="related-links"></a>관련 링크
* [Active Directory 관리 센터에서 Active Directory 개체 찾기](https://technet.microsoft.com/library/dd560661.aspx)
* [어떻게 Azure Active Directory PowerShell을 사용 하는 개체에 대 한 Azure Active Directory tooquery](https://msdn.microsoft.com/library/azure/jj151815.aspx)

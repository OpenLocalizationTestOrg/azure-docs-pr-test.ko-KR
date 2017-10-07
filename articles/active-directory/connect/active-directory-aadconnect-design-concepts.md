---
title: "Azure AD Connect: 설계 개념 | Microsoft Docs"
description: "이 항목에서는 특정 구현 설계 영역을 자세히 설명합니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4114a6c0-f96a-493c-be74-1153666ce6c9
ms.service: active-directory
ms.custom: azure-ad-connect
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1e5d5c6a716ca653fb14fc059e8155124b433732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-design-concepts"></a>Azure AD Connect: 설계 개념
이 항목의 hello 용도는 Azure AD Connect의 hello 구현 설계 하는 동안 간주할 수 있는 toodescribe 영역입니다. 이 항목은 특정 영역을 심층 분석하고 이 개념을 다른 항목에서처럼 간단히 설명합니다.

## <a name="sourceanchor"></a>sourceAnchor
hello sourceAnchor 특성으로 정의 됩니다 *개체의 hello 수명 동안 변경할 수 없는 특성*합니다. 개체를 고유 하 게 식별 hello 종류로 동일한 개체 온-프레미스와 Azure AD에서 합니다. hello 특성 라고도 **immutableId** hello 두 이름은 서로 바꿔 사용할 수는 데 사용 됩니다.

hello 단어에 변경할 수 없으므로 "을 변경할 수 없습니다", 중요 toothis 항목입니다. 이 설정 된 후에이 특성의이 값을 변경할 수 없으며, 되므로 중요 한 toopick을 지 원하는 시나리오 설계 합니다.

hello 특성은 다음 시나리오는 hello에 사용 됩니다.

* 새 동기화 엔진 서버를 구축하거나 재해 복구 시나리오를 다시 구축할 때,이 특성은 개체 온-프레미스의 Azure AD 내의 기존 개체에 연결됩니다.
* 클라우드 전용 id tooa 동기화 된 id 모델을 이동 하면 경우이 특성 개체가 너무 수 있도록 온-프레미스 개체와 Azure AD에 "하드 일치" 기존 개체입니다.
* 페더레이션 다음 hello와 함께이 특성을 사용 하는 경우 **userPrincipalName** hello에 사용 되는 사용자를 식별 하는 toouniquely 클레임 합니다.

이 항목 toousers 관련해 서에 sourceAnchor에 대 한 설명입니다. hello 동일한 규칙이 적용 tooall 개체 유형 이지만 사용자에 대해서만 일반적으로이 문제에이 중요 합니다.

### <a name="selecting-a-good-sourceanchor-attribute"></a>알맞은 sourceAnchor 특성을 선택합니다.
hello 특성 값을 hello 규칙에 따라야 합니다.

* 길이는 60자 미만이어야 합니다.
  * 문자가 a-z, A-Z 또는 0-9가 아니면 인코드되고 3개의 문자로 계산됩니다.
* &#92; ! # $ % & * + / = ? ^ &#96; { } | ~ < > ( ) ' ; : , [ ] " @ _
* 전역적으로 고유해야 합니다.
* 문자열, 정수 또는 이진이어야 합니다.
* 사용자 이름을 기반으로 할 수 없습니다. 사용자 이름은 변경됩니다.
* 대/소문자를 구분할 수 없으며 대/소문자에 따라 달라질 수 있는 값을 사용하지 않도록 해야 합니다.
* Hello 개체가 만들어질 때 할당 해야

Hello sourceAnchor를 선택한 경우 않습니다 형식 문자열의 Azure AD 연결 Base64Encode hello 특성 값 tooensure 특수 문자가 없는 표시 합니다. ADFS 보다 다른 페더레이션 서버를 사용 하는 경우 해야 서버 Base64Encode hello 특성 수도 있습니다.

hello sourceAnchor 특성은 대/소문자 구분입니다. "JohnDoe" 값 "johndoe"와 동일는 hello 있습니다. 하지만 대/소문자만 다른 두 개체가 있어서는 안 됩니다.

단일 포리스트가 있는 경우 온-프레미스를 사용 해야 하는 다음 hello 특성은 **objectGUID**합니다. 기본 설정을 사용 하 여 Azure AD Connect의 고도 DirSync에 의해 사용 되는 특성을 hello를 사용 하는 hello 특성 이기도 합니다.

다중 포리스트 되어 있고 이동 하지 마십시오 사용자 포리스트 및 도메인 사이의 다음 **objectGUID** 좋은 특성 toouse도이 경우에 합니다.

포리스트 및 도메인 간에 사용자를 이동 하는 경우 다음 찾아야는 특성을 변경 하지 않는 또는 이동할 수 있습니다 hello 사용자와 hello 이동 중. 권장 되는 방법에는 toointroduce 합성 특성입니다. GUID처럼 보이는 것을 포함할 수 있는 특성이 적합합니다. 개체를 만드는 동안 새 GUID는 만들고 hello 사용자에 게 표시 합니다. 사용자 지정 동기화 규칙을 만들 수 있습니다 hello 동기화 엔진 서버 toocreate hello에 따라이 값 **objectGUID** 및 업데이트 hello 선택한 특성에 추가 합니다. Hello 개체를 이동 하면이 값의 있는지 tooalso 복사 hello 내용을 확인 합니다.

다른 솔루션은 toopick 바뀌지 않으면 알고 있는 기존 특성입니다. 일반적으로 사용되는 특성에는 **employeeID**가 있습니다. 문자를 포함 하는 특성을 고려 하면 없는지 확인 (대문자 및 소문자) 가능성이 hello 케이스가 없는 hello 특성의 값에 대 한 변경할 수 있습니다. Hello 사용자의 hello 이름으로 해당 특성을 포함 하는 잘못 된 특성을 사용 하지 않아야 합니다. 결혼 또는 이혼 hello 이름이 예상된 toochange는이 특성에 대해 허용 되지 않습니다. 이 또한 한 가지 이유 이유와 같은 특성 **userPrincipalName**, **메일**, 및 **targetAddress** 가능한 tooselect hello Azure AD Connect 설치에서 되지 않습니다 마법사입니다. 이러한 특성에는 또한 hello 포함 "@" 문자는 hello sourceAnchor에 허용 되지 않습니다.

### <a name="changing-hello-sourceanchor-attribute"></a>Hello sourceAnchor 특성 변경
hello 개체가 Azure AD에서 생성 되었음을 있으며 hello identity 동기화 된 후에 hello sourceAnchor 특성 값을 변경할 수 없습니다.

이러한 이유로 hello 다음 제한 사항이 적용 tooAzure AD 연결:

* hello sourceAnchor 특성은 초기 설치 중만 설정할 수 있습니다. Hello 설치 마법사를 다시 실행 하는 경우이 옵션은 읽기 전용입니다. 필요한 경우 toochange이이 설정을 제거 하 고 다시 설치 해야 합니다.
* 해야 다른 Azure AD Connect 서버에 설치 하는 경우 선택 hello 같이 이전에 사용한 동일한 sourceAnchor 특성입니다. DirSync 사용 이전 하 고 AD tooAzure 이동 하는 경우 연결을 사용 해야 합니다 **objectGUID** DirSync에 의해 사용 되는 hello 특성 이므로 합니다.
* Hello 개체에 대 한 다음 Azure AD Connect 동기화 오류를 throw 하 고 hello 문제를 해결 하 고 hello sourceAnchor hello에서 다시 변경 하는 해당 개체에서 더 이상 변경 내용을 허용 하지 않는 내보낸된 tooAzure 광고를 수행한 후 sourceAnchor에 대 한 hello 값이 변경 되는 경우 소스 디렉터리입니다.

## <a name="using-msds-consistencyguid-as-sourceanchor"></a>msDS-ConsistencyGuid를 sourceAnchor로 사용
기본적으로 Azure AD Connect (1.1.486.0 버전 및 이전) objectGUID hello sourceAnchor 특성으로 사용 합니다. ObjectGUID는 시스템에서 생성됩니다. 온-프레미스 AD 개체를 만들 때는 해당 값을 지정할 수 없습니다. 섹션에서 설명한 대로 [sourceAnchor](#sourceanchor), toospecify hello sourceAnchor 값 해야 하는 시나리오가 있습니다. Hello 시나리오 인 적용 가능한 tooyou hello sourceAnchor 특성으로 구성 가능한 AD 특성 (예를 들어 게스트가 ConsistencyGuid)를 사용 해야 합니다.

Azure AD Connect (버전 1.1.524.0 후) 이제 sourceAnchor 특성으로 게스트가 ConsistencyGuid hello 사용을 용이 하 게 합니다. 이 기능을 사용할 경우 Azure AD Connect hello 동기화 규칙을을 자동으로 구성 합니다.

1. 게스트가 ConsistencyGuid를 사용자 개체에 대 한 hello sourceAnchor 특성으로 사용 합니다. ObjectGUID는 다른 개체 형식에 사용됩니다.

2. 지정 된 모든 온-프레미스 AD 사용자 개체 속성을 가진 게스트가 ConsistencyGuid 채워져 있지 Azure AD Connect는 온-프레미스 Active Directory에서 해당 objectGUID 값 백 toohello 게스트가 ConsistencyGuid 특성을 씁니다. Hello 게스트가 ConsistencyGuid 특성이 채워진 후에 Azure AD Connect 다음 hello 개체 tooAzure AD을 내보냅니다.

>[!NOTE]
> 한 번 온-프레미스 AD 개체 (즉, hello AD 커넥터 공간으로 가져오고 hello 메타 버스에 투영) Azure AD Connect로 가져오는, 더 이상 해당 sourceAnchor 값을 변경할 수 없습니다. toospecify hello sourceAnchor 값에 대 한는 주어진 온-프레미스 AD 개체, Azure AD Connect로 가져오기 전에 해당 게스트가 ConsistencyGuid 특성을 구성 합니다.

### <a name="permission-required"></a>필요한 권한
이 기능은 toowork에 대 한 hello AD DS 사용 되는 계정 toosynchronize 온-프레미스 Active Directory와 온-프레미스 Active Directory에서 쓰기 권한 toohello 게스트가 ConsistencyGuid 특성을 부여 되어야 합니다.

### <a name="how-tooenable-hello-consistencyguid-feature---new-installation"></a>Tooenable는 ConsistencyGuid 기능-새로 설치 하는 hello 하는 방법
새로 설치 하는 동안 sourceAnchor로 ConsistencyGuid hello 사용을 활성화할 수 있습니다. 이 섹션에서는 기본 설치 및 사용자 지정 설치를 자세히 설명합니다.

  >[!NOTE]
  > 최신 버전의 Azure AD Connect (1.1.524.0 후)에서는 새로 설치 하는 동안 ConsistencyGuid sourceAnchor 활용 hello 합니다.

### <a name="how-tooenable-hello-consistencyguid-feature"></a>Tooenable는 ConsistencyGuid 기능 hello 하는 방법
현재 hello 기능은 새로운 Azure AD Connect 설치 하는 동안만 활성화할 수 있습니다.

#### <a name="express-installation"></a>기본 설치
빠른 모드와 Azure AD Connect를 설치할 때 hello Azure AD Connect 마법사는 자동으로 가장 적절 한 광고 hello 특성 toouse 논리 hello를 사용 하 여 hello sourceAnchor 특성으로 결정:

* 먼저, Azure AD 테 넌 트 tooretrieve hello AD 특성으로 사용 하는 hello Azure AD Connect 마법사 쿼리 hello hello 이전 Azure AD Connect 설치에 sourceAnchor 특성 (있는 경우). 이 정보를 사용할 수 있는 경우 Azure AD Connect hello 동일한 AD 특성을 사용 합니다.

  >[!NOTE]
  > 최신 버전의 Azure AD Connect (1.1.524.0 후) 설치 하는 동안 사용 되는 hello sourceAnchor 특성에 대 한 Azure AD 테 넌 트의 정보를 저장 합니다. 이전 버전의 Azure AD Connect는 그렇지 않습니다.

* 사용 하는 hello sourceAnchor 특성에 대 한 정보를 사용할 수 없는 경우 hello 마법사는 온-프레미스 Active Directory에 hello 게스트가 ConsistencyGuid 특성의 hello 상태를 확인 합니다. Hello 디렉터리에서 개체에 hello 특성이 구성 되지 않으면 hello 마법사 hello 게스트가 ConsistencyGuid hello sourceAnchor 특성으로 사용 합니다. Hello 디렉터리에 있는 하나 이상의 개체에 hello 특성은 구성 된 경우 hello 특성 다른 응용 프로그램에서 사용 되 고 sourceAnchor 특성으로 적합 하지 않은 hello 마법사 종료 중...

* 이 경우 hello 마법사 대신 toousing objectGUID hello sourceAnchor 특성으로 합니다.

* Hello sourceAnchor 특성은 결정 되 면 hello 마법사 Azure AD 테 넌 트에 hello 정보를 저장 합니다. hello 정보는 나중에 Azure AD Connect 설치 하 여 사용 됩니다.

Express 설치가 완료 되 면 hello 마법사 hello 원본 앵커 특성으로 사용할 특성 선택 않은 알려 줍니다.

![sourceAnchor로 선택된 AD 특성을 알려주는 마법사](./media/active-directory-aadconnect-design-concepts/consistencyGuid-01.png)

#### <a name="custom-installation"></a>사용자 지정 설치
Azure AD Connect 사용자 지정 모드를 설치할 때는 hello Azure AD Connect 마법사 sourceAnchor 특성을 구성할 때 두 가지 옵션이 제공 합니다.

![사용자 지정 설치 - sourceAnchor 구성](./media/active-directory-aadconnect-design-concepts/consistencyGuid-02.png)

| 설정 | 설명 |
| --- | --- |
| Azure 내 hello 원본 앵커를 관리할 수 있도록 | Azure AD toopick hello 특성을 원하는 경우이 옵션을 선택 합니다. 이 옵션을 선택 하는 경우 Azure AD Connect 마법사 적용 hello 동일 [Express 설치 중에 사용 하는 sourceAnchor 특성 선택 논리](#express-installation)합니다. 유사한 tooExpress 설치 hello 마법사 알려는 특성 선택 않은 hello로 원본 앵커 특성 사용자 지정 설치가 완료 된 후입니다. |
| 특정 특성 | Toospecify hello sourceAnchor 특성으로 기존 AD 특성을 원하는 경우이 옵션을 선택 합니다. |

### <a name="how-tooenable-hello-consistencyguid-feature---existing-deployment"></a>Tooenable는 ConsistencyGuid 기능-기존 배포를 hello 하는 방법
Hello 원본 앵커 특성으로 objectGUID를 사용 하는 기존 Azure AD Connect 배포를 설정한 경우 전환할 수도 있습니다 toousing ConsistencyGuid 대신 합니다.

>[!NOTE]
> 최신 버전의 Azure AD Connect (1.1.552.0 후) hello 원본 앵커 특성으로 ObjectGuid tooConsistencyGuid에서 전환 지원 합니다.

hello 원본 앵커 특성으로 objectGUID tooConsistencyGuid에서 tooswitch:

1. Hello Azure AD Connect 마법사를 시작 하 고 클릭 **구성** toogo toohello 작업 화면입니다.

2. 선택 hello **원본 앵커 구성** 옵션을 작업 하 고 클릭 **다음**합니다.

   ![기존 배포에 대해 ConsistencyGuid 사용 - 2단계](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment01.png)

3. Azure AD 관리자 자격 증명을 입력하고 **다음**을 클릭합니다.

4. Azure AD Connect 마법사는 온-프레미스 Active Directory에 hello 게스트가 ConsistencyGuid 특성의 hello 상태를 분석합니다. Hello 특성에서 구성 되지 않으면 개체를 다른 응용 프로그램에서 현재 hello 특성을 사용 하며 안전 toouse 있는지 디렉터리, Azure AD Connect 끝나는 hello 것 hello 원본 앵커 특성으로 합니다. 클릭 **다음** toocontinue 합니다.

   ![기존 배포에 대해 ConsistencyGuid 사용 - 4단계](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment02.png)

5. Hello에 **준비 tooConfigure** 화면 **구성** toomake hello 구성 변경 합니다.

   ![기존 배포에 대해 ConsistencyGuid 사용 - 5단계](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment03.png)

6. Hello 구성 완료 되 면 해당 게스트가 ConsistencyGuid hello 원본 앵커 특성으로 사용 중인 hello 마법사에 표시 합니다.

   ![기존 배포에 대해 ConsistencyGuid 사용 - 6단계](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment04.png)

Hello 분석 (4 단계) 하는 동안 hello 특성 hello 디렉터리에 있는 하나 이상의 개체에 구성 된 경우 hello 마법사 완료 hello 특성 다른 응용 프로그램에서 사용 되 고 아래 hello 다이어그램에 나타난 것 처럼 오류가 반환 됩니다. 인 경우 해당 hello 특성은 기존 응용 프로그램에 사용 되지 않는 특정 toosuppress 오류 hello 하는 방법에 대 한 내용은 toocontact 지원 해야 합니다.

![기존 배포에 대해 ConsistencyGuid 사용 - 오류](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeploymenterror.png)

### <a name="impact-on-ad-fs-or-third-party-federation-configuration"></a>AD FS 또는 타사 페더레이션 구성에 미치는 영향
Azure를 사용 하는 경우 AD Connect toomanage 온-프레미스 AD FS 배포, Azure AD Connect hello sourceAnchor로 hello 클레임 규칙 toouse hello 동일한 AD 특성을 자동으로 업데이트 합니다. 이렇게 하면 ad FS에 의해 생성 된 해당 hello ImmutableID 클레임 hello sourceAnchor 값 내보낸된 tooAzure AD와 일치 합니다.

Hello sourceAnchor 값과 일치 하는 클레임 toobe 내보낸 tooAzure AD로 ImmutableID에 대 한 클레임 규칙 hello를 수동으로 업데이트 해야 Azure AD Connect 외부에서 AD FS를 관리 하는 인증에 대 한 타사 페더레이션 서버를 사용 하는 경우 문서 섹션에 설명 된 [수정 AD FS 클레임 규칙](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-management#modclaims)합니다. hello 마법사 설치가 완료 된 후에 경고를 수행 하는 hello를 반환 합니다.

![타사 페더레이션 구성](./media/active-directory-aadconnect-design-concepts/consistencyGuid-03.png)

### <a name="adding-new-directories-tooexisting-deployment"></a>새 디렉터리 tooexisting 배포 추가
배포한 Azure AD Connect hello ConsistencyGuid 기능을 사용 하 고 원하는 tooadd 이제 다른 디렉터리 toohello 배포 가정 합니다. Tooadd hello 디렉터리를 시도할 때 Azure AD Connect 마법사 hello 디렉터리에 hello 게스트가 ConsistencyGuid 특성의 hello 상태를 확인 합니다. Hello 디렉터리에 있는 하나 이상의 개체에 hello 특성은 구성 된 경우 hello 마법사 완료 hello 특성 다른 응용 프로그램에서 사용 되 고 아래 hello 다이어그램에 나타난 것 처럼 오류가 반환 됩니다. 인 경우 해당 hello 특성은 기존 응용 프로그램에 사용 되지 않는 특정 toosuppress 오류 hello 하는 방법에 대 한 내용은 toocontact 지원 해야 합니다.

![새 디렉터리 tooexisting 배포 추가](./media/active-directory-aadconnect-design-concepts/consistencyGuid-04.png)

## <a name="azure-ad-sign-in"></a>Azure AD 로그인
Azure AD와 온-프레미스 디렉터리를 통합 하는 동안 것이 중요 한 toounderstand hello 동기화 설정을 hello 방식으로 사용자에 주는 영향을 인증 합니다. Azure AD는 UPN (userPrincipalName) tooauthenticate hello 사용자를 사용합니다. 그러나 사용자가 동기화 하는 경우에 hello 특성 toobe userPrincipalName의 값에 대해 신중 하 게 사용을 선택 해야 합니다.

### <a name="choosing-hello-attribute-for-userprincipalname"></a>UserPrincipalName에 대 한 hello 특성을 선택합니다.
확인 해야 Azure 곳에 사용 되는 UPN toobe hello 값을 제공 하는 데 hello 특성 선택 하면

* hello 형식의 것 않은 toohello UPN 구문 (RFC 822)를 준수 하는 hello 특성 값username@domain
* hello 접미사의 hello hello 값 일치 tooone의 Azure AD에서 사용자 지정 도메인 확인

기본 설정 hello hello 특성에 대 한 선택 항목은 userPrincipalName 가정 합니다. Hello userPrincipalName 특성에 hello 값이 포함 되어 있지 않으면 tooAzure에서 프로그램 사용자 toosign 합니다를 선택 해야 **사용자 지정 설치**합니다.

### <a name="custom-domain-state-and-upn"></a>사용자 지정 도메인 상태 및 UPN
것이 중요 한 tooensure hello UPN 접미사에 대 한 확인 된 도메인 임을 합니다.

John은 contoso.com의 사용자입니다. 이한일은 원하는 toouse hello 온-프레미스 UPN john@contoso.com toosign tooAzure 한 후에 사용자가 Azure AD tooyour 디렉터리 contoso.onmicrosoft.com. toodo에 따라서 동기화 했는지, tooadd 필요 하 고 시작 하려면 먼저 Azure AD에서 contoso.com으로 사용자 지정 도메인 확인 hello 사용자를 동기화 하는 중입니다. John, 예를 들어 contoso.com의 hello UPN 접미사는 Azure AD에서 확인 된 도메인을 일치 하지 않습니다, Azure AD contoso.onmicrosoft.com으로 hello UPN 접미사를 바꿉니다.

### <a name="non-routable-on-premises-domains-and-upn-for-azure-ad"></a>라우팅할 수 있는 온-프레미스가 아닌 도메인 및 Azure AD에 대한 UPN
일부 조직에는 라우팅할 수 없는 도메인(예: contoso.local) 또는 간단한 단일 레이블 도메인(예: contoso)이 있습니다. Azure AD에 수 tooverify 라우팅할 수 없는 도메인 없는 있습니다. Azure AD Connect Azure AD의 tooonly 확인 된 도메인을 동기화 할 수 있습니다. Azure AD 디렉터리를 만들면 라우팅 가능한 도메인을 만들고 다시 Azure AD에 대한 기본 도메인(예: contoso.onmicrosoft.com)이 됩니다. 따라서 데이터베이스가 필요한 tooverify 이러한 시나리오에서는 다른 라우팅 가능한 도메인 toosync toohello 기본 onmicrosoft.com 도메인 원하는 경우에 합니다.

읽기 [추가 사용자 지정 도메인 이름을 tooAzure Active Directory](../active-directory-add-domain.md) 에 대 한 자세한 정보를 추가 하 고 도메인을 확인 합니다.

Azure AD Connect는 라우팅할 수 없는 도메인 환경에서 실행하는지를 검색하고 Express 설정을 계속 진행하는 경우 적절하게 경고합니다. 해당 hello hello 사용자의 UPN이 가능성이 라우팅할 수 없는 도메인에서 작동 하는 경우 라우팅할 수 없는 접미사를 너무 있어야 합니다. 예를 들어 Azure AD Connect를 contoso.local에서 실행 하는 경우 기본 설정을 사용 하는 대신 있습니다 toouse 사용자 지정 설정을 제안 합니다. 수 toospecify hello 특성 hello 사용자가 동기화 된 tooAzure AD 후 tooAzure에 UPN toosign으로 사용 해야 하는 사용자 지정 설정을 사용 하 고 합니다.

## <a name="next-steps"></a>다음 단계
[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.

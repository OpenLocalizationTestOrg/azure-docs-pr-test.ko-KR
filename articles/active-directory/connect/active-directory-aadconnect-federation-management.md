---
title: "aaaActive Directory 페더레이션 서비스 관리 및 Azure AD Connect와 사용자 정의 | Microsoft Docs"
description: "Azure AD Connect를 사용한 AD FS 관리 및 Azure AD Connect와 PowerShell을 사용한 사용자 AD FS 로그인 환경의 사용자 지정입니다."
keywords: "AD FS, ADFS, AD FS 관리, AAD Connect, 연결, 로그인, AD FS 사용자 지정, 트러스트 복구, O365, 페더레이션, 신뢰 당사자"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a>Azure AD Connect를 사용하여 Active Directory Federation Services 관리 및 사용자 지정
이 문서에서는 설명 방법을 toomanage 및 Azure Active Directory (Azure AD) 연결을 사용 하 여 Active Directory Federation Services (AD FS)를 사용자 지정 합니다. AD FS 팜 전체 구성에 대 한 toodo이 필요할 수 있습니다 다른 일반적인 AD FS 작업 포함 됩니다.

| 항목 | 포함된 내용 |
|:--- |:--- |
| **AD FS 관리** | |
| [복구 hello 신뢰](#repairthetrust) |어떻게 Office 365와 toorepair hello 페더레이션 신뢰 합니다. |
| [대체 로그인 ID를 사용하여 Azure AD와 페더레이션](#alternateid) | 대체 로그인 ID를 사용하여 페더레이션 구성  |
| [AD FS 서버 추가](#addadfsserver) |어떻게 추가 AD FS 서버가 있는 AD FS tooexpand 팜 합니다. |
| [AD FS 웹 응용 프로그램 프록시 서버 추가](#addwapserver) |어떻게 추가 응용 프로그램 프록시 WAP (웹) 서버가 있는 AD FS tooexpand 팜 합니다. |
| [페더레이션된 도메인을 추가합니다.](#addfeddomain) |어떻게 tooadd 페더레이션된 도메인입니다. |
| [Hello SSL 인증서 업데이트](active-directory-aadconnectfed-ssl-update.md)| 어떻게 tooupdate hello SSL 인증서는 AD FS 팜에 대 한 합니다. |
| **AD FS 사용자 지정** | |
| [사용자 지정 회사 로고 또는 일러스트레이션 추가](#customlogo) |어떻게 toocustomize AD FS 로그인 페이지 회사 로고 및 일러스트레이션 합니다. |
| [로그인 설명 추가](#addsignindescription) |어떻게 tooadd에 로그인 페이지 설명 합니다. |
| [AD FS 클레임 규칙 수정](#modclaims) |어떻게 toomodify AD FS는 다양 한 페더레이션 시나리오에 대 한 클레임입니다. |

## <a name="manage-ad-fs"></a>AD FS 관리
Hello Azure AD Connect 마법사를 사용 하 여 최소한의 사용자 개입으로 Azure AD Connect에서 다양 한 AD FS와 관련 된 작업을 수행할 수 있습니다. Hello 마법사를 실행 하려면 hello 마법사를 실행 하 여 Azure AD Connect 설치를 마친 후 다시 tooperform 추가 작업 합니다.

## 복구 hello 신뢰<a name=repairthetrust></a>
Azure AD Connect toocheck hello hello AD FS의 현재 상태와 Azure AD 신뢰를 사용 하 여 수 있으며 toorepair hello 신뢰 적절 한 조치를 수행할 수 있습니다. 따라 이러한 단계 toorepair Azure AD와 AD FS 신뢰 합니다.

1. 선택 **복구 AAD와 ad FS를 신뢰** 추가 작업의 hello 목록에서 합니다.
   ![AAD 및 ADFS 트러스트 복구](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)

2. Hello에 **tooAzure AD 연결** 페이지 Azure AD에 대 한 전역 관리자 자격 증명을 제공 하 고 클릭 **다음**합니다.
   ![TooAzure AD 연결](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)

3. Hello에 **원격 액세스 자격 증명** 페이지에서 도메인 관리자에 게 hello 자격 증명을 입력 합니다.

   ![원격 액세스 자격 증명](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    **다음**을 클릭한 후 Azure AD Connect가 인증서 상태를 확인하고 문제를 표시합니다.

    ![인증서의 상태](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    hello **준비 tooconfigure** 페이지 toorepair hello 신뢰를 수행할 수 있는 작업이 hello 목록을 보여 줍니다.

    ![준비 tooconfigure](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. 클릭 **설치** toorepair hello 신뢰 합니다.

> [!NOTE]
> Azure AD Connect는 자체 서명된 인증서에 대해서만 복구 또는 조치를 취할 수 있습니다. Azure AD Connect에서 타사 인증서를 복구할 수 없습니다.

## <a name=alternateid></a>대체 ID를 사용하여 Azure AD와 페더레이션
Hello 온-프레미스 사용자 계정 Name(UPN) 및 동일한 사용자 계정 이름 유지 되는 hello 클라우드 hello는 것이 좋습니다. Hello 온-프레미스 UPN 사용 (예: 라우팅할 수 없는 도메인. Contoso.local)을 변경할 수 없습니다 또는 toolocal 응용 프로그램 종속성 인해 좋습니다 대체 로그인 id입니다. 대체 로그인 ID는 로그인, 메일 등의 해당 UPN 이외의 특성으로 사용자가 로그인 수 있는 환경 tooconfigure가 있습니다. Active Directory에서 Azure AD Connect 기본값 toohello userPrincipalName 특성의 사용자 계정 이름에 대 한 hello 선택 합니다. 사용자 계정 이름에 대해 다른 특성을 선택하고 AD FS를 사용하여 페더레이션할 경우 Azure AD Connect는 대체 로그인 ID에 맞게 AD FS를 구성합니다. 사용자 계정 이름으로 선택할 수 있는 다른 특성은 아래와 같습니다.

![대체 ID 특성 선택 항목](media/active-directory-aadconnect-federation-management/attributeselection.png)

AD FS에 대한 대체 로그인 ID 구성은 크게 다음 두 단계로 구성됩니다.
1. **Hello 오른쪽 발급 클레임 집합이 구성**: hello Azure AD 신뢰 당사자에 hello 발급 클레임 규칙 수정된 toouse 선택한 hello UserPrincipalName 특성은 hello hello 사용자의 대체 ID를 신뢰 합니다.
2. **Hello AD FS 구성에 대체 로그인 ID를 사용 하도록 설정**: AD FS hello 대체 id입니다. 사용 하는 hello 적절 한 포리스트에 사용자가 조회할 수 있도록 hello AD FS 구성을 업데이트 됩니다 이 구성은 Windows Server 2012 R2(KB2919355) 이상의 AD FS에 대해 지원됩니다. Hello AD FS 서버는 2012 r 2 인 경우 hello hello 있는지 확인 합니다. Azure AD Connect KB이 필요 합니다. Hello KB 검색 되지 않으면 경고가 나타납니다 구성이 완료 된 후 아래와 같이:

    ![2012R2의 KB 누락에 대한 경고](media/active-directory-aadconnect-federation-management/kbwarning.png)

    누락 된 KB 발생할 경우 toorectify hello 구성 hello 필요한 설치 [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) hello 트러스트를 사용 하 여 다음 복구 및 [복구 AAD 및 AD FS 신뢰](#repairthetrust)합니다.

> [!NOTE]
> Toomanually alternateID 및 단계에 대 한 자세한 내용은 구성, 읽기 [대체 로그인 ID 구성](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)

## AD FS 서버 추가 <a name=addadfsserver></a>

> [!NOTE]
> tooadd AD FS 서버에 Azure AD Connect hello PFX 인증서가 필요 합니다. 따라서 Azure AD Connect를 사용 하 여 hello AD FS 팜을 구성 하는 경우에이 작업을 수행할 수 있습니다.

1. **추가 페더레이션 서버 배포**를 선택하고 **다음**을 클릭합니다.

   ![추가 페더레이션 서버](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. Hello에 **tooAzure AD 연결** 페이지, Azure AD에 대 한 전역 관리자 자격 증명을 입력 하 고 클릭 **다음**합니다.

   ![TooAzure AD 연결](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. Hello 도메인 관리자 자격 증명을 제공 합니다.

   ![도메인 관리자 자격 증명](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. Azure AD Connect Azure AD Connect를 사용 하 여 새 AD FS 팜을 구성 하는 동안 사용자가 제공한 hello PFX 파일의 hello 암호를 요청 합니다. 클릭 **암호 입력** tooprovide hello hello PFX 파일 암호를 합니다.

   ![인증서 암호](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![SSL 인증서 지정](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. Hello에 **AD FS 서버** 페이지 hello 서버 이름 또는 IP 주소 toobe 추가 입력 toohello AD FS 팜을 합니다.

   ![AD FS 서버](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. 클릭 **다음**, 이동 하 여 최종 hello **구성** 페이지. Azure AD Connect hello 서버 toohello AD FS 팜에 추가 완료 되 면 hello 옵션 tooverify hello 연결을 제공 됩니다.

   ![준비 tooconfigure](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![설치 완료](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## AD FS WAP 서버 추가 <a name=addwapserver></a>

> [!NOTE]
> WAP 서버 tooadd Azure AD Connect hello PFX 인증서가 필요 합니다. 따라서 Azure AD Connect를 사용 하 여 hello AD FS 팜을 구성한 경우이 작업에 수행할 수만 있습니다.

1. 선택 **웹 응용 프로그램 프록시 배포** hello 사용 가능한 작업 목록에서 합니다.

   ![웹 응용 프로그램 프록시 배포](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. Hello Azure 전역 관리자 자격 증명을 제공 합니다.

   ![TooAzure AD 연결](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. Hello에 **지정 SSL 인증서** 페이지에서 Azure AD Connect와 hello AD FS 팜을 구성할 때 사용자가 제공한 hello PFX 파일에 대 한 hello 암호를 제공 합니다.
   ![인증서 암호](media/active-directory-aadconnect-federation-management/WapServer3.PNG)

    ![SSL 인증서 지정](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. WAP 서버로 추가 하는 hello 서버 toobe를 추가 합니다. Hello WAP 서버는 도메인에 가입된 toohello 되지 않을 수 있습니다, 때문에 추가 되 고 관리자 자격 증명이 toohello 서버 hello 마법사 요청 합니다.

   ![관리 서버 자격 증명](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. Hello에 **프록시 트러스트 자격 증명** 페이지 신뢰 및 액세스 hello 팜의 기본 서버로 hello AD FS 관리 자격 증명이 tooconfigure hello 프록시를 제공 합니다.

   ![프록시 트러스트 자격 증명](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. Hello에 **준비 tooconfigure** hello 마법사 페이지에서 수행 되는 작업 목록은 hello에 표시 합니다.

   ![준비 tooconfigure](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. 클릭 **설치** toofinish hello 구성 합니다. Hello 구성이 완료 되 면 hello 마법사 제공 옵션 tooverify hello 연결 toohello 서버 hello 합니다. 클릭 **확인** toocheck 연결 합니다.

   ![설치 완료](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## 페더레이션된 도메인을 추가합니다. <a name=addfeddomain></a>

것이 쉬운 tooadd 도메인 toobe Azure AD Connect를 사용 하 여 Azure AD와 페더레이션 합니다. Azure AD Connect 페더레이션에 대 한 hello 도메인을 추가 하 고 Azure AD와 페더레이션 하는 여러 도메인이 있는 경우 규칙 toocorrectly hello 발급자를 반영 하는 hello 클레임을 수정 합니다.

1. tooadd 페더레이션된 도메인으로 선택 hello 작업 **더 추가 Azure AD 도메인**합니다.

   ![추가 Azure AD 도메인](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. Hello hello 마법사의 다음 페이지에서 Azure AD에 대 한 hello 전역 관리자 자격 증명을 제공 합니다.

   ![TooAzure AD 연결](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. Hello에 **원격 액세스 자격 증명** 페이지 hello 도메인 관리자 자격 증명을 제공 합니다.

   ![원격 액세스 자격 증명](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. Hello 다음 페이지에서 hello 마법사는 온-프레미스 디렉터리와 페더레이션 할 수 있는 Azure AD 도메인의 목록을 제공 합니다. Hello 도메인 hello 목록에서 선택 합니다.

   ![Azure AD 도메인](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    Hello 도메인을 선택한 후 hello 마법사 영향 hello 구성 hello를 가져와 됩니다 있습니다 마법사 hello 추가 작업에 대 한 적절 한 정보를 제공 합니다. 경우에 따라 hello을 제공 합니다. 정보 toohelp Azure AD에서 확인 아직 하지 않는 도메인을 선택할 경우 hello 도메인을 확인 합니다. 참조 [추가 사용자 지정 도메인 이름을 tooAzure Active Directory](../active-directory-add-domain.md) 내용을 확인 합니다.

5. **다음**을 누릅니다. hello **준비 tooconfigure** 페이지 hello Azure AD Connect를 수행 하는 작업 목록이 표시 됩니다. 클릭 **설치** toofinish hello 구성 합니다.

   ![준비 tooconfigure](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> Hello에서 사용자가 추가 수 toologin tooAzure AD 됩니다 전에 페더레이션된 도메인을 동기화 해야 합니다.

## <a name="ad-fs-customization"></a>AD FS 사용자 지정
hello 다음 섹션에서는 hello 일반적인 작업 중 일부에 대 한 AD FS 로그인 페이지를 사용자 지정할 때 tooperform를 발생할 수 있습니다.

## 사용자 지정 회사 로고 또는 일러스트레이션 추가 <a name=customlogo></a>
hello에 표시 되는 hello 회사의 toochange hello 로고 **로그인** 페이지에서 다음 Windows PowerShell cmdlet 및 구문을 hello를 사용 합니다.

> [!NOTE]
> hello hello 로고는 10KB 이내인 파일 크기는 96dpi에서 260 x 35에 크기를 권장 합니다.

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> hello *TargetName* 매개 변수는 필수입니다. AD FS와 함께 제공 되는 hello 기본 테마의 기본을 이름은입니다.

## 로그인 설명 추가 <a name=addsignindescription></a>
로그인 페이지 설명 toohello tooadd **로그인 페이지**, hello 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다.

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## AD FS 클레임 규칙 수정 <a name=modclaims></a>
AD FS에서 사용할 수 있는 풍부한 클레임 언어 원하는 toocreate 사용자 지정 클레임 규칙입니다. 자세한 내용은 참조 [hello 클레임 규칙 언어의 역할 hello](https://technet.microsoft.com/library/dd807118.aspx)합니다.

hello 다음 단원에서는 tooAzure AD 및 AD FS 페더레이션 관련 된 일부 시나리오에 대 한 사용자 지정 규칙을 작성 하는 방법.

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a>Hello 특성에 없는 값에 조건부 변경할 수 없는 ID
Azure AD Connect를 사용 하면 개체가 경우 원본 앵커 tooAzure AD 동기화로 사용 하는 특성 toobe를 지정할 수 있습니다. Hello 값 hello 사용자 지정 특성에 비어 있지 않은 경우에 변경할 수 없는 ID 클레임 tooissue를 할 수 있습니다.

예를 들어, 선택할 수 **ms-ds-consistencyguid** hello 원본 앵커 및 문제에 대 한 hello 특성으로 **ImmutableID** 으로 **ms-ds-consistencyguid** 사례 hello에 특성에 대 한 값을 있습니다. Hello 특성에 대 한 값이 없는 경우 발급 **objectGuid** 대로 hello 변경할 수 없는 id입니다. 사용자 지정 클레임 규칙 집합이 hello hello 다음 섹션에에서 설명 된 대로 생성할 수 있습니다.

**규칙 1: 쿼리 특성**

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

이 규칙에 hello 값을 쿼리 하는 **ms-ds-consistencyguid** 및 **objectGuid** Active Directory에서 사용자 hello에 대 한 합니다. AD FS 배포에서 hello 저장소 이름 tooan 적절 한 저장소 이름을 변경 합니다. 에 대해 정의 된 대로 페더레이션에서는 hello 클레임 유형 tooa 적절 한 클레임 종류를 변경할 수도 **objectGuid** 및 **ms-ds-consistencyguid**합니다.

또한를 사용 하 여 **추가** 아닌 **문제**, 나가는 문제 hello 엔터티에 대 한 추가 하지 않도록 하 고 hello 값 중간 값으로 사용할 수 있습니다. 변경할 수 없는 id입니다. hello으로 어떤 값 toouse를 설정한 후 이상 규칙에 hello 클레임을 발급 합니다.

**규칙 2: hello 사용자에 대 한 ms-ds-consistencyguid 있는지 확인**

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

이 규칙은 이라는 임시 플래그를 정의 **idflag** 너무 설정 된**useguid** 없는 경우 없는 **ms-ds-consistencyguid** hello 사용자에 대해 채워집니다. 이 뒤에 있는 hello 논리 hello 팩트 AD FS가 빈 클레임을 허용 하지 않는 것입니다. 규칙 1에 클레임 http://contoso.com/ws/2016/02/identity/claims/objectguid 및 http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid를 추가할 때 /fd 되므로 **msdsconsistencyguid** 경우에만 클레임 hello 사용자에 대 한 hello 값은 채워집니다. 채워지지 않은 경우 AD FS는 빈 값을 갖는 것을 확인하고 즉시 삭제합니다. 모든 개체에는 **objectGuid**가 있으므로 규칙 1이 실행된 후 항상 클레임이 발생합니다.

**규칙 3: 있는 경우 변경이 불가능한 ID로 ms-ds-consistencyguid 발급**

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

이는 암시적 **Exist** 확인입니다. Hello 클레임에 대 한 hello 값이 있으면 그런 후 실행 하는 변경할 수 없는 hello로 id입니다. hello를 사용 하 여 hello 이전 예제 **nameidentifier** 클레임입니다. 해야 toochange이 toohello 적절 한 클레임 유형을 변경할 수 없는 ID hello에 대 한 사용자 환경에서 합니다.

**규칙 4: ms-ds-consistencyGuid가 없는 경우 변경이 불가능한 ID로 objectGuid 발급**

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

이 규칙에 단순히 hello 임시 플래그를 확인 하는지에 **idflag**합니다. Tooissue hello 클레임 기반 하는지 여부를 결정할 값에 있습니다.

> [!NOTE]
> 이러한 규칙의 hello 순서가 중요 합니다.

### <a name="sso-with-a-subdomain-upn"></a>하위 도메인 UPN을 사용한 SSO
에 설명 된 대로 Azure AD Connect를 사용 하 여 페더레이션 도메인 toobe를 여러 개 추가할 수 있습니다 [새 페더레이션된 도메인을 추가](active-directory-aadconnect-federation-management.md#addfeddomain)합니다. 수정 해야 hello 사용자 계정 이름 (UPN) 클레임 hello 발급자 ID toohello 루트 도메인 및 해당 hello 하위 도메인 되지 않도록 hello 자식 hello 페더레이션된 루트 도메인에 대해서도 설명 합니다.

기본적으로 hello 클레임 ID가로 설정 하는 발급자에 대 한 규칙:

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![기본 발급자 ID 클레임](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

hello 기본 규칙 hello UPN 접미사를 가져와서을 hello 발급자 ID 클레임에 사용 합니다. 예를 들어 John은 sub.contoso.com의 사용자이고 contoso.com은 Azure AD를 사용하여 페더레이션됩니다. John 입력 john@sub.contoso.com tooAzure AD에에서 로그인 하는 동안 사용자 이름 hello으로 합니다. AD FS의 hello 기본 발급자 ID 클레임 규칙 hello 방식으로 다음이 처리 합니다.

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

**클레임 값:** http://sub.contoso.com/adfs/services/trust/

toohave 유일한 hello 루트 도메인의 hello 발급자 클레임 값 같이 hello 클레임 규칙 toomatch hello 다음 변경 합니다.

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a>다음 단계
[사용자 로그인 옵션](active-directory-aadconnect-user-signin.md)에 대해 알아봅니다.

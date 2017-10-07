---
title: "aaaIdentity 동기화 및 중복 특성 복원 력 | Microsoft Docs"
description: "어떻게 toohandle 개체와 함께 UPN 또는 / / ProxyAddress 충돌 하는 동안 Azure AD Connect를 사용 하 여 디렉터리 동기화의 새로운 동작입니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 537a92b7-7a84-4c89-88b0-9bce0eacd931
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.openlocfilehash: e27dcbf9d71f83fa9566cae2fd99350297d1cd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="identity-synchronization-and-duplicate-attribute-resiliency"></a>ID 동기화 및 중복 특성 복원력
중복 특성 복원력은 Microsoft의 동기화 도구 중 하나를 실행하는 경우 **UserPrincipalName** 및 **ProxyAddress**의 충돌로 발생하는 마찰을 제거하는 Azure Active Directory의 기능입니다.

이 두 특성은 모두에서 일반적으로 필요한 toobe 고유 **사용자**, **그룹**, 또는 **연락처** 지정된 Azure Active Directory 테 넌 트의 개체입니다.

> [!NOTE]
> 사용자만 UPN을 가질 수 있습니다.
> 
> 

이 기능을 사용 하는 새로운 동작 hello hello 동기화 파이프라인의 hello 클라우드 부분에 있으면 클라이언트 알 수 없는 및 Azure AD Connect, 디렉터리 동기화 및 MIM + 커넥터를 포함 하 여 Microsoft 동기화 제품에 대 한 관련 되므로 합니다. hello 일반 용어 "동기화 클라이언트"는이 문서 toorepresent 이러한 제품 중 하나에 사용 됩니다.

## <a name="current-behavior"></a>현재 동작
가 시도 tooprovision이 고유성 제약 조건을 위반 하는 UPN 또는 / / ProxyAddress 값으로 새 개체를 Azure Active Directory는 해당 개체를 만들지를 차단 합니다. 마찬가지로, 고유 하지 않은 UPN 또는 / / ProxyAddress 개체 업데이트 되 면 hello 업데이트가 실패 합니다. 시도 업데이트를 프로 비전 하는 hello 각 내보내기 주기 시 hello 동기화 클라이언트에서 다시 시도 되 고 toofail hello 충돌이 해결 될 때까지 계속 됩니다. 각 시도 시 생성 되는 오류 보고서 전자 메일 및 hello 동기화 클라이언트에서 오류가 기록 됩니다.

## <a name="behavior-with-duplicate-attribute-resiliency"></a>중복 특성 복원력으로 동작
완전히 대신 tooprovision 실패 하거나 중복 된 특성으로 Azure Active Directory "를 선택 하면" hello 고유성 제약 조건을 위반 하 게 hello 중복 된 특성 개체를 업데이트 합니다. 이 특성에 필요한 경우 프로 비전, UserPrincipalName, 같은 hello 서비스 자리 표시자 값을 할당 합니다. 이러한 임시 값의 hello 형식은  
“***<OriginalPrefix>+<4DigitNumber>@<InitialTenantDomain>.onmicrosoft.com***”.  
다음과 같은 hello 특성이 필요 하지 않은 경우는 **/ / ProxyAddress**, Azure Active Directory 단순히 hello 충돌 특성을 격리 하 고 hello 개체 만들기 또는 업데이트를 진행 합니다.

Hello 특성을 격리 시 hello 충돌에 대 한 정보 hello 이전 동작에 사용 되는 동일한 오류 보고서를 전자 메일 hello에 전송 됩니다. 그러나이 정보에만 나타납니다 hello 오류 보고서에 한 번 발생 하는 hello 격리 하는 경우 것 중지 toobe 기록 나중에 전자 메일 됩니다. 또한이 개체에 대 한 hello 내보내기에 성공 하면 이후 hello 동기화 클라이언트 오류를 기록 하지 않습니다 하 고는 hello를 다시 시도 하지 만들기 / 업데이트 작업을 다음 동기화 주기 시.

이 문제는 새 특성 되었습니다 toosupport toohello 사용자, 그룹 및 연락처 개체 클래스를 추가 했습니다.  
**DirSyncProvisioningError**

위반 하는 hello 고유성 제약 조건을 추가 해야 정상적으로 사용 되는 toostore hello 충돌 하는 특성이 있는 다중 값된 특성입니다. 백그라운드 타이머 작업에 대 한 중복 된 특성 충돌 해결 및 격리를 통해 문제의 hello 특성을 자동으로 제거 하는 모든 시간 toolook를 실행 하는 Azure Active Directory에 설정 되었습니다.

### <a name="enabling-duplicate-attribute-resiliency"></a>중복 특성 복원력 활성화
중복 특성 복원 력 모든 Azure Active Directory 테 넌 트 간에 hello 새로운 기본 동작을 됩니다. 2016 년 8 월 22 일 년 이후에 처음으로 hello에 대 한 동기화를 사용 하도록 설정 된 모든 테 넌 트에 대해 기본적으로에 됩니다. 동기화 이전 toothis 날짜를 사용 하도록 설정 된 테 넌 트 hello 기능 일괄 처리에서 사용 하도록 설정 해야 합니다. 2016 년 9 월에에서 시작 됩니다.이 출시 및 tooeach 테 넌 트의 기술 알림 접촉이 hello 특정 날짜 hello 기능을 설정할 때 전자 메일 알림이 전송 됩니다.

> [!NOTE]
> 중복 특성 복원력이 설정된 후에는 해제할 수 없습니다.

테 넌 트에 대 한 hello 기능이 활성화 된 경우 toocheck, 후 그렇게 hello hello Azure Active Directory PowerShell 모듈의 최신 버전을 다운로드 및 실행 하 여:

`Get-MsolDirSyncFeatures -Feature DuplicateUPNResiliency`

`Get-MsolDirSyncFeatures -Feature DuplicateProxyAddressResiliency`

> [!NOTE]
> 테 넌 트에 대해 켜져 전에 집합 MsolDirSyncFeature cmdlet tooproactively hello 중복 특성 탄력성 기능을 사용을 더 이상 사용할 수 없습니다. toobe 수 tootest hello 기능을 새 Azure Active Directory 테 넌 트 toocreate가 필요 합니다.

## <a name="identifying-objects-with-dirsyncprovisioningerrors"></a>DirSyncProvisioningErrors로 개체 식별
Tooduplicate 속성 충돌, PowerShell Azure Active Directory 및 Office 365 관리 포털 hello 인해 이러한 오류가 있는 tooidentify 개체는 현재 두 가지 방법입니다. 계획 tooextend tooadditional 포털 기반 보고 hello 앞에 있습니다.

### <a name="azure-active-directory-powershell"></a>Azure Active Directory PowerShell
이 항목의 PowerShell cmdlet hello에 대 한 hello 다음은 true입니다.

* Cmdlet을 다음 hello 모두 대/소문자 구분입니다.
* hello **– ErrorCategory PropertyConflict** 항상 포함 되어야 합니다. 다른 종류의 현재는 **ErrorCategory**, 하지만 hello 향후에 확장할 수 있습니다.

먼저 **Connect-MsolService**를 실행하고 테넌트 관리자에 대한 자격 증명을 입력하여 시작합니다.

그런 다음 다른 방법으로 다음 cmdlet과 연산자에 해당 하는 tooview의 오류 hello를 사용 합니다.

1. [모두 표시](#see-all)
2. [속성 형식으로](#by-property-type)
3. [충돌 값으로](#by-conflicting-value)
4. [문자열 검색을 사용하여](#using-a-string-search)
5. [정렬](#sorted)
6. [제한된 수량 또는 모두](#in-a-limited-quantity-or-all)

#### <a name="see-all"></a>모두 표시
연결 되 면 toosee 일반 프로 비전 오류 hello 테 넌 트에 특성 목록을 실행 합니다.

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict`

이 hello 다음과 같은 결과 생성합니다.  
 ![Get MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "Get MsolDirSyncProvisioningError")  

#### <a name="by-property-type"></a>속성 형식으로
속성 형식에 의해 toosee 오류 추가 hello **-PropertyName** hello로 플래그 **UserPrincipalName** 또는 **ProxyAddresses** 인수:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName UserPrincipalName`

또는

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName ProxyAddresses`

#### <a name="by-conflicting-value"></a>충돌 값으로
toosee 오류 tooa 특정 속성을 관련 된 추가 hello **-PropertyValue** 플래그 (**-PropertyName** 이 플래그를 추가 하는 경우 함께 사용 해야 합니다).

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyValue User@domain.com -PropertyName UserPrincipalName`

#### <a name="using-a-string-search"></a>문자열 검색을 사용하여
hello를 사용 하는 광범위 한 문자열 검색 toodo **-SearchString** 플래그입니다. 이 사용할 수 독립적으로 모든 플래그의 hello 예외와 함께 위의 hello **-ErrorCategory PropertyConflict**는 항상 필요한 것은:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -SearchString User`

#### <a name="in-a-limited-quantity-or-all"></a>제한된 수량 또는 모두
1. **MaxResults <Int>**  수 toolimit hello 쿼리 tooa 특정 수의 값을 사용 합니다.
2. **모든** 사용된 tooensure 오류가 많이 있는 경우 모두 hello 모든 결과 검색 될 수 있습니다.

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -MaxResults 5`

## <a name="office-365-admin-portal"></a>Office 365 관리 포털
Hello Office 365 관리 센터에서 디렉터리 동기화 오류를 볼 수 있습니다. hello Office 365 포털만 화면에서 보고서를 hello **사용자** 이러한 오류가 있는 개체입니다. **그룹** 및 **연락처** 간의 충돌에 대한 정보는 표시하지 않습니다.

![활성 사용자](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "활성 사용자")

Admin 님 안녕하세요 Office 365에서에서 디렉터리 동기화 오류 tooview 센터 방법에 지침은 [Office 365의 디렉터리 동기화 오류를 식별](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)합니다.

### <a name="identity-synchronization-error-report"></a>ID 동기화 오류 보고서
충돌 하는 중복 된 특성을 가진 개체에 포함 된 알림을이 새로운 동작으로 처리 될 때 Identity 동기화 오류 보고서에 전자 메일로 보낼 hello 표준 toohello 기술 알림 연락처 hello 테 넌 트에 대 한 전송 됩니다. 그러나 이 동작에서 중요한 변경 사항이 있습니다. Hello 지난에 중복 된 특성 충돌에 대 한 정보 hello 충돌이 해결 될 때까지 모든 후속 오류 보고서에 포함 됩니다. 이 새로운 동작으로 지정 된 충돌에 대 한 hello 오류 알림 않습니다에 표시 한 번-hello 시간 hello 충돌 하는 특성 격리 됩니다.

모양의 어떤 hello 전자 메일 알림 / / ProxyAddress 충돌에 대 한 예는 다음과 같습니다.  
    ![활성 사용자](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "활성 사용자")  

## <a name="resolving-conflicts"></a>충돌 해결
이러한 오류에 대 한 전략 및 해결 방법을 문제를 해결 하지 다를 수는 hello 방식 hello 지난 오류 중복 된 특성을 처리 합니다. hello 유일한 차이점은 hello 충돌을 해결 되 면 hello 테 넌 트 서비스 측 tooautomatically hello 통해 hello 타이머 작업 스윕의 질문 toohello 적절 한 개체에 hello 특성 추가 한다는 합니다.

hello 다음 문서에 간략하게 설명 다양 한 문제 해결 및 해결 방법: [중복 되거나 잘못 된 특성에는 Office 365의 디렉터리 동기화 되지 않게](https://support.microsoft.com/kb/2647098)합니다.

## <a name="known-issues"></a>알려진 문제
이러한 알려진 문제로 인해 데이터 손실 또는 서비스 저하가 발생하지 않습니다. 그 중 일부는 미적인 따라서는 다른 표준 "*사전 복원 력*" 중복 된 특성 오류 toobe hello 충돌 특성을 포함 하며 다른 격리 대신 throw 하면 특정 오류 toorequire 추가 수동 픽스업 합니다.

**핵심 동작:**

1. 특정 한 특성 구성 사용 하 여 개체 격리 되 고 중복 된 것과 반대로 toohello 특성으로 tooreceive 내보내기 오류를 계속 합니다.  
   예:
   
    a. 새로운 사용자가 **Joe@contoso.com**의 UPN과 ProxyAddress **smtp:Joe@contoso.com**로 AD에서 만들어집니다.
   
    b. hello이 개체의 속성 충돌할 ProxyAddress 인 기존 그룹  **SMTP:Joe@contoso.com** 합니다.
   
    c. 을 내보낼 때는 **/ / ProxyAddress 충돌** hello 충돌 특성 격리 하지 않고 오류가 throw 됩니다. hello 복원 력 기능은 사용 하기 전에 것 처럼 각 다음 동기화 주기 시 hello 작업이 다시 시도 됩니다.
2. 두 개의 그룹이 생성 되는 경우 온-프레미스 hello로 동일 SMTP 주소, 중복 되는 표준 hello 첫 번째 시도에 실패 한 tooprovision **/ / ProxyAddress** 오류입니다. 그러나 hello 중복 값은 제대로 격리 hello 시 다음 동기화 주기.

**Office 포털 보고서**:

1. UPN 충돌 집합에서 두 개체에 대 한 hello 자세한 오류 메시지는 동일한 hello입니다. 이는 실제로 하나에만 변경된 데이터가 있는 경우 둘 모두 해당 UPN을 변경 / 격리했음을 나타냅니다.
2. UPN 충돌에 대 한 hello 자세한 오류 메시지에는 해당 UPN 변경/격리는 사용자에 대 한 잘못 된 displayName hello 보여 줍니다. 예:
   
    a. **사용자 A**는 먼저 **UPN = User@contoso.com**과 동기화합니다.
   
    b. **사용자 B** 가 된 다음 동기화 시도 toobe **UPN = User@contoso.com** 합니다.
   
    c. **사용자 B의** UPN 너무 변경 **User1234@contoso.onmicrosoft.com**  및  **User@contoso.com**  너무 추가**DirSyncProvisioningErrors**합니다.
   
    d. hello 오류 메시지에 대 한 **사용자 B** 나타나야 합니다 **사용자 A** 이미  **User@contoso.com**  UPN을 하지만 보듯이 **사용자 B의** 자체 표시 이름입니다.

**ID 동기화 오류 보고서**:

에 대 한 hello 링크 *방법과 관련 된 단계 tooresolve이이 문제* 올바르지 않습니다.  
    ![활성 사용자](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "활성 사용자")  

너무 가리켜야[https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency)합니다.

## <a name="see-also"></a>참고 항목
* [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
* [Office 365에서 디렉터리 동기화 오류 확인](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)


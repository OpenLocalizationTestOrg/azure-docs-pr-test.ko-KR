---
title: "Active Directory 그룹 기반의 라이선스 추가 시나리오 aaaAzure | Microsoft Docs"
description: "Azure Active Directory 그룹 기반 라이선스의 추가 시나리오"
services: active-directory
keywords: "Azure AD 라이선스"
documentationcenter: 
author: curtand
manager: femila
editor: piotrci
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/02/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 782b7c9aa1c062a55c1241d69af673466f7a849c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-limitations-and-known-issues-using-groups-toomanage-licensing-in-azure-active-directory"></a>시나리오, 제한 사항 및 Azure Active Directory에서 그룹 toomanage 라이선스 사용 시 알려진된 문제

Azure Active Directory (Azure AD) 그룹 기반의 라이선스에 대 한 자세한 내용 및 예제 toogain 다음 hello를 사용 합니다.

## <a name="usage-location"></a>사용 위치

일부 Microsoft 서비스는 모든 위치에서 사용할 수 없습니다. 관리자에 게는 toospecify hello tooa 사용자 라이선스를 할당할 수 있습니다, 전에 **사용 위치** hello 사용자 속성입니다. [Azure 포털 hello](https://portal.azure.com)에 지정할 수 있습니다 **사용자** &gt; **프로필** &gt; **설정을**합니다.

그룹 라이선스 할당에 대 한 사용 위치를 지정 하지 않고 모든 사용자는 hello 디렉터리의 hello 위치를 상속 합니다. 사용자가 여러 위치에 있는 경우 다음 사항을 있는지 tooreflect 제대로 사용자 개체에 라이선스를 갖고 있는 사용자가 toogroups 추가 하기 전에.

> [!NOTE]
> 그룹 라이선스 할당이 이루어져도 사용자에 대한 기존 사용 위치는 수정되지 않습니다. 항상 설정 하 사용 위치 사용자 만들기 흐름의 일환으로 라이선스 할당의 hello 결과 올바른지 항상, 그리고 사용자가 되지 않은 위치에서 서비스를 받지 않음 방법을 사용 하면 (예를 들어 통해 AAD Connect 구성)-Azure ad에서는 것이 좋습니다. 사용할 수 있습니다.

## <a name="use-group-based-licensing-with-dynamic-groups"></a>동적 그룹에서 그룹 기반 라이선스 사용

모든 보안 그룹에서 그룹 기반 라이선스를 사용할 수 있으며, 이는 Azure AD 동적 그룹과 결합할 수 있음을 의미합니다. 추가 하 고 그룹에서 사용자를 제거 하는 사용자 개체 특성 tooautomatically에 대 한 규칙을 실행 하는 동적 그룹.

동적 그룹을 만들 수는 예를 들어 원하는 tooassign toousers 일부 제품에 대 한 합니다. 각 그룹은 해당 특성으로 사용자를 추가 합니다. 규칙에 의해 채워집니다 하 고 각 그룹을 원하는 tooreceive hello 할당 된 라이선스 수는 있습니다. Hello 특성 온-프레미스를 할당할 수 있으며 Azure AD와 동기화 하거나 hello 클라우드에서 직접 hello 특성을 관리할 수 있습니다.

라이선스는 toohello 그룹 추가 된 후에 곧 toohello 사용자를 할당 됩니다. Hello 특성이 변경 되 면 hello 사용자가 hello 그룹 및 hello 라이선스를 제거 합니다.

### <a name="example"></a>예제

어떤 사용자가 액세스 tooMicrosoft 웹 서비스 있어야 결정 하는 온-프레미스 id 관리 솔루션의 hello 예제를 참조 하세요. 사용 하 여 **extensionAttribute1** toostore 문자열 hello 사용자 있어야 hello 라이선스를 나타내는 값입니다. Azure AD Connect는 이 값을 Azure AD와 동기화합니다.

사용자에 따라 라이선스 중 하나만 필요하거나 두 라이선스가 모두 필요할 수 있습니다. 예를 들어 배포할 Office 365 Enterprise e 5 및 Enterprise Mobility + 보안 (EMS) 라이선스 그룹에 toousers 다음과 같습니다.

#### <a name="office-365-enterprise-e5-base-services"></a>Office 365 Enterprise E5: 기본 서비스

![Office 365 Enterprise E5 기본 서비스의 스크린샷](media/active-directory-licensing-group-advanced/o365-e5-base-services.png)

#### <a name="enterprise-mobility--security-licensed-users"></a>Enterprise Mobility + Security: 허가된 사용자

![Enterprise Mobility + Security 허가된 사용자의 스크린샷](media/active-directory-licensing-group-advanced/o365-e5-licensed-users.png)

이 예에서 한 명의 사용자를 수정 하 고의 extensionAttribute1 toohello 값이 설정 `EMS;E5_baseservices;` hello 사용자 toohave 두 라이선스를 선택 합니다. 이 수정 작업은 온-프레미스에서 수행할 수 있습니다. Hello 후 hello 클라우드와 동기화를 변경 하 고 hello 사용자 tooboth 그룹을 자동으로 추가 됩니다 라이선스가 할당 된 합니다.

![Tooset 사용자의 extensionAttribute1 hello 하는 방법을 보여 주는 스크린샷](media/active-directory-licensing-group-advanced/user-set-extensionAttribute1.png)

> [!WARNING]
> 기존 그룹의 멤버 자격 규칙을 수정할 때는 주의해야 합니다. 변경 되는 규칙, hello 그룹의 구성원 hello 다시 확인 됩니다. 및 더 이상 일치 하는 사용자가 새 hello 규칙 제거 됩니다 (여전히 hello 새 규칙을 일치 하는 사용자가 영향을 받지이 프로세스 중). 이러한 사용자 프로세스 동안 제거 hello 서비스 중단 또는 일부 경우에 발생할 수 있습니다. 데이터가 손실 될 라이선스를 포함 됩니다.

> 라이선스 할당에 종속 큰 동적 그룹이 있는 경우 더 작은 테스트 그룹의 모든 주요 변경 내용이 toohello 주 그룹에 적용 하기 전에 유효성을 검사 하는 것이 좋습니다.

## <a name="multiple-groups-and-multiple-licenses"></a>여러 그룹 및 여러 라이선스

사용자는 라이선스를 가진 여러 그룹의 구성원이 될 수 있습니다. 다음은 일부의 tooconsider가입니다.

- 여러 라이선스의 hello 동일한 제품 겹칠 수 있으며 결과 대 한 모든 설정 적용된 toohello 사용자 되 고 서비스. hello 다음 예제에서는 두 개의 라이선스 그룹: *E3 기준 서비스* hello foundation 서비스 toodeploy 먼저 tooall 사용자를 포함 합니다. 및 *서비스 확장 E3* 추가 서비스 (영향 및 플래너) toodeploy toosome 사용자만 포함 합니다. 이 예제에서는 hello 사용자 tooboth 그룹 추가 되었습니다.

  ![사용하도록 설정된 서비스의 스크린샷](media/active-directory-licensing-group-advanced/view-enabled-services.png)

  결과적으로, hello 사용자가이 제품에 대 한 하나의 라이선스를 사용 하는 동안 사용 하도록 설정 하는 hello 제품에 hello 12 서비스의 7.

- 선택 hello *E3* 라이선스 그룹의 어떤 서비스 toobe hello 사용자에 대해 활성화 발생에 대 한 정보를 포함 하 여 자세한 정보를 보여 줍니다.

  ![그룹별로 사용하도록 설정된 서비스의 스크린샷](media/active-directory-licensing-group-advanced/view-enabled-service-by-group.png)

## <a name="direct-licenses-coexist-with-group-licenses"></a>그룹 라이선스와 공존하는 직접 라이선스

라이선스 그룹에서 상속 하는 사용자를 직접 제거 하거나 수 hello 사용자의 속성에서 해당 라이선스 할당을 수정 합니다. 변경 내용을 hello 그룹에서 수행 해야 하 고 tooall 사용자가 전파 합니다.

그러나 수, 추가 toohello에서 toohello 사용자 라이선스를 상속 하는 직접 tooassign 동일한 제품 라이선스 hello 합니다. 다른 사용자에 게 영향을 주지 않고 한 명의 사용자에 대 한 hello 제품에서 추가 서비스를 사용할 수 있습니다.

직접 할당된 라이선스를 제거하더라도 상속된 라이선스에는 영향을 주지 않습니다. Hello 사용자를 게 Office 365 Enterprise E3 라이선스 그룹에서 상속 되는 것이 좋습니다.

1. Hello 사용자 hello 에서만에서 hello 라이선스를 상속 하는 처음에 *E3 기본 서비스* 와 같이 4 개의 서비스 계획을 수 있는 그룹:

  ![E3 그룹에서 사용하도록 설정된 서비스의 스크린샷](media/active-directory-licensing-group-advanced/e3-group-enabled-services.png)

2. 선택할 수 있습니다 **할당** toodirectly E3 라이선스 toohello 사용자를 할당 합니다. 이 경우 보아야 toodisable Yammer 엔터프라이즈를 제외한 모든 서비스 계획:

  ![방법 스크린샷 tooassign 라이선스 직접 tooa 사용자](media/active-directory-licensing-group-advanced/assign-license-to-user.png)

3. 결과적으로, hello 사용자는 여전히 hello E3 제품의 라이선스를 하나만 사용합니다. 하지만 hello 직접 할당 hello만 해당 사용자에 대 한 엔터프라이즈 Yammer 서비스를 사용 하도록 설정 합니다. Hello에 직접 할당할와 hello 그룹 구성원 자격으로 사용 되는 서비스를 확인할 수 있습니다.

  ![상속된 할당 대 직접 할당의 스크린샷](media/active-directory-licensing-group-advanced/direct-vs-inherited-assignment.png)

4. 직접 할당을 사용 하는 경우 작업을 수행 하는 hello 허용 됩니다.

  - Yammer 엔터프라이즈 해제할 수 있습니다 hello 사용자 개체에 직접 합니다. hello **켜기/끄기** 토글 hello 그림에서이 서비스에 대해 다른 것과 반대로 toohello로 설정할 서비스 설정/해제 합니다. Hello 서비스를 hello 사용자에서 직접 사용 하기 때문에 수정할 수 있습니다.
  - 추가 서비스 직접 라이선스를 할당 하는 hello의 일부분으로도 사용할 수 있습니다.
  - hello **제거** hello 사용자에서 사용 되는 tooremove hello 직접 라이선스를 사용할 수 있는 단추입니다. Hello 이제 사용자만는 hello 상속된 그룹 라이선스 및 hello 원래 서비스로 사용 하도록 유지를 확인할 수 있습니다.

    ![Tooremove 할당 지시 하는 방법을 보여 주는 스크린샷](media/active-directory-licensing-group-advanced/remove-direct-license.png)

## <a name="managing-new-services-added-tooproducts"></a>Tooproducts 추가 된 새 서비스 관리
새 서비스 tooa 제품을 추가 하면 Microsoft에서 할당 한 모든 그룹 toowhich 기본적으로 사용할 수 있게 hello 제품 라이선스입니다. 장애인 테 넌 트에 대 한 제품 변경에 대 한 구독된 toonotifications 미리 알리는 hello 향후 서비스 추가 대 한 메일을 받게 됩니다.

관리자로 서 hello 변경 영향을 받는 모든 그룹을 검토 하 고 hello 각 그룹에 새 서비스를 해제 하는 등의 작업을 수행할 수 있습니다. 예를 들어 특정 서비스만 배포할 그룹을 만든 경우 해당 그룹을 다시 방문하여 새로 추가된 서비스가 사용하지 않도록 설정되었는지 확인할 수 있습니다.

이 프로세스가 진행되는 과정의 예는 다음과 같습니다.

1. Hello, 원래 할당 된 *Office 365 Enterprise e 5* 제품 tooseveral 그룹입니다. 호출 이러한 그룹 중 하나 *O365 E5-Exchange만* 가 디자인 된 tooenable만 hello *Exchange Online 계획 2 개* 해당 멤버에 대 한 서비스입니다.

2. Hello e 5를 새 서비스-와 제품 확장 되도록 하는 Microsoft에서 알림을 받은 *Microsoft 스트림*합니다. Hello 서비스 테 넌 트 사용 가능 해지면 할 수 있는 hello 다음:

3. Toohello 이동 [ **Azure Active Directory > 라이선스 > 모든 제품** ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) 블레이드에 대 한 선택 *Office 365 Enterprise e 5*을 선택한 후 **사용이 허가 된 그룹**  tooview 해당 제품 인 모든 그룹의 목록입니다.

4. 클릭 하 여 원하는 tooreview hello 그룹에 (이 경우 *O365 E5-Exchange만*). Hello 열립니다 **라이선스** 탭 합니다. Hello E5 라이선스에 클릭 하면 사용된 하는 모든 서비스를 나열 하는 블레이드가 열립니다.
> [!NOTE]
> hello *Microsoft 스트림* 서비스에 자동으로 추가 되 고 추가 toohello에서이 그룹에서 사용 하도록 설정 *Exchange Online* 서비스:

  ![새 서비스의 스크린 샷 추가 tooa 그룹 라이선스](media/active-directory-licensing-group-advanced/manage-new-services.png)

5. 이 그룹의 toodisable hello 새로운 서비스 hello를 클릭 합니다 **켜기/끄기** hello를 누른 다음 toohello 서비스를 설정/해제 **저장** tooconfirm hello 변경 단추입니다. Azure AD는 이제 hello 그룹 tooapply hello 변경;의 모든 사용자를 처리 새 사용자 추가 toohello 그룹 hello 체계가 없습니다 *Microsoft 스트림* 서비스를 사용 합니다.

  > [!NOTE]
  > 사용자가 hello 서비스가 몇 가지 다른 라이선스 할당 (다른 그룹의 구성원 인지 직접 라이선스 할당)을 통해 활성화 되어 있을 수 있습니다.

6. 필요한 경우 hello 할당 된 다른 그룹이 제품에 대해 동일한 단계를 수행 합니다.

## <a name="use-powershell-toosee-who-has-inherited-and-direct-licenses"></a>PowerShell toosee 상속한 사용자를 사용 하 고 라이선스를 직접
사용자는 라이선스가 직접 할당 하거나 그룹에서 상속 하는 경우 PowerShell 스크립트 toocheck를 사용할 수 있습니다.

1. Hello 실행 `connect-msolservice` cmdlet tooauthenticate tooyour 테 넌 트를 연결 합니다.

2. `Get-MsolAccountSku`사용 되는 toodiscover hello 테 넌 트의 모든 프로 비전 된 제품 라이선스를 수 있습니다.

  ![Get-msolaccountsku hello cmdlet의 스크린샷](media/active-directory-licensing-group-advanced/get-msolaccountsku-cmdlet.png)

3. 사용 하 여 hello *AccountSkuId* 사용 하 여 관심 있는 hello 라이선스에 대 한 값 [이 PowerShell 스크립트](./active-directory-licensing-ps-examples.md#check-if-user-license-is-assigned-directly-or-inherited-from-a-group)합니다. Hello에 대 한 정보는 어떻게 hello 라이선스가 할당 되지 라이선스가이 사용자의 목록을 생성 됩니다.

## <a name="use-audit-logs-toomonitor-group-based-licensing-activity"></a>감사 로그 toomonitor 그룹 기반의 라이선스는 작업을 사용 하 여

사용할 수 있습니다 [Azure AD 감사 로그](./active-directory-reporting-activity-audit-logs.md#audit-logs) toosee 모든 활동 관련 toogroup 기반 라이선스를 포함 하 여:
- 그룹에 대한 라이선스를 변경한 사용자
- hello 시스템 그룹 라이선스 변경 처리를 시작 및 종료 시간과
- 그룹 라이선스 할당의 결과로 tooa 사용자 라이선스 변경 된 합니다.

>[!NOTE]
> 감사 로그 대부분 블레이드 hello hello 포털의 Azure Active Directory 섹션에 나와 있습니다. 위치에 액세스에 따라 필터 hello 블레이드의 미리 적용 된 tooonly 표시 작업 관련 toohello 컨텍스트 수 있습니다. 원하는 hello 결과 표시 되지 않는 경우에 검토 [필터링 옵션 hello](./active-directory-reporting-activity-audit-logs.md#filtering-audit-logs) 에서 필터링 되지 않은 hello 감사 로그를 볼 또는 [ **Azure Active Directory > 활동 > 감사 로그** ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Audit).

### <a name="find-out-who-modified-a-group-license"></a>라이선스 그룹을 수정한 사용자 확인

1. 집합 hello **활동** 너무 필터링*집합 그룹 라이선스* 클릭 **적용**합니다.
2. hello 결과 설정 또는 그룹에서 수정 될 라이선스의 모든 사례를 포함 합니다.
>[!TIP]
> Hello에 hello 그룹의 hello 이름을 입력할 수도 있습니다 *대상* tooscope hello 결과 필터링 합니다.

3. 변경 내용 hello 목록 toosee hello 정보 보기에서에서 항목을 클릭 합니다. 아래 *속성 수정* hello 라이선스 할당에 대 한 기존 패턴과 새 값이 나열 됩니다.

세부 정보를 포함한 최근 그룹 라이선스 변경의 예는 다음과 같습니다.

![스크린샷 그룹 라이선스 변경](media/active-directory-licensing-group-advanced/audit-group-license-change.png)

### <a name="find-out-when-group-changes-started-and-finished-processing"></a>그룹 변경이 처리를 시작하고 완료한 시점 확인

라이선스 그룹에 변경 되 면 Azure AD는 hello 변경 tooall 사용자 적용 시작 됩니다.

1. toosee 그룹 처리를 시작할 때 hello 설정 **활동** 너무 필터링*기반 그룹 라이선스 toousers 적용을 시작할*합니다. Hello 작업은 해당 hello 배우 참고 *Microsoft Azure AD 그룹 기반의 라이선스* -는 시스템 계정의 tooexecute 사용 되는 모든 그룹 라이선스 변경 됩니다.
>[!TIP]
> Hello 목록 toosee hello에서 항목을 클릭 *속성 수정* 필드-처리에 대해 선택 된 hello 라이선스 변경 내용을 표시 합니다. 여러 변경 내용 tooa 그룹 항목과 어떤 것으로 처리 된 확실 하지 않은 경우에 유용 합니다.

2. 그룹을 사용 하 여 hello 필터 값의 처리를 완료 하는 경우 마찬가지로, toosee *다 기반 그룹 라이선스 toousers 적용*합니다.
>[!TIP]
> 이 경우 hello *속성 수정* hello 결과의 요약을 포함 하는 필드-처리 된 오류가 발생 하는 경우 이것은 유용한 tooquickly 확인 합니다. 샘플 출력:
> ```
Modified Properties
...
Name : Result
Old Value : []
New Value : [Users successfully assigned licenses: 6, Users for whom license assignment failed: 0.];
> ```

3. hello toosee 방법 그룹, 처리 된 모든 사용자의 변경 내용을 포함 하 여에 대 한 전체 로그 hello 다음 필터를 설정 합니다.
  - **(작업자)에 의해 시작**: "Microsoft Azure AD 그룹 기반 라이선스"
  - **날짜 범위**(선택 사항): 특정 그룹이 처리를 시작 및 완료하는 시점을 알고 있는 경우에 범위를 사용자 지정합니다.

이 샘플 출력 처리의 완료 하는 사용자의 변경 내용 및 hello 모두 결과 처리의 시작 부분 hello를 보여 줍니다.

![스크린샷 그룹 라이선스 변경](media/active-directory-licensing-group-advanced/audit-group-processing-log.png)

>[!TIP]
> 너무 관련 항목을 클릭 하면*사용자 라이선스 변경* 라이선스 적용 된 변경 내용 tooeach 개별 사용자에 대 한 세부 정보가 표시 됩니다.

## <a name="limitations-and-known-issues"></a>제한 사항 및 알려진 문제

그룹 기반 라이선스를 사용 하는 것이 좋습니다 toofamiliarize 직접 hello 제한 사항 및 알려진된 문제 목록은 다음.

- 그룹 기반 라이선스는 현재 다른 그룹을 포함하는 그룹(중첩된 그룹)을 지원하지 않습니다. 라이선스 tooa 중첩 된 그룹에 적용 하면 hello 즉각적인 첫 번째 수준의 사용자 그룹 구성원만 hello 적용 하는 hello 라이선스를 보유 합니다.

- hello 기능 보안 그룹과 사용할 수 있습니다. Office 그룹은 현재 지원 되지 않으며 수 toouse 됩니다 hello 라이선스 할당 프로세스에서 해당 합니다.

- hello [Office 365 관리 포털](https://portal.office.com ) 그룹 기반의 라이선스 현재 지원 하지 않습니다. 라이선스 그룹에서 상속 하는 사용자를이 라이선스 hello Office 관리 포털에는 일반 사용자 라이선스도 나타납니다. 라이선스 또는 tooremove hello 라이선스를 시도 하는 toomodify 시도 하면 hello 포털 오류 메시지를 반환 합니다. 상속된 그룹 라이선스는 사용자가 직접 수정할 수 없습니다.

- 사용자 그룹에서 제거 hello 라이선스를 잃을 때 해당 라이선스 (예를 들어 SharePoint Online)에서 서비스 계획을 hello tooa 설정 **Suspended** 상태입니다. hello 서비스 계획을 설정 하지 않은 tooa 최종, 사용 안 함 상태입니다. 이 예방 조치를 통해 관리자가 그룹 멤버 자격 관리에서 실수하는 경우 사용자 데이터를 실수로 제거하지 않도록 방지할 수 있습니다.

- 대규모 그룹(예: 100,000명의 사용자)에 대해 라이선스를 할당하거나 수정하면 성능에 영향을 줄 수 있습니다. 특히, Azure AD 자동화에 의해 생성 된 변경 내용의 hello 볼륨 부정적인 성능에 영향을 hello Azure AD 간의 디렉터리 동기화의 및 온-프레미스 시스템.

- 라이선스 관리 자동화 tooall 유형의 hello 환경에서 변경 내용 자동으로 반응 하지 않습니다. 예를 들어 있는 부족 해질 수 있습니다 라이선스를 일부 사용자가 toobe 오류 상태에 발생 합니다. hello 사용 가능한 사용자 수를 toofree, 다른 사용자의 일부 직접 할당 된 라이선스를 제거할 수 있습니다. 그러나 hello 시스템에 자동으로 toothis 변경 대응 하며 해당 오류 상태에서 사용자가 수정 합니다.

  제한 사항 해결 방법 toothese 형식으로 toohello 이동할 수 있습니다 **그룹** 블레이드 Azure AD에서 클릭 하 고 **다시 처리**합니다. 이 명령은 해당 그룹의 모든 사용자를 처리 하 고 가능한 경우 hello 오류 상태를 확인 합니다.

- 그룹 기반 라이선스를 기록 하지 않습니다 오류 라이선스를 할당할 수 없습니다 Exchange Online;에서 중복 된 프록시 주소 구성 tooa 인해 tooa 사용자 때 이러한 사용자 라이선스 할당 중에 건너뜁니다. 방법에 대 한 자세한 내용은 tooidentify이이 문제를 해결 하 고, 참조 [이 여기서](./active-directory-licensing-group-problem-resolution-azure-portal.md#license-assignment-fails-silently-for-a-user-due-to-duplicate-proxy-addresses-in-exchange-online)합니다.

## <a name="next-steps"></a>다음 단계

toolearn 그룹 기반의 라이선스를 통해 라이선스가 관리에 대 한 다른 시나리오에 대 한 참조.

* [Azure Active Directory의 그룹 기반 라이선스란?](active-directory-licensing-whatis-azure-portal.md)
* [Azure Active Directory에서 tooa 그룹 라이선스 할당](active-directory-licensing-group-assignment-azure-portal.md)
* [Azure Active Directory에서 그룹에 대한 라이선스 문제 식별 및 해결](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Toomigrate 개별 toogroup 기반 라이선스 Azure Active Directory에서 사용자가 사용이 허가 된 방법](active-directory-licensing-group-migration-azure-portal.md)

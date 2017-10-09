---
title: "aaaWhat azure 셀프서비스 등록 이란? | Microsoft Docs"
description: "Azure에 대 한 개요 셀프 서비스 등록 하 고 toomanage hello 등록 프로세스를 방법 DNS 도메인 이름을 통해 tootake 합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: b9f01876-29d1-4ab8-8b74-04d43d532f4b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: dbf3b59e3807e98f7bf39f3d5591fcde01667323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-self-service-signup-for-azure"></a>Azure의 셀프 서비스 등록이란?
이 항목에서는 hello 셀프 서비스 등록 과정을 설명 합니다. 어떻게 하 고 DNS 도메인 이름을 통해 tootake 합니다.  

## <a name="why-use-self-service-signup"></a>셀프 서비스 등록을 사용하는 이유
* Get 고객 tooservices 더 빠르게 원합니다.
* 서비스에 대한 메일 기반 제공 사항을 만듭니다.
* 신속 하 게 사용자가 기억 하기 쉬운 작업 전자 메일 별칭을 사용 하 여 toocreate id 수 있는 전자 메일 기반 등록 흐름을 만듭니다.
* 관리되지 않는 Azure 디렉터리를 나중에 관리되는 디렉터리에 만들 수 있으며 다른 서비스에 다시 사용할 수 있습니다.

## <a name="terms-and-definitions"></a>용어 및 정의
* **셀프 서비스 등록**:이 사용자가 클라우드 서비스에 등록 하 고 해당 전자 메일 도메인에 따라 Azure Active Directory (Azure AD)에 자동으로 생성 하는 id 수 있는 hello 방법입니다.
* **관리 되지 않는 Azure directory**: hello 디렉터리를 해당 id를 만들 위치입니다. 관리되지 않는 디렉터리는 전역 관리자가 없는 디렉터리입니다.
* **메일로 확인된 사용자**: Azure AD의 사용자 계정의 한 유형입니다. 셀프 서비스 제공 사항에 등록한 후 자동으로 생성된 ID를 갖는 사용자를 메일로 확인된 사용자라고 합니다. 메일로 확인된 사용자는 creationmethod=EmailVerified로 태그가 지정된 디렉터리의 일반 멤버입니다.

## <a name="user-experience"></a>사용자 환경
예를 들어 있는 메일이 Dan@BellowsCollege.com 인 사용자가 메일을 통해 중요한 파일을 받는다고 가정해 보겠습니다. Azure 권한 관리 (Azure RMS)로 보호 된 hello 파일입니다. 하지만 Dan의 조직인 Bellows College는 Azure RMS에 등록하지 않았으며 Active Directory RMS도 배포하지 않았습니다. 이 경우 Dan 등록할 수는 무료 구독 tooRMS 개인 순서 tooread hello 보호 된 파일에 대 한 합니다.

Dan hello 첫 번째 사용자 제공이 셀프 서비스에 대해 BellowsCollege.com toosign에서 전자 메일 주소가 있는 경우 다음 관리 되지 않는 디렉터리 만들어질 수 BellowsCollege.com에 대 한 Azure AD에 있습니다. 관리 되지 않는 동일한 hello에서 만들어진 전자 메일 확인 사용자 계정은 해야만 합니다 hello BellowsCollege.com 도메인의 다른 사용자가이 제공 또는 유사한 셀프 서비스 제공에 등록 하는 경우 Azure에서 디렉터리입니다.

## <a name="admin-experience"></a>관리자 환경
관리 되지 않는 Azure 디렉터리의 hello DNS 도메인 이름을 소유 하 고 관리 인계 하거나 소유권을 증명 후 hello 디렉터리에 병합 수 있습니다. hello 다음 섹션에서는 더 자세하게에서 hello 관리자 환경에 설명 하지만 다음과 같습니다.

* 관리 되지 않는 Azure 디렉터리를 인수할 때 hello 관리 되지 않는 디렉터리의 전역 관리자에 게 하기만 하면 됩니다. 이를 내부 인수라고도 합니다.
* 관리 되지 않는 Azure 디렉터리를 병합 하 고 hello 관리 되지 않는 디렉터리 tooyour 관리 되는 Azure 디렉터리의 hello DNS 도메인 이름을 추가 하면 사용자-리소스의 매핑이 만들어집니다 하므로 tooaccess 서비스 중단 없이 사용자가 계속 수 있습니다. 이를 외부 인수라고도 합니다.

## <a name="what-gets-created-in-azure-active-directory"></a>Azure Active Directory에 생성되는 것은 무엇인가요?
#### <a name="directory"></a>디렉터리
* Hello 도메인에 대 한 Azure Active Directory 디렉터리를 만들어지면 도메인당 한 디렉터리입니다.
* hello Azure AD 디렉터리에 없는 전역 관리자

#### <a name="users"></a>사용자
* 각 사용자가 등록에 대해 사용자 개체에 hello Azure AD 디렉터리에 만들어집니다.
* 각 사용자 개체는 외부로 표시됩니다.
* 각 사용자에 등록 하는 액세스 toohello 서비스를 제공 됩니다.

### <a name="how-do-i-claim-a-self-service-azure-ad-directory-for-a-domain-i-own"></a>소유한 도메인에 대한 셀프 서비스 Azure AD 디렉터리를 어떻게 요구하나요?
도메인 유효성 검사를 수행하여 셀프 서비스 Azure AD 디렉터리를 요구할 수 있습니다. 도메인 유효성 검사 DNS 레코드를 만들어 직접 hello 도메인을 증명 합니다.

두 가지 방법으로 toodo Azure AD 디렉터리의 DNS 인수 가지가 있습니다.

* 내부 인수 (관리자는 관리 되지 않는 Azure 디렉터리를 검색 하는 관리 되는 디렉터리로 tooturn가)
* 외부 인수 (Admin tooadd 새 도메인 tootheir 관리 되는 Azure 디렉터리를 시도 하는 데 사용)

사용자 셀프 서비스 등록을 수행 하거나 새 도메인 tooan 기존의 관리 되는 디렉터리를 추가할 수 있습니다는 관리 되지 않는 디렉터리를 통해 수행한 때문에 도메인을 소유 하는 유효성 검사에 관심을 가질 수 있습니다. 예를 들어 contoso.com 이라는 도메인이 고 tooadd contoso.co.uk 또는 contoso.uk 이라는 이름의 새 도메인을 원하는 합니다.

## <a name="what-is-domain-takeover"></a>도메인 인수란?
이 섹션에서는 어떻게 toovalidate 도메인을 소유

### <a name="what-is-domain-validation-and-why-is-it-used"></a>도메인 유효성 검사란 무엇이며 사용해야 하는 이유는?
순서 tooperform 작업 디렉터리에 Azure AD는 hello DNS 도메인의 소유권을 확인 하는 필요 합니다.  Hello 도메인의 유효성 검사에 tooclaim hello 디렉터리와 하거나 승격 hello 셀프 서비스 디렉터리 tooa 관리 되는 디렉터리 또는 디렉터리를 관리 하는 hello 셀프 서비스를 기존 디렉터리 병합 수 있습니다.

## <a name="examples-of-domain-validation"></a>도메인 유효성 검사 예
두 가지 방법으로 toodo 디렉터리의 DNS 구성

* 내부 인수 (예를 들어 관리자 셀프 서비스, 관리 되지 않는 디렉터리를 검색 및 관리 되는 디렉터리에 tooturn 원하는)
* 외부 인수 (예를 들어 관리자가 시도 tooadd 새 도메인 tooa 관리 되는 디렉터리)

### <a name="internal-takeover---promote-a-self-service-unmanaged-directory-toobe-a-managed-directory"></a>내부 인수-셀프 서비스, 관리 되지 않는 디렉터리 toobe 관리 되는 디렉터리를 승격 합니다.
내부 구성 작업을 수행할 때 hello 디렉터리 관리 되지 않는 디렉터리 tooa 관리 되는 디렉터리에서 변환 합니다. Toocomplete DNS 도메인 이름 유효성 검사, TXT 레코드 또는 MX 레코드에에서 만드는 hello DNS 영역이 필요 합니다. DNS 영역에 MX 레코드 또는 TXT 레코드를 만드는 경우 다음을 수행합니다.

* Hello 도메인의 소유를 확인 합니다.
* 관리 되는 hello 디렉터리를 사용 하면
* Hello 디렉터리의 전역 관리자 hello 만듭니다

로즈 이동 대학에서 IT 관리자 검색 hello 학교에서 사용자가 셀프 서비스 제공에 대 한 등록 한 경우를 가정해 봅니다. Hello 등록 hello DNS의 소유자 이름을 BellowsCollege.com, hello IT 관리자는 Azure의 hello DNS 이름의 소유권을 확인 하 고 hello 관리 되지 않는 디렉터리 조치를 취할 수 있습니다. hello 디렉터리 다음 되는 관리 되는 디렉터리 및 hello IT 관리자는 hello 전역 관리자 역할이 할당 hello BellowsCollege.com 디렉터리에 대 한 합니다.

### <a name="external-takeover---merge-a-self-service-directory-into-an-existing-managed-directory"></a>외부 인수 - 셀프 서비스 디렉터리를 관리되는 기존 디렉터리에 병합
외부 프로그램 구성에서 이미 관리 되는 디렉터리 및 모든 사용자 및 그룹 디렉터리를 관리 하는 관리 되지 않는 디렉터리 toojoin에서 원하는 대신 자체 두 디렉터리를 구분 합니다.

관리 되는 디렉터리의 관리자의 경우 도메인을 추가 하 고 연결 된 디렉터리를 관리 되지 않는 toohave 발생 하는 해당 도메인.

예를 들어는 IT 관리자가 이미 등록 된 tooyour 조직 된 도메인 이름 Contoso.com에 대 한 관리 되는 디렉터리를 사용할 가정해 봅니다. 조직의 사용자가 조직이 소유하는 또 다른 도메인 이름인 전자 메일 도메인 이름 user@contoso.co.uk를 사용하여 제품에 대한 셀프 서비스 등록을 수행한 것을 발견합니다. 이 사용자는 현재 contoso.co.uk의 관리되지 않는 디렉터리에 계정이 있습니다.

Contoso.com에 대 한 기존 IT 관리 디렉터리에 hello contoso.co.uk에 대 한 관리 되지 않는 디렉터리를 병합 되므로 두 개의 별도 디렉터리 toomanage 않으려는 합니다.

외부 감염 다음과 같은 DNS 유효성 검사 프로세스 내부 인수 hello 합니다.  차이점은 기간: 사용자 및 서비스를 다시 매핑된 toohello IT 관리 되는 디렉터리입니다.

#### <a name="whats-hello-impact-of-performing-an-external-takeover"></a>외부 인수 수행의 hello 영향 이란?
외부 인수, 사용자가 tooaccess 서비스 중단 없이 계속 수 있도록 사용자-리소스의 매핑을 만들어집니다. 사용자가 계속 tooaccess 변경 없이 이러한 서비스 및 개인별 RMS를 포함 하 여 대부분의 응용 프로그램, 사용자-리소스의 hello 매핑을 처리 합니다. 응용 프로그램 사용자-리소스의 hello 매핑을 효과적으로 처리 하지 않을 경우 외부 인수 만족 스러운 서비스의 사용자를 명시적으로 차단 된 tooprevent 수 있습니다.

#### <a name="directory-takeover-support-by-service"></a>디렉터리 인수 지원 서비스
현재 다음 hello 서비스 지원 인수:

* RMS

다음 서비스는 hello 곧 원하는 인수:

* PowerBI

hello 다음 안을 외부 인수 후 추가 관리 작업 toomigrate 사용자 데이터는 필요 합니다.

* SharePoint/OneDrive

## <a name="how-tooperform-a-dns-domain-name-takeover"></a>어떻게 tooperform DNS 도메인 이름 구성
방법에 대 한 몇 가지 옵션이 tooperform 도메인 유효성 검사 (및는 구성 하려는 경우 수행):

1. Azure 관리 포털

   도메인을 추가하면 인수가 트리거됩니다.  Hello 도메인에 대 한 디렉터리가 이미 경우 hello 옵션 tooperform 외부 인수입니다.

   자격 증명을 사용 하 여 Azure 포털 toohello에 로그인 합니다.  Tooyour 기존 디렉터리를 탐색 한 다음 너무**도메인 추가**합니다.
2. Office 365

   Hello에 hello 옵션을 사용할 수 [도메인 관리](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/) 도메인 및 DNS 레코드를 사용한 Office 365 toowork의 페이지입니다. [Office 365에서 도메인 확인](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/)을 참조하세요.
3. Windows PowerShell

   단계를 수행 하는 hello 필요한 tooperform Windows PowerShell을 사용 하는 유효성 검사 됩니다.

   | 단계 | Cmdlet toouse |
   | --- | --- |
   | 자격 증명 개체 만들기 |Get-Credential |
   | TooAzure AD 연결 |Connect-MsolService |
   | 도메인 목록 가져오기 |Get-MsolDomain |
   | 챌린지 만들기 |Get-MsolDomainVerificationDns |
   | DNS 레코드 만들기 |DNS 서버에서 수행 |
   | Hello 챌린지를 확인 합니다. |Confirm-MsolEmailVerifiedDomain |

예:

1. TooAzure AD 연결 사용된 toorespond toohello 셀프 서비스 제공 되었던 hello 자격 증명을 사용 하 여:

        import-module MSOnline
        $msolcred = get-credential
        connect-msolservice -credential $msolcred
2. 도메인 목록을 가져옵니다.

    Get-MsolDomain
3. 그런 다음 Get-msoldomainverificationdns cmdlet toocreate hello challenge를 실행 합니다.

    Get-MsolDomainVerificationDns –DomainName *your_domain_name* –Mode DnsTxtRecord

    예:

    Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord
4. 이 명령에서 반환 되는 hello 값 (챌린지 hello)를 복사 합니다.

    예:

    MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9
5. 공용 DNS 네임 스페이스를 hello 이전 단계에서 복사한 hello 값이 포함 된 DNS txt 레코드를 만듭니다.

    이 레코드에 대 한 hello 이름은 hello hello 부모 도메인의 이름을, 따라서 Windows Server에서 DNS 역할 hello를 사용 하 여이 리소스 레코드를 만드는 경우 hello 레코드 이름을 비워 둡니다 이며 hello 텍스트 상자에 붙여넣을 hello 값
6. Hello Confirm-msoldomain cmdlet tooverify hello 챌린지를 실행 합니다.

    Confirm-MsolEmailVerifiedDomain -DomainName *your_domain_name*

    예:

    Confirm-MsolEmailVerifiedDomain -DomainName contoso.com

챌린지가 성공적 이면 오류 없이 toohello 프롬프트를 반환합니다.

## <a name="how-do-i-control-self-service-settings"></a>셀프 서비스 설정을 제어하는 방법
관리자는 현재 두 개의 셀프 서비스 컨트롤을 보유하며 다음을 제어할 수 있습니다.

* 여부 사용자 전자 메일을 통해 hello 디렉터리에 참여할 수 있습니다.
* 응용 프로그램 및 서비스를 사용자 자신이 사용하도록 허가할 수 있는지 여부

### <a name="how-can-i-control-these-capabilities"></a>이러한 기능은 어떻게 제어할 수 있나요?
관리자는 Azure AD cmdlet인 Set-MsolCompanySettings 매개 변수를 사용하여 이러한 기능을 구성할 수 있습니다.

* **AllowEmailVerifiedUsers** 는 관리되지 않는 디렉터리를 만들거나 결합시킬 수 있는지 여부를 제어합니다. 해당 매개 변수를 설정 하는 경우 $false, 더 전자 메일 확인 사용자 hello 디렉터리 조인할 수 너무.
* **AllowAdHocSubscriptions** tooperform 셀프 서비스 등록 하는 사용자가 hello 제어 합니다. 너무 해당 매개 변수를 설정 하면 $false 이면 사용자가 수행할 수 셀프 서비스 등록 합니다.

### <a name="how-do-hello-controls-work-together"></a>어떻게 수행 hello 컨트롤 함께 작동 합니까?
이 두 매개 변수를 사용할 수 함께 toodefine에 보다 자세히 제어할 셀프 서비스 등록 합니다. 예를 들어 hello 다음 명령을 사용 하면 사용자가 tooperform 셀프 서비스 등록만 해당 사용자 계정이 이미 있는 Azure AD의 경우 (즉, 사용자에 게 생성 하는 전자 메일 확인 된 계정 toobe는 수행할 수 없습니다 셀프서비스 위로):

    Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true

hello 다음 순서도 이러한 매개 변수에 대 한 모든 hello 다른 조합 및 설명 hello 디렉터리와 셀프 서비스 등록에 대 한 hello 결과 조건입니다.

![][1]

자세한 내용 및 toouse 이러한 매개 변수를 확인 하려면 어떻게의 예제에 대 한 [Set-msolcompanysettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)합니다.

## <a name="see-also"></a>참고 항목
* [어떻게 tooinstall Azure PowerShell 및 구성](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure Cmdlet 참조](/powershell/azure/get-started-azureps)
* [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)

<!--Image references-->
[1]: ./media/active-directory-self-service-signup/SelfServiceSignUpControls.png

---
title: "사용자 지정 역할 기반 액세스 제어 역할 aaaCreate toointernal 및 외부 사용자가 Azure에서 할당 | Microsoft Docs"
description: "내부 및 외부 사용자에게 PowerShell 및 CLI를 사용하여 만든 사용자 지정 RBAC 역할 할당"
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a>역할 기반 액세스 제어 소개

역할 기반 액세스 제어 기능은 Azure 포털만 허용 구독 hello 소유자 tooassign 자신의 환경에서 특정 리소스 범위를 관리할 수 있는 상세 역할로 tooother 사용자입니다.

외부 공동 작업자, 공급 업체 또는 freelancers toospecific 환경 하지만 반드시 toohello 전체 인프라 또는 리소스 하나에 액세스 해야 하는 작업 RBAC가 Smb를 위한 대규모 조직에 대 한 보안 관리를 향상 수 있습니다. 대금 청구 관련 범위입니다. RBAC hello 관리자 계정 (구독 수준에서 서비스 관리자 역할)에 의해 관리 되는 단일 Azure 구독을 소유 hello 유연성을 허용 하 고 아래에서 여러 사용자가 초대 toowork가 동일한 구독 없이 hello 관리 에 대 한 권한입니다. 관리 및 결제 관점에서 hello RBAC 기능은 다양 한 시나리오에서 Azure를 사용 하 여에 대 한 시간 및 관리 효율성 옵션 toobe을 증명 합니다.

## <a name="prerequisites"></a>필수 조건
RBAC를 사용 하 여 hello Azure 환경에에서 필요 합니다.

* 독립 실행형 있는 Azure 구독 toohello 사용자로 할당 소유자 (구독 역할)
* Hello 소유자 역할의 hello Azure 구독
* 액세스 toohello가 [Azure 포털](https://portal.azure.com)
* 리소스 공급자에 따라 toohave hello hello 사용자 구독에 등록 되어 있는지 확인: **Microsoft.Authorization**합니다. 어떻게 tooregister hello 리소스 공급자에 대 한 자세한 내용은 참조 하십시오. [공급자 리소스 관리자, 지역, API 버전 및 스키마](/azure-resource-manager/resource-manager-supported-services.md)합니다.

> [!NOTE]
> Office 365 구독 또는 Azure Active Directory 라이선스 (예: tooAzure Active Directory에 액세스)에서 hello O365 포털 하지 품질에 대 한 RBAC를 사용 하 여 사용자를 프로 비전 합니다.

## <a name="how-can-rbac-be-used"></a>RBAC를 사용할 수 있는 방법
RBAC는 Azure에서 세 가지 각기 다른 범위에 적용할 수 있습니다. Hello 가장 높은 범위 toohello 가장 낮은 하나에서에서 것은 다음과 같습니다.

* 구독(높음)
* 리소스 그룹
* 리소스 범위 (hello 최저 액세스 수준 tooan 개별 Azure 리소스 범위 대상으로 지정 된 사용 권한을 제공)

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a>Hello 구독 범위에서 RBAC 역할 할당
RBAC가 사용되는 일반적인 두 가지 예는 다음과 같습니다(제한되지는 않음).

* 특정 리소스 또는 전체 구독 hello toomanage 초대 hello 조직 (hello 관리 사용자의 Azure Active Directory 테 넌 트의 일부가 아님)에서 외부 사용자가
* 어느 toohello 내 (의 일부인 hello 사용자의 Azure Active Directory 테 넌 트) hello 조직이 하지만 다른 팀 또는 세분화 된 액세스 해야 하는 그룹의 일부는 사용자와 작업 전체 구독 또는 toocertain 리소스 그룹 또는 리소스의 범위가 hello에 환경

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a>구독 수준에서 Azure Active Directory 외부 사용자에 대한 액세스 권한 부여
RBAC 역할에만 부여할 수 **소유자** hello 구독의 따라서 hello admin 사용자도 로그온 해야이 역할이 미리 할당 되지 않았거나가 hello Azure 구독을 만든 사용자 이름입니다.

Hello Azure 포털에서에서 한 후 로그인 관리자의 경우 선택 "구독" 및 선택한 hello 원하는 하나입니다.
![Azure 포털에서 구독 블레이드](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) 기본적으로 hello admin 사용자 hello Azure 구독을 구매한 경우 hello 사용자로 표시 됩니다 **계정 관리자**,이 hello 구독 역할 되 고 있습니다. Hello Azure 구독 역할에 대 한 자세한 내용은 참조 하십시오. [hello 구독 또는 서비스를 관리 하는 Azure 관리자 역할을 추가 또는 변경](/billing/billing-add-change-azure-subscription-administrator.md)합니다.

이 예제에서는 사용자 hello "alflanigan@outlook.com"는 hello **소유자** "무료 평가판" hello의 구독 hello AAD에서에서 테 넌 트 "Azure 테 넌 트 Default"입니다. 이 사용자는 hello 작성자 hello로 hello Azure 구독에 있으므로 초기 "Outlook" Microsoft 계정 (Microsoft 계정 = Outlook, Live 등)이 테 넌이 트에 추가 된 다른 모든 사용자에 대 한 기본 도메인 이름은 hello **"@alflaniganuoutlook.onmicrosoft.com"**. 기본적으로 hello 새 도메인의 hello 구문을 함께 hello 테 넌 트 및 추가 hello 확장 만든 hello 사용자의 hello 사용자 이름 및 도메인 이름을 입력 하 여 형식이 **". onmicrosoft.com"**합니다.
또한 사용자가에 로그인 hello 테 넌 트의 사용자 지정 도메인 이름을 추가 하 고 hello 새 테 넌 트에 대 한 확인 합니다. 에 대 한 자세한 내용은 tooverify Azure Active Directory 테 넌 트에 사용자 지정 도메인 이름을 확인 하려면 어떻게 해야 [추가 사용자 지정 도메인 이름 tooyour 디렉터리](/active-directory/active-directory-add-domain)합니다.

이 예에서 hello "기본 테 넌 트 Azure" 디렉터리는 hello 도메인 이름 가진 사용자만 포함 "@alflanigan.onmicrosoft.com"입니다.

Hello 구독을 선택한 후 hello admin 사용자가 클릭 해야 **액세스 제어 (IAM)** 차례로 **새 역할을 추가**합니다.





![Azure Portal의 액세스 제어 IAM 기능](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![Azure Portal의 액세스 제어 IAM 기능에서 새 사용자 추가](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

hello 다음 단계에 할당 된 tooselect hello 역할 toobe 및 hello RBAC 역할에 할당 될 hello 사용자입니다. Hello에 **역할** hello 기본 제공 RBAC 역할에 대해서만 Azure에서 사용할 수 있는 드롭다운 메뉴 hello 관리: 사용자에 게 표시 합니다. 각 역할 및 해당 할당 가능한 범위에 대한 자세한 설명은 [Azure 역할 기반 액세스 제어의 기본 제공 역할](/active-directory/role-based-access-built-in-roles.md)을 참조하세요.

hello 관리: 사용자에는 다음 hello 외부 사용자의 tooadd hello 전자 메일 주소가 필요합니다. hello 동작은 hello 외부 사용자 toonot에에서 표시 hello 기존 테 넌 트에 대 한 필요 합니다. 아래에 표시 것 hello 외부 사용자를 초대 후 **구독 > 액세스 제어 (IAM)** 프로그램 RBAC 역할 hello 구독 범위에 현재 할당 되어 있는 모든 hello 현재 사용자와 합니다.





![사용 권한을 toonew RBAC 역할 추가](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![구독 수준에서 RBAC 역할 목록](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

hello 사용자 "chessercarlton@gmail.com" 초대 된 toobe 되었습니다는 **소유자** hello "무료 평가판" 구독에 대 한 합니다. Hello 외부 사용자는 hello 초대를 보낸 후 활성화 링크를 전자 메일 확인을 받게 됩니다.
![RBAC 역할에 대한 이메일 초대](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)

조직 외부 toohello 되 고, hello 새 사용자가 없습니다 모든 기존 특성 hello "기본 Azure 테 넌 트" 디렉터리에 있습니다. Hello 외부 사용자가 부여한 동의 toobe 역할을 지정한 그 hello 구독과 연결 된 hello 디렉토리에 기록 된 후 생성 됩니다.





![RBAC 역할에 대한 이메일 초대 메시지](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

hello 외부 사용자의 외부 사용자로 Azure Active Directory 테 넌 트 hello에 표시 되 고 Azure 포털 hello와 hello 클래식 포털에서 볼 수 있습니다.





![사용자 블레이드 Azure Active Directory Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![사용자 블레이드 Azure Active Directory Azure 클래식 포털](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

Hello에 **사용자** 보기 두 포털 hello 외부 사용자에 의해 인식 될 수 있습니다.

* hello Azure 포털에서에서 다른 아이콘 유형을 hello
* hello 클래식 포털에서 지점 소싱 다른 hello

그러나 부여 **소유자** 또는 **참가자** hello에 대 한 액세스 tooan 외부 사용자 **구독** 범위, hello 액세스 toohello admin 사용자 디렉터리를 허용 하지 않습니다 하지 않는 한 hello **전역 관리자** 허용 합니다. Hello 사용자 속성에서 hello **사용자 유형** 두 개의 공통 매개 변수 있는 **멤버** 및 **게스트** 식별할 수 있습니다. 멤버는 게스트는 외부 원본에서 사용자를 초대 toohello 디렉터리 동안 hello 디렉터리에 등록 되어 있는 사용자입니다. 자세한 내용은 [Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법](/active-directory/active-directory-b2b-admin-add-users)을 참조하세요.

> [!NOTE]
> Hello 포털에서 hello 자격 증명을 입력 한 후 hello 외부 사용자 선택 hello 올바른 디렉터리 toosign에 있는지 확인 합니다. hello 동일한 사용자 수 액세스 toomultiple 디렉터리가 있을 수 둘 중 하나 hello 표시줄 오른쪽에 hello Azure 포털에서 hello 사용자 이름을 클릭 하 여 선택한 hello 드롭다운 목록에서 hello 적절 한 디렉터리를 선택 합니다.

Hello 디렉터리에 게스트 하면서 hello 외부 사용자 hello Azure 구독에 대 한 모든 리소스를 관리할 수는 있지만 hello 디렉터리에 액세스할 수 없습니다.





![제한 된 tooazure active directory Azure 포털에 액세스](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

Azure Active Directory와 Azure 구독에는 다른 Azure 리소스와 Azure 구독이 가진 것과 같은 자식-부모 관계가 없습니다(예: 가상 컴퓨터, 가상 네트워크, 웹앱, 저장소 등). 후자의 모든 hello 생성, 관리 되 고 Azure 구독에 사용 되는 toomanage hello 액세스 tooan Azure 디렉터리는 Azure 구독에 따라 요금이 청구 있습니다. 자세한 내용은 참조 하십시오. [어떻게 Azure 구독을 관련된 tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory)합니다.

모든 hello 기본 제공 RBAC 역할에서 **소유자** 및 **참가자** hello 환경, 참가자를 만들 수 없는 hello 차이 되 고 새 delete tooall 리소스 완전 한 관리 액세스를 제공 합니다. RBAC 역할입니다. hello 다른 기본 제공 역할 같은 **가상 컴퓨터 참가자** hello와 상관 없이 hello 이름을 가리키는 toohello 리소스만 완전 한 관리 액세스를 제공 합니다. **리소스 그룹** 생성 될 합니다.

할당 hello 기본 제공 RBAC 역할의 **가상 컴퓨터 참가자** 구독 수준에 해당 hello 사용자만 할당 hello 역할을 의미 합니다.

* 그룹을 볼 수 있는 모든 가상 컴퓨터에 관계 없이 해당 배포 날짜 및 hello 리소스의 일부
* Hello 구독에는 완전 한 관리 액세스 toohello 가상 컴퓨터
* Hello 구독에서 다른 리소스 종류를 볼 수 없습니다.
* 요금 청구 관점에서 변경 사항을 수행할 수 없습니다.

> [!NOTE]
> RBAC는 Azure 포털만 기능 되 고, 액세스 toohello 클래식 포털 권한을 부여 하지 않습니다.

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a>기본 제공 RBAC 역할 tooan 외부 사용자를 할당 합니다.
이 테스트의 서로 다른 시나리오에 대 한 외부 사용자 hello "alflanigan@gmail.com"으로 추가 됩니다 한 **가상 컴퓨터 참가자**합니다.




![가상 컴퓨터 참여자 기본 제공 역할](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

이 외부 사용자에 게이 기본 제공 역할에 대 한 일반적인 동작 hello toosee 이며만 가상 컴퓨터와 인접 한 리소스 관리자만 리소스를 배포 하는 동안 필요한 관리 합니다. 기본적으로 이러한 제한 된 역할 액세스를 제공 hello Azure 포털에서에서 만든만 tootheir 연락처 리소스에 관계 없이 일부를 구축할 수 있습니다 hello 클래식 포털도에서 (예: 가상 컴퓨터).





![Azure Portal에서 가상 컴퓨터 참가자 역할 개요](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a>동일한 사용자 hello에 대 한 구독 수준에서 부여 액세스할 디렉터리
hello 프로세스 흐름은 동일한 tooadding 외부 사용자의 경우 모두 액세스 toohello 역할에 부여할 hello 사용자 뿐 아니라 hello 관리자 관점 hello RBAC 역할이 부여 하는 것입니다. hello 차이점은 로그인 한 후 hello 구독 내에서 모든 hello 리소스 범위 hello 대시보드에서 사용할 수 있을 hello 초대 된 사용자는 전자 메일 초대 받지 것입니다.

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a>Hello 리소스 그룹 범위에서 RBAC 역할 할당
RBAC 역할을 할당 한 **리소스 그룹** 범위는 두 가지 유형의 사용자-외부 또는 내부 hello 구독 수준에서 hello 역할을 할당 하는 데는 동일한 프로세스에 (hello의 일부가 동일한 디렉터리). hello 사용자 hello RBAC 역할 할당은 toosee 자신의 환경에서 사용할 수 있는 hello 리소스 그룹 할당 된 액세스 hello에서 **리소스 그룹** hello Azure 포털에서에서 아이콘입니다.

## <a name="assign-rbac-roles-at-hello-resource-scope"></a>Hello 리소스 범위에서 RBAC 역할 할당
Hello 역할 hello 구독 수준에서 또는 hello 리소스 그룹 수준에서 할당 하는 데는 동일한 프로세스에 Azure에서 리소스 범위에는 RBAC 역할을 할당, 다음 hello 동일한 두 시나리오 모두에 대 한 워크플로 합니다. Hello RBAC 역할에 할당 되어 있는 hello 사용자가 할당 된 액세스 중 하나에 hello에 hello 항목만 볼 수는 다시 **모든 리소스** 탭에서 대시보드를 직접 합니다.

RBAC 모두에서 리소스 그룹 범위 또는 리소스에 대 한 중요 한 측면은 hello 사용자 toomake 있는지 toosign 인 toohello 올바른 디렉터리에 대 한 합니다.





![Azure Portal에서 디렉터리 로그인](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a>Azure Active Directory 그룹에 대한 RBAC 역할 할당
Hello in Azure 제품 hello 권한 관리, 배포 및 hello 없이 할당된 된 사용자로 다양 한 리소스를 관리의 세 가지 서로 다른 범위에서 RBAC를 사용 하 여 모든 hello 시나리오 개인 구독 관리 해야 합니다. 구독, 리소스 그룹 또는 리소스 범위에 대 한 관계 없이 hello RBAC 역할 할당, 뒤에 할당 된 hello 사용자가 만든 모든 hello 리소스 hello 사용자가 액세스할 수 hello 하나의 Azure 구독으로 청구 됩니다. 이러한 방식으로 hello 청구 전체 해당 Azure 구독에 대 한 관리자 권한이 있는 사용자가 hello 리소스를 관리 하 고 있는 관계 없이 hello 사용에 대 한 전체 개요입니다.

대규모 조직의 RBAC 역할을 적용할 수 있습니다 hello에 해당 hello admin 사용자 hello 관점을 고려 하는 Azure Active Directory 그룹에 대 한 동일한 방식으로 toogrant hello 세분화 된 액세스 하려는 각 사용자에 대해 개별적으로 쓰지 전체 부서 또는 팀에 대 한 따라서 매우 시간 및 관리 효율성 옵션으로 고려 합니다. tooillustrate이 예에서는, hello **참가자** 역할에에서 추가 되었습니다 hello 그룹 tooone hello 구독 수준에서 hello 테 넌 트입니다.





![AAD 그룹에 대한 RBAC 역할 추가](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

이러한 그룹은 Azure Active Directory 내에서만 프로비전되고 관리되는 보안 그룹입니다.

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a>사용자 지정 RBAC 역할 tooopen 지원 PowerShell을 사용 하 여 요청 만들기
Azure에서 사용할 수 있는 hello 기본 제공 RBAC 역할 hello hello 환경에서 사용할 수 있는 리소스에 따라 특정 사용 권한 수준을 확인 합니다. 그러나 hello 관리 사용자의 요구 사항에 맞게 이러한 역할이 있으면 hello 옵션 toolimit 액세스가 더 많은 사용자 지정 RBAC 역할을 만들어 됩니다.

기본 제공 역할 하나 tootake 필요 RBAC 역할 사용자 지정 만들기, 편집 하 고 hello 환경에서 다시 가져와야 합니다. hello 다운로드 및 업로드 hello 역할의 PowerShell 또는 CLI를 사용 하 여 관리 됩니다.

중요 한 toounderstand hello 필수 구성 요소는 사용자 지정 역할 만들기의 hello 구독 수준에서 세분화 된 액세스 권한을 부여 하 고 지원 요청을 열고의 초대 hello 사용자 hello 유연성 허용할 수 있는 경우

이 예제에서는 hello 기본 제공 역할에 대 한 **판독기** 범위로 지정 되지 tooedit 있지만 허용 하는 사용자가 액세스 tooview 모든 hello 리소스 하거나 새로 만들 되었습니다 tooallow hello 사용자 hello 옵션 열기 지원 요청을 사용자 지정 합니다.

hello 내보내기의 첫 번째 작업 hello **판독기** 역할 요구 toobe 완료 PowerShell에서 관리자 권한으로 승격 된 권한으로 실행 합니다.

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![판독기 RBAC 역할의 PowerShell 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

Hello 역할의 tooextract hello JSON 템플릿이 필요합니다.





![사용자 지정 판독기 RBAC 역할의 JSON 템플릿](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

일반적인 RBAC 역할은 **작업**, **NotActions** 및 **AssignableScopes**라는 세 가지 주요 섹션으로 구성됩니다,

Hello에 **동작** 섹션에 나열 된 모든 hello이 역할에 대해 허용 되는 작업입니다. 각 작업은 리소스 공급자에서 할당 된 중요 한 toounderstand 것 합니다. 이 경우 지원 티켓 hello 작성용 **Microsoft.Support** 리소스 공급자를 나열 합니다.

toobe 수 toosee 리소스 공급자 사용 가능 하 고 구독에 등록 된 모든 hello, PowerShell을 사용할 수 있습니다.
```
Get-AzureRMResourceProvider

```
또한 hello 사용 가능한 모든 PowerShell cmdlet toomanage hello 리소스 공급자 hello를 확인할 수 있습니다.
    ![리소스 공급자 관리의 PowerShell 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)

모든 리소스 공급자 hello 섹션 아래에 표시 되는 특정 RBAC 역할에 대 한 작업을 hello toorestrict **NotActions**합니다.
마지막으로, 해당 hello RBAC 역할 안녕하세요 명시적 구독 Id 사용 되는 위치에 필수입니다. hello 구독 Id가 나열 됩니다 hello **AssignableScopes**, 그렇지 않으면 있습니다 수 없으며 tooimport hello 역할 구독에 있습니다.

만들고 hello RBAC 역할 사용자 지정 후 toobe 가져온된 백 hello 환경이 필요 합니다.

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

이 예제에서는이 RBAC 역할에 대 한 사용자 지정 이름을 hello 수준이 "판독기 지원 티켓 액세스" hello 구독 및 tooopen 지원 요청에서 모든 항목 hello 사용자 tooview를 허용 합니다.

> [!NOTE]
> hello hello 동작 여 지원 요청을 허용 하는 두 개의 기본 제공 RBAC 역할은 **소유자** 및 **참가자**합니다. 사용자 toobe 수 tooopen 지원 요청에 대 한 그는 RBAC 역할을 할당 해야 hello 구독 범위 에서만 지원에 대 한 모든 요청은 Azure 구독에 따라 만들어지므로 합니다.

이 새로운 사용자 지정 역할 hello에서 tooan 사용자 지정 된 같은 디렉터리입니다.





![hello Azure 포털에서에서 가져온 사용자 지정 RBAC 역할의 스크린 샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![hello에 사용자 지정 가져온된 RBAC 역할 toouser 할당의 스크린샷 같은 디렉터리](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![가져온 사용자 지정 RBAC 역할에 대한 사용 권한 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

hello 예제가 되었습니다 추가 사용자 지정이 RBAC 역할의 자세한 tooemphasize hello 제한 다음과 같습니다.
* 새 지원 요청을 만들 수 있습니다.
* 새 리소스 범위를 만들 수 없습니다(예: 가상 컴퓨터).
* 새 리소스 그룹을 만들 수 없습니다.





![지원 요청을 만드는 사용자 지정 RBAC 역할의 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![사용자 지정 RBAC 역할의 스크린샷 수 없습니다. toocreate Vm](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![사용자 지정 RBAC 역할의 스크린샷 수 없습니다. toocreate 새 RGs](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a>사용자 지정 RBAC 역할 tooopen 지원 Azure CLI를 사용 하 여 요청 만들기
Azure CLI에 hello 방식으로 toogo는 Mac에서 및 액세스 tooPowerShell 필요 없이 실행 합니다.

hello 단계 toocreate 사용자 지정 역할 동일 hello 유일한 예외는 CLI를 사용 하 여 hello 역할 다운로드할 수 없습니다는 JSON 템플릿을에에서 볼 수 있는 hello CLI hello 됩니다.

이 예의 기본 제공 역할 hello 선택 **백업 판독기**합니다.

```

azure role show "backup reader" --json

```





![백업 읽기 역할의 CLI 스크린샷 표시](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

Hello hello 속성에는 JSON 템플릿을 복사한 후 Visual Studio에서 hello 역할을 편집 **Microsoft.Support** hello에 리소스 공급자를 추가한 **동작** 이 사용자를 열 수 있도록 섹션 toobe hello 백업 자격 증명 모음에 대 한 판독기를 계속 하면서 지원 요청. 다시이 필요한 tooadd hello 구독 ID가이 역할 hello에 사용 되는 위치 **AssignableScopes** 섹션.

```

azure role create --inputfile <path>

```





![사용자 지정 RBAC 역할 가져오기의 CLI 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

이제 hello 새 역할을 hello Azure 포털에서에서 사용할 수 있으며 hello 할당 프로세스는 동일 hello 이전 예제와 같이 hello 합니다.





![CLI 1.0을 사용하여 만든 사용자 지정 RBAC 역할의 Azure Portal 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

Hello 현재 최신 빌드 2017 년 1 hello Azure 클라우드 셸은 일반적으로 사용할 수 있습니다. Azure 클라우드 셸은 보수 tooIDE 및 hello Azure 포털입니다. 이 서비스에서 Azure 내에서 인증되고 호스트되는 브라우저 기반 셸을 가져오고 컴퓨터에 설치된 CLI 대신 사용할 수 있습니다.





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)

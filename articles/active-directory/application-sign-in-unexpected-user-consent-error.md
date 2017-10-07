---
title: "동의 tooan 응용 프로그램을 수행할 때 예기치 않은 오류가 aaa | Microsoft Docs"
description: "Hello 및 프로세스를 승인 tooan 응용 프로그램에 대 한 수행할 수 있는 작업 중 발생할 수 있는 오류에 설명"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: dfee35f3a10e3cc4313109cedd972499452320f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-error-when-performing-consent-tooan-application"></a>동의 tooan 응용 프로그램을 수행할 때 예기치 않은 오류

이 문서에서는 승인 tooan 응용 프로그램의 hello 프로세스 중 발생할 수 있는 오류를 설명 합니다. 오류 메시지를 포함하지 않는 예기치 않은 동의 프롬프트의 문제를 해결하려는 경우 [Azure AD의 인증 시나리오](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)를 참조하세요.

Azure Active Directory와 통합 하는 많은 응용 프로그램 사용 권한 tooaccess 순서 toofunction의 다른 리소스를 필요 합니다. 이러한 리소스는 Azure Active Directory와도 통합 되어, 경우에 종종 일반적인 hello를 사용 하 여 요청 된 사용 권한을 tooaccess 동의 프레임 워크 것입니다. 

이 인해 동의 프롬프트를 표시 되 고 hello는 일반적으로 발생 처음으로 응용 프로그램 사용 되지만 hello 응용 프로그램의 후속 사용에도 발생할 수 있습니다.

특정 조건에는 사용자 tooconsent toohello 응용 프로그램에 필요한 사용 권한을 충족 해야 합니다. 이러한 조건이 충족되지 않으면 다양한 오류가 발생할 수 있습니다. 내용은 다음과 같습니다.

## <a name="requesting-not-authorized-permissions-error"></a>권한 없는 사용 권한 요청 오류
* **AADSTS90093:** &lt;clientAppDisplayName&gt; toogrant을 수 있는 권한이 없는 하나 이상의 사용 권한을 요청 합니다. 사용자 대신 toothis 응용 프로그램에 동의할 수 있는 관리자를 게 문의 하십시오.

이 오류는 사용자는 회사 관리자가 아닌가 toouse 관리자만 부여할 수 있는 권한을 요청 하는 응용 프로그램을 시도할 때 발생 합니다. 해당 조직 대신 하 여 액세스 toohello 응용 프로그램을 부여 하는 관리자가이 오류를 해결할 수 있습니다.

## <a name="policy-prevents-granting-permissions-error"></a>사용 권한 부여를 방지하는 정책 오류
* **AADSTS90093:** 의 관리자로 &lt;tenantDisplayName&gt; 부여 수 없도록 정책을 설정한 &lt;응용 프로그램의 이름&gt; 사용 권한을 요청 하는 hello 합니다. 관리자에 게 문의 &lt;tenantDisplayName&gt;, toothis 앱에서 사용자 대신 사용 권한을 부여할 수 있는 합니다.

관리자가 아닌 사용자가 승인 해야 하는 응용 프로그램 toouse 다음 회사 관리자가 사용자 tooconsent tooapplications에 대 한 hello 기능을 설정 하는 경우이 오류가 발생 합니다. 해당 조직 대신 하 여 액세스 toohello 응용 프로그램을 부여 하는 관리자가이 오류를 해결할 수 있습니다.

## <a name="intermittent-problem-error"></a>일시적인 문제 오류
* **AADSTS90090:** hello 권한을 toogrant를 너무 시도 기록 하는 일시적인 문제가 발생 했습니다. 같습니다&lt;clientAppDisplayName&gt;합니다. 나중에 다시 시도하세요.

이 오류는 일시적인 서비스 쪽 문제가 발생했음을 나타냅니다. Tooconsent toohello 응용 프로그램을 다시 시도 하 여 해결할 수 있습니다.

## <a name="resource-not-available-error"></a>리소스 사용할 수 없음 오류
* **AADSTS65005:** hello 앱 &lt;clientAppDisplayName&gt; 권한을 tooaccess 리소스 요청 &lt;resourceAppDisplayName&gt; 사용할 수 없는 합니다. 

Hello 응용 프로그램 개발자를 게 문의 하십시오.

##  <a name="resource-not-available-in-tenant-error"></a>테넌트에서 리소스 사용할 수 없음 오류
* **AADSTS65005:** &lt;clientAppDisplayName&gt; tooa 리소스 액세스를 요청 하는 &lt;resourceAppDisplayName&gt; 조직에서 사용할 수 없는 &lt; tenantDisplayName&gt;합니다. 

이 리소스를 사용할 수 있도록 하거나 &lt;tenantDisplayName&gt;의 관리자에게 문의합니다.

## <a name="permissions-mismatch-error"></a>권한 불일치 오류
* **AADSTS65005:** hello 앱 동의 tooaccess 리소스를 요청한 &lt;resourceAppDisplayName&gt;합니다. Hello 앱 어 떠 미리 구성 된 앱 등록 중 일치 하지 않기 때문에이 요청에 실패 했습니다. 연락처 hello 앱 vendor.* *

Hello 응용 프로그램 사용자 (테 넌 트) hello 조직의 디렉터리에서 찾을 수 없는 리소스는 응용 프로그램 사용 권한 tooaccess 요청 tooconsent toois 유형 모두에 이러한 오류가 발생 합니다. 이 오류는 다음과 같은 이유로 발생할 수 있습니다.

-   hello 클라이언트 응용 프로그램 개발자가 해당 응용 프로그램, 잘못 구성 toorequest 액세스 tooan 잘못 된 리소스를 발생 합니다. 이 경우 응용 프로그램 개발자 hello hello 클라이언트 응용 프로그램 tooresolve의 hello 구성이이 문제를 업데이트 해야 합니다.

-   Hello 대상 리소스 응용 프로그램을 나타내는 서비스 사용자 hello 조직에 존재 하지 않는 또는 지난 hello에 존재 하지만 제거 되었습니다. tooresolve이, 서비스 사용자에 대 한 발급 hello 클라이언트 응용 프로그램 사용 권한 tooit를 요청할 수 있도록 hello 조직에서 hello 리소스 응용 프로그램 프로 비전 되어야 합니다. 다양 한 방법으로 응용 프로그램의 hello 유형에 따라에 발생할 수이 있습니다는 다음 작업을 포함 하 여:

    -   Hello 리소스 응용 프로그램 (Microsoft 게시 된 응용 프로그램)에 대 한 구독

    -   승인 toohello 리소스 응용 프로그램

    -   Hello Azure 포털을 통해 hello 응용 프로그램 권한 부여

    -   Hello Azure AD 응용 프로그램 갤러리에서에서 hello 응용 프로그램을 추가합니다.

## <a name="next-steps"></a>다음 단계 

[Azure Active Directory에서 앱, 사용 권한 및 동의(v1 끝점)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[범위, 권한 및 hello Azure Active Directory (v2.0 끝점)에 동의](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)



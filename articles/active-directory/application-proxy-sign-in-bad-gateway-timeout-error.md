---
title: "aaa \"응용 프로그램 프록시 응용 프로그램을 사용 하는 경우이 회사 응용 프로그램 오류에 액세스할 수 없습니다 | \"Microsoft Docs"
description: "어떻게 tooresolve 공용 액세스는 Azure AD 응용 프로그램 프록시 응용 프로그램과 함께 발급 합니다."
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
ms.openlocfilehash: 490b106b7d774ee43fc076cc5d082997a1df85e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cant-access-this-corporate-application-error-when-using-an-application-proxy-application"></a>응용 프로그램 프록시 응용 프로그램을 사용하는 경우 발생하는 "이 회사 응용 프로그램에 액세스할 수 없습니다." 오류

이 문서가 도움이 되었나요 tootroubleshoot 일반적인 문제는 Azure AD 응용 프로그램 프록시 응용 프로그램의 "이 회사 앱에 액세스할 수 없습니다" 오류를 참조 하는 경우를 처리 합니다.

## <a name="overview"></a>개요
이 오류가 표시 되 면 hello 페이지는 상태 코드를 공유할 수도 있습니다. 해당 코드는 hello 다음 중 하나일 것입니다.

-   **게이트웨이 시간 초과**: hello 응용 프로그램 프록시 서비스는 hello 커넥터 tooreach 수 없습니다. 일반적으로 hello 커넥터 할당, 자체 커넥터 또는 hello hello 커넥터 주위 규칙 네트워킹 문제가 있음을 나타냅니다.

-   **잘못 된 게이트웨이**: hello 커넥터가 없습니다 tooreach hello 백 엔드 응용 프로그램입니다. Hello 응용 프로그램의 구성이 잘못을 의미할 수 있습니다.

-   **사용 권한 없음**: hello 사용자 권한이 부여 된 tooaccess hello 응용 프로그램이 아닙니다. 이 hello 사용자 toohello 응용 프로그램이 Azure Active Directory에서 할당 되지 않은 경우 또는 hello 백 엔드에 hello 사용자 권한 tooaccess hello 응용 프로그램이 없는 경우 발생할 수 있습니다.

hello hello "상태 코드" 필드에 대 한 hello 오류 메시지의 왼쪽 아래에 텍스트를 보면 hello 살펴보고 toofind hello 코드입니다. 또한 hello 추가 팁 포함 된 hello 페이지의 맨 아래에서 모든 메모를 찾아보십시오.

   ![게이트웨이 시간 초과 오류](./media/application-proxy/connection-problem.png)

에 대 한 내용은 tootroubleshoot 이러한 오류 및 제안 된 수정 사항에 대 한 자세한 내용은의 근본 원인을 hello 하는 방법, 아래의 hello 해당 섹션을 참조 합니다.

## <a name="gateway-timeout-errors"></a>게이트웨이 시간 초과 오류

게이트웨이 시간 초과 hello 서비스가 tooreach hello 커넥터를 시도 하 고는 없습니다 toowithin hello 제한 시간 창 발생 합니다. 일반적으로는 tooa 없는 작업 커넥터를 커넥터 그룹을 할당 하는 응용 프로그램 또는 hello 커넥터에 필요한 일부 포트가 열려 있지 않습니다.


## <a name="bad-gateway-errors"></a>잘못된 게이트웨이 오류

잘못 된 게이트웨이 오류 hello 커넥터에 없습니다 tooreach hello 백 엔드 응용 프로그램을 나타냅니다. hello 올바른 응용 프로그램을 게시 하 고 있는지 확인 합니다. 이 오류를 발생시키는 일반적인 실수:

-   입력 오류와 hello 내부 URL이 잘못

-   Hello hello 응용 프로그램의 루트를 게시 되지 않습니다. 예를 들어 게시 <http://expenses/reimbursement> tooaccess 시도 하지만 <http://expenses>

-   Hello 위임 KCD (Kerberos 제한) 구성에 있는 문제

-   Hello 백 엔드 응용 프로그램에 문제가 있습니다.

## <a name="forbidden-errors"></a>금지된 오류

사용할 수 없음된 오류를 표시 되 면 hello 사용자 할당 되지 않은 toohello 응용 프로그램입니다. Azure Active Directory 또는 hello 백 엔드 응용 프로그램에 수 있습니다.

toolearn tooassign 사용자가 Azure에서 응용 프로그램 toohello hello를 참조 하는 방법을 [구성 문서](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal#add-a-test-user)합니다.

Hello 사용자가 Azure에서 toohello 응용 프로그램 할당, 확인 하는 경우에 hello 백 엔드 응용 프로그램에서 hello 사용자 구성을 확인 합니다. Kerberos 제한 위임/통합 Windows 인증을 사용하는 경우 몇 가지 지침은 KCD 문제 해결 페이지를 볼 수 있습니다.

## <a name="check-hello-applications-internal-url"></a>Hello 응용 프로그램의 내부 URL 확인

첫 번째 빠른 단계로 다시 확인 확인 하 여 수정 hello 내부 URL을 통해 hello 응용 프로그램을 여 **엔터프라이즈 응용 프로그램**, hello를 차례로 선택 하 고 **응용 프로그램 프록시** 메뉴. 이 hello 올바른 내부 URL을 hello 온-프레미스 네트워크 tooaccess hello 응용 프로그램에서 사용 된 것을 확인 합니다.

## <a name="check-hello-application-is-assigned-tooa-working-connector-group"></a>Hello 응용 프로그램 작업 커넥터 그룹 tooa 할당 확인

tooverify hello 응용 프로그램 작업 커넥터 그룹 tooa를 할당 되어 있습니다.

1.  너무 이동 하 여 hello 포털에서 hello 응용 프로그램을 열고**Azure Active Directory**에, **엔터프라이즈 응용 프로그램**, 다음 **모든 응용 프로그램입니다.** Hello 응용 프로그램을 연 다음 선택 **응용 프로그램 프록시** hello 왼쪽된 메뉴에서 합니다.

2.  Hello 커넥터 그룹 필드를 확인 합니다. Hello 그룹에 활성 커넥터가 없는 경우 경고를 표시 합니다. 모든 경고 보이지 않으면 이동 너무: "verify 모든 필요한 포트를 허용 목록" 합니다.

3.  이 hello 경우 잘못 커넥터 그룹 hello 드롭다운 tooselect hello 올바른 그룹을 사용 하 고 더 이상 모든 경고를 볼 수를 확인 합니다. Hello 커넥터 그룹을 의도 한 경우, hello 경고 메시지 tooopen hello 페이지 커넥터 관리를 클릭 합니다.

4.  여기에서의 몇 가지 방법으로 toodrill를 추가로 가지 있습니다.

  * 현재 커넥터 hello 그룹으로 이동: toothis 그룹에 속해야 하며 시야 toohello 대상 백 엔드 응용 프로그램을 포함 하는 활성 커넥터를 설정한 경우 hello 커넥터를 할당 하는 hello 그룹으로 이동할 수 있습니다. 따라서 toodo hello 커넥터를 클릭 합니다. Hello "커넥터 그룹" 필드에 hello 드롭 다운 tooselect hello 올바른 그룹을 사용 하 고 저장을 클릭 합니다.

  * 해당 그룹에 대 한 새 커넥터를 다운로드 합니다:이 페이지에서 가져올 수 있습니다 hello 링크 너무[새 커넥터를 다운로드](https://download.msappproxy.net/Subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/Connector/Download)합니다. hello 응용 프로그램으로 동일한 서버를 hello 하는 hello 커넥터 요구 toobe 직접적인 toohello 백 엔드 응용 프로그램을 사용 하는 컴퓨터에 설치 하 고에 일반적으로 배치 됩니다. 사용 하 여 hello 커넥터 링크 toodownload hello 대상 컴퓨터에 커넥터를 다운로드 합니다. 다음 hello 커넥터를 클릭 하 고 hello "커넥터 그룹" 드롭 다운 toomake toohello 권한 그룹에 속해 있는지를 사용 합니다.

  * 비활성 커넥터 조사: 되는 커넥터 비활성으로 표시 되 면는 없습니다 tooreach hello 서비스입니다. 이 일반적으로 인해 toosome 필요한 포트가 차단 되 고 있습니다. toosolve이 문제점, 너무 "확인 모든 필요한 포트를 허용 목록" 이동 합니다.

다음이 단계를 사용한 후 tooensure hello 응용 프로그램은 커넥터 수, 테스트 hello 응용 프로그램을 다시 사용 tooa 할당 된 그룹입니다. 아직 작동 하지 않아, toohello 다음 섹션을 계속 합니다.

## <a name="check-all-required-ports-are-whitelisted"></a>모든 필요한 포트가 허용 목록에 포함되는지 확인

필요한 모든 포트가 열려 있는지 tooverify 포트 열기에 설명서를 참조 하십시오. 모든 hello 필요한 포트가 열려 있으면 toohello 다음 섹션을 이동 합니다.

## <a name="check-for-other-connector-errors"></a>다른 커넥터 오류에 대한 확인

Hello 문제를 해결 hello 위의 중 hello 다음 단계 toolook 문제 또는 hello 자체 커넥터를 사용 하 여 오류에 대 한 것입니다. Hello에 몇 가지 일반적인 오류를 볼 수 있습니다 [문제 해결 문서](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors)합니다. 

모든 오류 hello 커넥터 로그 tooidentify에서 직접 찾아볼 수도 있습니다. 이 오류 메시지 중 많은 수 tooshare 수정 사항에 대 한 보다 구체적인 권장 사항을 수입니다. tooview hello 로그를 확인 하려면 어떻게 toolearn [커넥터 설명서](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood)합니다.

## <a name="additional-resolutions"></a>추가 해상도

위의 hello hello 문제를 해결 하지 않은 경우 몇 가지 다른 가능한 원인 있습니다. tooidentify hello 문제:

응용 프로그램이 구성 된 toouse 경우 IWA Windows 통합 인증 (), single sign on 없이 hello 응용 프로그램을 테스트 합니다. 파일이 없으면 toohello 다음 단락을 이동 합니다. single sign on, 없이 toocheck hello 응용 프로그램을 통해 응용 프로그램을 열고 **엔터프라이즈 응용 프로그램** toohello 이동 **Single Sign On** 메뉴. 변경 hello에서에서 드롭다운 "통합 Windows 인증" 너무 "Azure AD에서 single sign-on disabled"입니다. 

이제 브라우저를 열고 tooaccess hello 응용 프로그램을 다시 시도 하십시오. 인증에 대 한 메시지가 표시 되어야 하 고이 정보를 hello 응용 프로그램으로 가져옵니다. 이 방법이 작동 hello single sign on 수 있도록 하는 hello 위임 KCD (Kerberos 제한) 구성 hello 문제가 있습니다. 참조 hello KCD 문제 해결 페이지입니다.

Toosee hello 오류를 계속 진행 하면 toohello 컴퓨터에 커넥터를 설치 하는 hello 브라우저 및 시도 tooreach hello 내부 URL hello 응용 프로그램에 사용 되는 열 있는 이동 합니다. hello 커넥터 처럼 작동 hello에서 다른 클라이언트가 동일한 시스템. Hello 응용 프로그램을 연결할 수 없는 경우 해당 컴퓨터는 없습니다 tooreach hello 응용 프로그램, 이유를 조사 하거나 수 tooaccess hello 응용 프로그램 서버에 커넥터를 사용 합니다.

경우 toolook 문제 또는 hello 자체 커넥터를 사용 하 여 오류에 대 한 컴퓨터에서 hello 응용 프로그램을 연결할 수 있습니다. Hello에 몇 가지 일반적인 오류를 볼 수 있습니다 [문제 해결 문서](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors)합니다. 모든 오류 hello 커넥터 로그 tooidentify에서 직접 찾아볼 수도 있습니다. 이 오류 메시지 중 많은 수 tooshare 수정 사항에 대 한 보다 구체적인 권장 사항을 수입니다. tooview hello 로그를 확인 하려면 어떻게 toolearn [커넥터 설명서](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood)합니다.

## <a name="next-steps"></a>다음 단계
[Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)

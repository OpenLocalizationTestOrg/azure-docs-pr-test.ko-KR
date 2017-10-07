---
title: "Azure MFA 및 AD FS를 사용 하 여 클라우드 리소스 aaaSecure | Microsoft Docs"
description: "Azure MFA 및 AD FS hello 클라우드에서 tooget 시작 하는 방법을 설명 하는 hello Azure Multi-factor authentication 페이지입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a>Azure Multi-Factor Authentication 및 AD FS를 사용하여 클라우드 리소스 보안 유지
Azure Active Directory와 페더레이션 조직의 경우 Azure Multi-factor Authentication 또는 Azure AD에 액세스 하는 Active Directory Federation Services (AD FS) toosecure 리소스를 사용 합니다. Azure Multi-factor Authentication 또는 Active Directory Federation Services를 사용 하 여 프로시저 toosecure Azure Active Directory 리소스를 다음 hello를 사용 합니다.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>AD FS를 사용하여 Azure AD 리소스 보안 유지
toosecure 클라우드 리소스에 있도록를 설정 클레임 규칙 2 단계 인증을 성공적으로 수행할 때 Active Directory Federation Services hello multipleauthn 클레임을 내보냅니다. 이 클레임 tooAzure AD에 전달 됩니다. 이 프로시저 toowalk hello 단계를 수행 합니다.


1. AD FS 관리를 엽니다.
2. Hello 왼쪽에서 선택 **신뢰 당사자 트러스트**합니다.
3. **Microsoft Office 365 ID 플랫폼**을 마우스 오른쪽 단추로 클릭하고 **클레임 규칙 편집**을 선택합니다.

   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. 발급 변환 규칙에서 **규칙 추가**를 클릭합니다.

   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. 변환 클레임 규칙 추가 마법사 hello, 선택 **통과 또는 들어오는 클레임 필터링** 에서 드롭 다운 hello 및 **다음**합니다.

   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. 규칙의 이름을 지정합니다. 
7. 선택 **인증 방법 참조** 들어오는 hello로 클레임 유형입니다.
8. **모든 클레임 값 통과**를 선택합니다.
    ![변환 클레임 규칙 추가 마법사](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. **마침**을 클릭합니다. Hello AD FS 관리 콘솔을 닫습니다.

## <a name="trusted-ips-for-federated-users"></a>페더레이션 사용자를 위한 신뢰할 수 있는 IP
신뢰할 수 있는 Ip tooby 패스 2 단계 인증에 대 한 특정 IP 주소 또는 페더레이션된 사용자 자신의 인트라넷 내에서 발생 하는 요청에 대 한 관리자를 수 있습니다. hello 다음 섹션에서는 설명 방법을 tooconfigure Azure Multi-factor Authentication 신뢰할 수 있는 Ip 페더레이션된 사용자와 페더레이션된 사용자 인트라넷 내에서 요청을 시작 하는 경우 2 단계 인증을 무시 합니다. 이 내부 회사 네트워크 클레임 유형 hello를 사용 하 여 AD FS toouse 통과 또는 필터는 들어오는 청구 서식 파일을 구성 하 여 수행 됩니다.

이 예제는 신뢰 당사자 트러스트에 대해 Office 365를 사용합니다.

### <a name="configure-hello-ad-fs-claims-rules"></a>Hello AD FS 클레임 규칙 구성
hello 먼저 toodo tooconfigure hello AD FS 클레임 됩니다. Hello 내부 회사 네트워크에 대 한 클레임 형식 및 다른 하나는 사용자의 로그인 페이지에 유지, 두 개의 클레임 규칙을 만듭니다.

1. AD FS 관리를 엽니다.
2. Hello 왼쪽에서 선택 **신뢰 당사자 트러스트**합니다.
3. **Microsoft Office 365 ID 플랫폼**을 마우스 오른쪽 단추로 클릭하고 **클레임 규칙 편집...**를 선택합니다.
   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)
4. 발급 변환 규칙에서 **규칙 추가**를 클릭합니다.
   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)
5. 변환 클레임 규칙 추가 마법사 hello, 선택 **통과 또는 들어오는 클레임 필터링** 에서 드롭 다운 hello 및 **다음**합니다.
   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)
6. Hello 상자 다음 tooClaim 규칙 이름에 규칙 이름을 지정 합니다. 예를 들어 InsideCorpNet입니다.
7. Hello 드롭다운 목록에서에서 다음 tooIncoming 클레임 유형, 선택 **내부 회사 네트워크**합니다.
   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)
8. **마침**을 클릭합니다.
9. 발급 변환 규칙에서 **규칙 추가**를 클릭합니다.
10. 변환 클레임 규칙 추가 마법사 hello, 선택 **사용자 지정 규칙을 사용 하 여 클레임 보내기** 에서 드롭 다운 hello 및 **다음**합니다.
11. 클레임 규칙 이름 아래의 상자 hello: 입력 *Keep Users Signed In*합니다.
12. Hello 사용자 지정 규칙 상자에 다음을 입력 합니다.

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. **Finish**를 클릭합니다.
14. **Apply**를 클릭합니다.
15. **Ok**를 클릭합니다.
16. AD FS 관리를 닫습니다.

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a>페더레이션 사용자로 Azure Multi-Factor Authentication 신뢰할 수 있는 IP 구성
Hello 클레임을 저장 했으므로 신뢰할 수 있는 Ip를 구성할 수 있습니다.

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. Hello 왼쪽에서 클릭 **Active Directory**합니다.
3. 디렉터리에서 신뢰할 수 있는 Ip tooset 저장할 hello 디렉터리를 선택 합니다.
4. 선택한 디렉터리 hello 클릭 **구성**합니다.
5. Hello multi-factor 인증 섹션에서 클릭 **서비스 설정 관리**합니다.
6. Hello 서비스 설정 페이지에서 신뢰할 수 있는 Ip 선택 **authentication을 건너뛰도록 다중-factor-요청에 대 한 페더레이션된 사용자의 내 인트라넷에서**합니다.  

   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. **저장**을 클릭합니다.
8. Hello 업데이트를 적용 한 후 클릭 **닫습니다**합니다.

끝났습니다. 이 시점에서 Office 365 페더레이션된 사용자 클레임 hello 회사 인트라넷 외부에서 발생 하는 경우에 toouse MFA 포함 되어야 합니다.

---
title: Multi-factor Authentication FAQ aaaAzure | Microsoft Docs
description: "자주 묻는 질문 및 답변 tooAzure Multi-factor Authentication 관련합니다. Multi-Factor Authentication은 사용자 이름 및 암호 이상을 요구하여 사용자 ID를 확인하는 방법입니다. 추가 계층을 보안 toouser 로그인 및 트랜잭션을 제공합니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8305cf4c41bf8e9802df192fecdb7e463eff9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication에 대한 질문과 대답
이 FAQ Azure Multi-factor Authentication 및 hello Multi-factor Authentication 서비스를 사용 하는 방법에 대 한 일반적인 질문에 대답 합니다. 나뉘어집니다 hello 서비스에 대 한 질문으로 일반적으로 모델의 경우 사용자 경험, 대금 청구 및 문제 해결.

## <a name="general"></a>일반
**Q: Azure Multi-Factor Authentication 서버는 사용자 데이터를 어떻게 처리하나요?**

Multi-factor Authentication 서버 사용자 데이터 hello 온-프레미스 서버에만 저장 됩니다. 영구 사용자 데이터가 없으며 hello 클라우드에 저장 됩니다. Hello 사용자 2 단계 인증을 수행 하는 경우 Multi-factor Authentication 서버 데이터 toohello 인증을 위한 Azure Multi-factor Authentication 클라우드 서비스를 보냅니다. Multi-factor Authentication 서버와 hello Multi-factor Authentication 클라우드 서비스 간의 통신 포트 443 아웃 바운드을 통해 Secure Sockets Layer (SSL) 또는 보안 TLS (전송 계층)를 사용합니다.

인증 및 사용 현황 데이터는 수집 인증 요청 toohello 클라우드 서비스를 보내면 보고서. 2단계 인증 로그에 포함된 데이터 필드는 다음과 같습니다.

* **고유 ID** (사용자 이름 또는 온-프레미스 Multi-Factor Authentication 서버 ID)
* **이름과 성** (선택 사항)
* **전자 메일 주소** (선택 사항)
* **전화 번호** (음성 통화 또는 SMS 인증을 수행할 때)
* **장치 토큰** (모바일 앱 인증을 수행할 때)
* **인증 모드**
* **인증 결과**
* **Multi-Factor Authentication 서버 이름**
* **Multi-Factor Authentication 서버 IP**
* **클라이언트 IP** (사용 가능한 경우)

hello 선택적 필드는 Multi-factor Authentication 서버에서 구성할 수 있습니다.

확인 결과 (성공 또는 거부) hello 고 hello 이유가 거부 된 경우 저장 hello 인증 데이터. 이 데이터는 인증 및 사용 보고서에서 사용할 수 있습니다.

## <a name="billing"></a>결제
Tooeither hello를 참조 하 여 대부분 청구 관련 질문에 대답할 수 있습니다 [Multi-factor Authentication 가격 페이지](https://azure.microsoft.com/pricing/details/multi-factor-authentication/) 또는 hello 설명서에 대 한 [어떻게 tooget Azure Multi-factor Authentication](multi-factor-authentication-versions-plans.md)합니다.

**Q: 내 조직 hello 전화 통화 및 문자 메시지 인증에 사용 되는 전송에 대 한 요금이 청구는?**

아니요, 개별 전화 통화에 대 한 비용이 청구 되지 않습니다 또는 문자 메시지 toousers Azure Multi-factor Authentication을 통해 전송 합니다. 인증 단위 MFA 공급자를 사용 하는 경우 사용 하는 hello 방법 아니라 각 인증에 대 한 요금이 청구 됩니다.

사용자가 hello 전화 통화 또는 문자 메시지를 받을 따라 tootheir 개인 전화 서비스에 대 한 요금이 청구 될 수 있습니다.

**Q: hello 사용자별으로 청구 모델 요금을 청구 하나요 나 사용 가능한 모든 사용자 또는 2 단계 인증을 수행 하는 것 만으로 hello?**

요금 청구는 2 단계 인증 그 달을 수행 여부에 관계 없이 구성 된 사용자 toouse Multi-factor Authentication의 hello 수를 기반으로 합니다.

**Q:Multi-Factor Authentication은 어떤 방식으로 청구됩니까?**

사용자 단위 또는 인증 단위 MFA 공급자를 만들 때 해당 조직의 Azure 구독이 사용량을 기준으로 매월 청구됩니다. 이 청구 모델은 비슷한 toohow Azure 가상 컴퓨터 및 웹 사이트의 사용에 대 한 청구 합니다.

Azure Multi-factor Authentication에 대 한 구독을 구매 하는 경우 조직의 각 사용자에 대 한 hello 연간 사용료만 유용 합니다. MFA 라이선스 및 Office 365, Azure AD Premium 또는 Enterprise Mobility + Security 번들은 이 방법으로 청구됩니다. 

다음에서 옵션에 대 한 자세한 [어떻게 tooget Azure Multi-factor Authentication](multi-factor-authentication-versions-plans.md)합니다.

**Q: Azure Multi-Factor Authentication의 평가판 버전이 있나요?**

일부 경우에 그렇습니다.

Multi-factor Authentication for Azure Administrators hello Azure 및 Office 365 관리자 포털을 포함 하 여 tooMicrosoft 온라인 서비스 액세스 비용 없이 Azure MFA 기능 하위 집합을 제공 합니다. 이 제품에는 Azure Active Directory 인스턴스에서 MFA 라이선스, 번들 또는 독립 실행형 소비 기반 공급자를 통해 Azure MFA의 hello 전체 버전을 갖지 않는 tooglobal 관리자만 적용 됩니다. 관리자 hello 무료 버전을 사용 하는 경우 Azure MFA의 정식 버전 구입 하는 다음 모든 전역 관리자가 높은 toohello 버전을 자동으로 지불 됩니다.

Office 365 사용자에 대해 Multi-factor Authentication tooOffice 365 서비스, Exchange Online 및 SharePoint Online을 포함 하 여 액세스 비용 없이 Azure MFA 기능 하위 집합을 제공 합니다. 이 제품은 hello Azure Active Directory의 해당 인스턴스에 없는 경우 hello 정식 버전의 Azure MFA MFA 라이선스, 번들 또는 독립 실행형 소비 기반 공급자를 통해 때 할당 된 Office 365 라이선스가 있는 toousers 적용 됩니다.

**Q: 조직에서 사용자당 청구 모델과 인증당 청구 모델 간을 전환할 수 있습니까?**

조직에서 사용량 기반 청구를 포함하는 독립 실행형 서비스로 MFA를 구입한 경우 MFA 공급자를 만들 때 청구 모델을 선택합니다. MFA 공급자를 만든 후에 hello 청구 모델을 변경할 수 없습니다. 그러나 hello MFA 공급자를 삭제 하 고이 다른 청구 모델 작업을 하나를 만들 수 있습니다.

MFA 공급자가 만들어지면 연결 된 Azure Active Directory (즉, "Azure AD 테 넌 트") tooan 수 있습니다. Hello 현재 MFA 공급자가 연결 된 tooan Azure AD 테 넌 트를 안전 하 게 hello MFA 공급자를 삭제 고 만들 수 있습니다 연결된 toohello 동일한 Azure AD 테 넌 트 되는 것입니다. 또는 모든 사용자가 MFA에 대해 사용할 수 있는 충분 한 MFA, Azure AD Premium 또는 Enterprise Mobility + 보안 (EMS) 라이선스 toocover를 구입, hello MFA 공급자를 완전히 삭제할 수 있습니다.

MFA 공급자가 *하지* , 연결 된 tooan Azure AD 테 넌 트 또는 있습니다 연결 hello 새 MFA 공급자 tooa 다른 Azure AD 테 넌 트, 사용자 설정 및 구성 옵션 전송 되지 않습니다. 또한 Azure MFA 서버를 기존 필요를 통해 생성 되는 정품 인증 자격 증명을 사용 하 여 다시 활성화 toobe hello 새 MFA 공급자입니다. MFA 서버 toolink hello를 다시 활성화 하 toohello 새 MFA 공급자에 영향을 주지 전화 통화 및 문자 메시지 인증 하지만 모바일 앱 알림을 hello 모바일 앱을 다시 활성화 될 때까지 모든 사용자에 대해 작동이 중지 됩니다.

[Azure Multi-Factor Auth 공급자 시작](multi-factor-authentication-get-started-auth-provider.md)에서 MFA 공급자에 대해 자세히 알아보세요.

**Q: 조직에서 언제든지 사용량 기반 요금 청구 및 구독(라이선스 기반 모델) 간을 전환할 수 있나요?**

일부 경우에 그렇습니다.

디렉터리에 *사용자당* Azure Multi-Factor Authentication 공급자가 있는 경우 MFA 라이선스를 추가할 수 있습니다. 라이선스를 갖고 있는 사용자는 hello 사용자 단위 사용량 기반 요금 청구에 계산 되지 않습니다. 여전히 라이선스가 없는 사용자가 hello MFA 공급자를 통해 MFA에 대해 사용할 수 있습니다. 구입 하 고 할당 하는 경우 모든 사용자에 대 한 라이선스 toouse Multi-factor Authentication을 구성을 hello Azure Multi-factor Authentication 공급자를 삭제할 수 있습니다. 항상 hello 향후에 더 많은 사용자 라이선스 수보다 있는 경우 다른 사용자 단위 MFA 공급자를 만들 수 있습니다.

디렉터리에는 *인증 단위* Azure Multi-factor Authentication 공급자 hello MFA 공급자는 연결 된 tooyour 구독으로 항상 각 인증에 대 한 청구 됩니다. MFA 라이선스 toousers를 할당할 수 있지만 계속 청구 됩니다 모든 2 단계 확인 요청에 대해 할당 된 MFA 라이선스 누군가로부터 제공 여부.

**Q: 내 조직 toouse가 않으며 identities toouse Azure Multi-factor Authentication 동기화?**

조직에서 사용량 기반 청구 모델을 사용하는 경우 Azure Active Directory는 선택 사항이며 필수가 아닙니다. MFA 공급자에 연결 된 Azure AD 테 넌 트 tooan 없으면 Azure Multi-factor Authentication 서버 또는 hello Azure Multi-factor Authentication SDK 온-프레미스만 배포할 수 있습니다.

라이선스 구입 하 고 toousers hello 디렉터리에 할당 하는 경우 toohello Azure AD 테 넌 트 추가 되기 때문에 azure Active Directory는 hello 라이선스 모델에 필요 합니다.

## <a name="manage-and-support-user-accounts"></a>사용자 계정 관리 및 지원

**Q: 해야 알 내 사용자 toodo, 전화에 응답을 수신 하지 않는 또는 전화 번호와 없는 여부?**

모든 사용자가 두 가지 이상의 인증 방법을 구성했기를 바랍니다. 다시, 로그인 tootry 알려 하지만 hello 로그인 페이지에서 다른 본인 확인 방법을 선택 합니다.

사용자가 toohello를 가리킬 수 [최종 사용자 문제 해결 가이드](./end-user/multi-factor-authentication-end-user-troubleshoot.md)합니다.


**Q: 어떻게 해야 합니까 경우 tootheir 계정에서 사용자를 가져올 수 없습니다.**

Hello 사용자의 계정으로 지정 함으로써 toogo hello 등록 프로세스를 통해 다시 설정할 수 있습니다. 에 대 한 자세한 내용은 [hello 클라우드에서 Azure Multi-factor Authentication을 사용 하 여 사용자 및 장치 설정 관리](multi-factor-authentication-manage-users-and-devices.md)합니다.

**Q: 내 사용자 중 하나가 앱 암호를 사용하는 전화기를 분실한 경우 어떻게 해야 하나요?**

tooprevent 무단 액세스를 모든 hello 사용자의 앱 암호 삭제 합니다. Hello 사용자에 게 장치를 교체를 후 hello 암호를 다시 만들 수 있습니다. 에 대 한 자세한 내용은 [hello 클라우드에서 Azure Multi-factor Authentication을 사용 하 여 사용자 및 장치 설정 관리](multi-factor-authentication-manage-users-and-devices.md)합니다.

**Q: 사용자 수 없는 로그인 한 경우 toonon 브라우저 앱?**

조직 여전히 사용 중인 경우 레거시 클라이언트로 [hello 앱 암호 사용을 허용](multi-factor-authentication-whats-next.md#app-passwords), 다음 사용자가 자신의 사용자 이름 및 암호로 toothese 레거시 클라이언트에 로그인 할 수 없습니다. 대신, 너무 필요한[앱 암호를 설정](./end-user/multi-factor-authentication-end-user-app-passwords.md)합니다. 사용자 (delete)의 선택을 취소 해야 자신의 로그인 정보 hello 응용 프로그램을 다시 시작 하 고 자신의 사용자 이름을 사용 하 여 로그인 하 고 *앱 암호* 일반 암호 대신 합니다.

조직으로 지정 되지 않은 기존 클라이언트 있습니다 해야 없도록 사용자 toocreate 앱 암호입니다.

> [!NOTE]
> Office 2013 클라이언트에 대한 최신 인증
>
> 앱 암호는 최신 인증을 지원하는 않는 앱에만 필요합니다. Office 2013 클라이언트 최신 인증 프로토콜을 지원 하지만 toobe 구성 해야 합니다. 최신 Office 클라이언트는 최신 인증 프로토콜을 자동으로 지원합니다. 자세한 내용은 참조 hello [Office 2013 최신 인증 공개 미리 보기 공지](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)합니다.

**Q: 내 사용자가 이제는 hello 텍스트 메시지를 받지 않으면 때로는 또는 tootwo 양방향 문자 메시지를 회신 있지만 hello 확인 시간이 초과 합니다.**

문자 메시지 배달 및 양방향 SMS 응답 수신 되지 않을 수도 있으므로 hello 서비스의 hello 안정성에 영향을 줄 수 있는 제어할 수 없는 요인이 있습니다. 이러한 요소는 hello 대상 국가, hello 휴대폰 통신 업체 및 신호 강도 hello 포함 됩니다.

사용자에 게 안정적으로 텍스트 메시지를 수신 하는 문제가 자주 있으면 알려 toouse hello 모바일 앱 또는 전화 통화 방법을 대신 합니다. hello 모바일 앱에는 모두 셀룰러와 Wi-fi 연결을 통해 알림을 받을 수 있습니다. 또한 hello 장치에 신호가 없는 전혀 하는 경우에 hello 모바일 앱 확인 코드를 생성할 수 있습니다. hello Microsoft Authenticator 앱에 사용할 수 있는 [Android](http://go.microsoft.com/fwlink/?Linkid=825072), [IOS](http://go.microsoft.com/fwlink/?Linkid=825073), 및 [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071)합니다.

텍스트 메시지를 사용해야 하는 경우 가능하면 양방향 SMS보다는 단방향 SMS를 사용하는 것이 좋습니다. 단방향 SMS 보다 안정적 이며 사용자에서 다른 국가에서 보낸 회신 tooa 텍스트 메시지에서 전역 SMS 요금이 발생 수 없습니다.

**Q: hello 기간 hello 시스템 시간이 초과 되기 전에 내 사용자가 문자 메시지의 tooenter hello 인증 코드를 변경할 수 있습니까?**

일부 경우에 가능합니다. 

Azure MFA 서버 v7.0 이상 단방향 SMS를 구성할 수 있습니다 hello 제한 시간 설정을 구성 하 여 레지스트리 키입니다. Hello MFA 클라우드 서비스는 hello 텍스트 메시지를 보내면 hello 확인 코드 (또는 일회용 암호)와 MFA 서버 toohello를 반환 됩니다. 기본적으로 300 초 동안 메모리에 hello 코드를 저장 하는 hello와 MFA 서버입니다. Hello 사용자 hello 하기 전에 hello 코드를 입력 하지 않습니다 300 초를 통과 하는 경우의 인증이 거부 됩니다. 이러한 단계 toochange hello 기본 제한 시간 설정을 사용 합니다.

1. TooHKLM\Software\Wow6432Node\Positive Networks\PhoneFactor 이동 합니다.
2. 라는 DWORD 레지스트리 키를 만드는 **pfsvc_pendingSmsTimeoutSeconds** hello 기간 hello Azure MFA 서버 toostore 일회용 암호를 지정 하는 시간 (초)로 설정 하 고 있습니다.

>[!TIP] 
>여러 MFA 서버를 설정한 경우 hello 원래 인증 요청을 처리 하는 하나 hello toohello 사용자 보낸 hello 확인 코드를 알고 있습니다. Hello 사용자가 hello 코드를 입력할 때 hello toohello 전송 해야 하는 인증 요청 toovalidate 동일한 서버입니다. Hello 코드 유효성 검사 tooa 다른 서버에 전달 되 면 hello 인증이 거부 됩니다. 

Azure MFA 서버와 양방향 SMS에 대 한 제한 시간 설정 hello hello MFA 관리 포털에서에서 구성할 수 있습니다. 사용자가 SMS toohello hello 정의 된 제한 시간 이내에 응답 하지, 해당 인증이 거부 됩니다. 

(Hello AD FS 어댑터 또는 hello 네트워크 정책 서버 확장 프로그램 포함) hello 클라우드에서 Azure MFA를 단방향 SMS에 대 한 hello 시간 제한 설정을 구성할 수 없습니다. Azure AD는 180 초에 대 한 hello 확인 코드를 저장합니다. 

**Q: Azure Multi-factor Authentication 서버에서 하드웨어 토큰을 사용할 수 있나요?**

Azure Multi-factor Authentication 서버를 사용하는 경우 타사 OATH(공개 인증), TOTP(시간 기반, 일회용 암호) 토큰을 가져온 후 2단계 인증에 사용할 수 있습니다.

ActiveIdentity 토큰은 CSV 파일의 hello 비밀 키를 입력 하 고 tooAzure Multi-factor Authentication 서버를 가져올 TOTP OATH 토큰을 사용할 수 있습니다. Hello 사용자 입력을 허용할 수 hello 클라이언트 시스템으로 페더레이션 서비스 ADFS (Active Directory), 인터넷 정보 서버 (IIS) 폼 기반 인증을 전화 접속 사용자 서비스 RADIUS (Remote Authentication)와 OATH 토큰을 사용할 수 있습니다.

형식에 따라 hello로 제 3 자 TOTP OATH 토큰을 가져올 수 있습니다.  

- 휴대용 대칭 키 컨테이너(PSKC)  
- CSV hello 파일 일련 번호, 비밀 키 자료 32 형식에서 및 시간 간격을 포함 하는 경우  

**Q: Azure Multi-factor Authentication 서버 toosecure 터미널 서비스를 사용할 수 있습니까?**

예, 그렇지만 Windows Server 2012 R2 이상을 사용하는 경우 RD 게이트웨이(원격 데스크톱 게이트웨이)를 사용해서만 터미널 서비스의 보안을 유지할 수 있습니다.

Azure Multi-factor Authentication 서버에서 Windows Server 2012 및 이전 버전에서 toohello 로컬 보안 기관 (LSA) 보안 패키지를 연결 하는 방법을 변경 하는 Windows Server 2012 r 2의 보안 변경 내용. Windows 2012 이전의 터미널 서비스 버전의 경우 [Windows 인증으로 응용 프로그램 보호](multi-factor-authentication-get-started-server-windows.md#to-secure-an-application-with-windows-authentication-use-the-following-procedure)를 수행할 수 있습니다. Windows Server 2012 R2를 사용하는 경우 RD 게이트웨이가 필요합니다.

**Q: MFA 서버에서 발신자 ID를 구성했지만 익명 발신자로부터 Multi-Factor Authentication을 받는 사용자가 여전히 있습니다.**

Multi-factor Authentication 전화를 통해 hello 공중 전화망을 배치 하는 경우 때로는 라우팅될 때 전화 걸기 ID를 지원 하지 않는 통신 업체를 통해 이 때문에 발신자 ID 불가능할 hello Multi-factor Authentication 시스템에서 항상 보냅니다 하는 경우에 합니다.

**Q: 왜 내 사용자가 되는 증명된 tooregister의 보안 정보?**
사용자 수는 다음과 같은 경우 해당 보안 정보가 증명된 tooregister 수:

- hello 사용자는 Azure AD에서 관리자가 MFA에 대해 설정 되어 있지만 보안 정보를 아직 해당 계정에 대 한 등록 되어 있지 않습니다.
- hello 사용자 셀프 서비스 암호 재설정 Azure ad에서에 대 한 활성화 되었습니다. hello 보안 정보는 현재까지 잊어버린 hello 나중에 암호를 재설정 하는 데 도움이 됩니다.
- hello 사용자가 조건부 액세스 정책 toorequire MFA을 MFA에 대해 이전에 등록 되지 않은 응용 프로그램을 액세스 합니다.
- hello 사용자를 Azure AD (Azure AD Join 포함), 장치 등록 및 조직에서 장치 등록에 대 한 MFA 요구 하지만 hello 사용자가 MFA에 대해 이전에 등록 되지 않습니다.
- hello 사용자가 (MFA를 요구)는 Windows 10에서 비즈니스용 Windows Hello를 생성 하 고 MFA에 대 한 이전에 등록 되지 않았습니다.
- hello 조직에 만든 있고 적용 된 toohello 사용자 된 등록 MFA 정책을 활성화 합니다.
- hello 사용자는 이전에 MFA에 대 한 등록 했지만 관리자 않으므로 사용 하지 않도록 설정 확인 방법 선택 했습니다. hello 사용자 MFA 등록을 수행 해야 하므로 tooselect 새 기본 확인 방법 다시 합니다.


## <a name="errors"></a>오류
**Q: 사용자가 모바일 앱 알림을 사용할 때 "활성화된 계정에 대한 인증 요청이 아닙니다." 오류 메시지가 표시되면 사용자는 어떻게 해야 하나요?**

Toofollow 알려이 프로시저 tooremove hello 모바일 앱에서 자신의 계정을 다시 추가 합니다.

1. 너무 이동[Azure 포털 프로필](https://account.activedirectory.windowsazure.com/profile/) 조직 계정으로 로그인 합니다.
2. **추가 보안 인증**을 선택합니다.
3. Hello 모바일 앱에서 기존 계정을 hello를 제거 합니다.
4. 클릭 **구성**, 한 다음 hello 지침 tooreconfigure hello 모바일 앱을 따릅니다.

**Q: 어떻게 해야 합니까 tooa 비 브라우저 응용 프로그램에 로그인 할 때 0x800434D4L 오류 메시지를 표시 하는 경우?**

hello 0x800434D4L 오류가 표시 되는 toosign tooa 비 브라우저 응용 프로그램에서 2 단계 인증을 요구 하는 계정에서 작동 하지 않는 로컬 컴퓨터에 설치를 시도할 때 발생 합니다.

이 오류를 해결 하는 방법은 관리 관련 toohave 별도 사용자 계정에 대 한이 및 관리자가 아닌 작업 합니다. 이상 버전에서는 관리자가 아닌 계정을 사용 하 여 tooOutlook에 로그인 할 수 있도록 관리 계정과 비관리 계정 간에 사서함을 연결할 수 있습니다. 이 솔루션에 대 한 자세한 내용은 자세한 방법을 너무[관리자 hello 사용자의 사서함의 능력 tooopen 뷰와 hello 내용을 제공](http://help.outlook.com/141/gg709759.aspx?sl=1)합니다.

## <a name="next-steps"></a>다음 단계
여기에 대답 하지는 질문 hello 주석에 hello hello 페이지 맨 아래에 남겨 주세요. 또는 도움말을 얻는 몇 가지 추가 옵션은 다음과 같습니다.

* 검색 hello [Microsoft 지원 기술 자료](https://www.microsoft.com/en-us/Search/result.aspx?form=mssupport&q=phonefactor&form=mssupport) 솔루션 toocommon 기술 문제에 대 한 합니다.
* 검색 및 기술 관련 질문 및 답변 hello 커뮤니티를 검색 하거나 사용자 고유의 질문을 hello에 [Azure Active Directory 포럼](https://social.msdn.microsoft.com/Forums/azure/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required)합니다.
* 레거시 PhoneFactor 고객 본인이 궁금한 점이 있거나 암호 다시 설정 하는 데 도움이 필요한 경우 사용 하 여 hello [암호 재설정](mailto:phonefactorsupport@microsoft.com) tooopen 지원 사례를 연결 합니다.
* [Azure Multi-Factor Authentication 서버(PhoneFactor) 지원](https://support.microsoft.com/oas/default.aspx?prid=14947)을 통해 지원 전문가에게 문의하세요. 문의하는 경우 가능한 문제에 대한 많은 정보를 제공해주시면 도움이 됩니다. 정보를 제공할 수 있습니다 hello 오류 "," hello 특정 오류 코드 "," hello 특정 세션 ID "및" hello 오류 보여 준다는 사실을 알았습니다 hello 사용자의 hello ID 본 위치 hello 페이지에 포함 됩니다.

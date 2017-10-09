---
title: "고가용성을 위해 Azure MFA 서버 aaaConfigure | Microsoft Docs"
description: "고가용성을 제공하는 구성에서 Azure Multi-Factor Authentication 서버의 여러 인스턴스를 배포합니다."
services: multi-factor-authentication
keywords: Azure MFA,
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 8c6b1921c734c7a7273e443b3591fbbb15cd5e6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-high-availability"></a>고가용성을 위한 Azure Multi-Factor Authentication 서버 구성

toodeploy 해야 tooachieve 가용성이 높은 Azure 서버 MFA 배포와, 여러 MFA 서버입니다. 이 섹션에서는 정보 부하 분산 된 디자인 tooachieve Azure MFS 서버 배포 하면 대로 고가용성 목표 합니다.

## <a name="mfa-server-overview"></a>MFA 서버 개요

hello 다음 다이어그램에에서 표시 된 것 처럼 여러 가지 구성 요소를 구성 하는 hello Azure MFA 서버 서비스 아키텍처:

 ![MFA 서버 아키텍처](./media/mfa-server-high-availability/mfa-ha-architecture.png)

된 MFA 서버 hello Azure Multi-factor Authentication 소프트웨어가 설치 되어 있는 Windows 서버입니다. Azure toofunction에 MFA 서비스 hello hello와 MFA 서버 인스턴스를 활성화 해야 합니다. 온-프레미스에는 둘 이상의 MFA 서버를 설치할 수 있습니다.

설치 된 첫 번째 MFA 서버 hello hello Azure MFA 서비스 기본적으로 활성화 되 면 마스터 MFA 서버 hello 합니다. hello 마스터 MFA 서버에는 쓰기 가능한 hello PhoneFactor.pfdata 데이터베이스 복사본이 있습니다. MFA 서버 인스턴스의 후속 설치는 슬레이브라고 합니다. hello MFA 슬레이브가 hello PhoneFactor.pfdata 데이터베이스의 복제 된 읽기 전용 복사본을 갖습니다. MFA 서버는 원격 프로시저 호출(RPC)을 사용하여 정보를 복제합니다. 모든 MFA 서버 전체적으로 이어야 독립 실행형 tooreplicate 정보 또는 도메인에 가입 합니다.

MFA 마스터와 MFA 서버 슬레이브는 2 단계 인증이 필요한 경우 hello MFA 서비스와 통신 합니다. 예를 들어 사용자가 toogain 액세스 tooan 필요한 응용 프로그램을 2 단계 인증을 시도 hello 사용자는 id 공급자를 Active Directory (AD)와 같은 인증 먼저 됩니다.

AD 사용한 인증을 거친 후 MFA 서버 hello hello MFA 서비스와 통신 합니다. MFA 서버 hello hello MFA 서비스 tooallow에서 알림을 위해 대기 중이거나 hello 사용자 액세스 toohello 응용 프로그램을 거부 합니다.

Hello MFA 마스터 서버가 오프 라인인 경우 인증 들어 여전히 처리할 수 있지만 변경 내용을 toohello MFA 데이터베이스를 필요로 하는 작업을 처리할 수 없습니다. (예를 들면: hello 사용자, 셀프 서비스 PIN 변경 및 추가할 사용자 정보를 변경)

## <a name="deployment"></a>배포

Hello를 부하 분산 Azure MFA 서버 및 관련된 구성 요소에 대 한 중요 사항을 따르는 것이 좋습니다.

* **RADIUS 표준 tooachieve 고가용성을 사용 하 여**합니다. Azure MFA 서버를 RADIUS 서버로 사용하는 경우, 한 MFA 서버를 기본 RADIUS 인증 대상으로, 다른 Azure MFA 서버를 보조 인증 에이전트로 구성할 수 있습니다. 그러나이 메서드 tooachieve 고가용성 수 유용 하지 hello 보조 인증에 대해 인증 될 수 전에 hello 기본 인증 대상에서 인증에 실패 하면 시간 제한 기간 toooccur 대기 해야 하기 때문에 대상입니다. 에 hello RADIUS 클라이언트와 hello RADIUS 서버에 (이 경우 RADIUS 서버 역할을 하는 hello Azure MFA 서버) 간에 보다 효율적인 tooload 균형 hello RADIUS 트래픽을 가리킬 수 있는 단일 URL로 hello RADIUS 클라이언트를 구성할 수 있도록 합니다.
* **필요한 toomanually 승격 MFA 슬레이브가**합니다. 마스터 Azure MFA 서버 hello 오프 라인인 경우 hello 보조 Azure MFA 서버 계속 tooprocess MFA 요청 합니다. 그러나 마스터 MFA 서버 있을 때까지 관리자 사용자를 추가 또는 수정 MFA 설정 안 및 사용자가 변경할 수 없습니다 hello 사용자 포털을 사용 하 여 합니다. 승격 MFA 슬레이브 toohello 마스터 역할은 항상는 수동 프로세스입니다.
* **구성 요소의 분리성**. Azure MFA 서버에 설치할 수 있는 여러 구성 요소를 구성 하는 hello hello 동일한 Windows Server 인스턴스 또는 다른 인스턴스에서 합니다. 이러한 구성 요소는 hello 사용자 포털, 모바일 앱 웹 서비스 및 hello ad FS 어댑터 (에이전트)를 포함 합니다. 이 separability 하면 가능한 toouse hello 웹 응용 프로그램 프록시 toopublish hello 사용자 포털 및 모바일 앱 웹 서버 hello 경계 네트워크에서 있습니다. 이러한 구성 추가 toohello hello 다음 다이어그램에에서 표시 된 대로 디자인의 전반적인 보안 합니다. hello MFA 사용자 포털 및 모바일 앱 웹 서버는 HA 부하 분산 된 구성에도 배포 될 수 있습니다.

   ![경계 네트워크와 MFA 서버](./media/mfa-server-high-availability/mfasecurity.png)

* **트래픽이 부하 분산 되는 경우 OTP (일회용 암호)를 통해 SMS (즉, 단방향 SMS)은 hello 고정 세션 사용 하 여**합니다. 단방향 SMS는 인증 옵션을 사용 하면 hello와 MFA 서버 toosend hello 사용자가 OTP를 포함 하는 텍스트 메시지입니다. hello 사용자 프롬프트 창 toocomplete hello MFA 챌린지의에서 hello OTP를 입력합니다. 잔액 Azure MFA 서버를 로드 하는 경우 hello 동일한 서버 hello 초기 인증 요청을 처리 하는 서버 여야 합니다 hello 메시지를 받는 hello OTP hello 사용자;에서 hello 회신 OTP 수신 하는 다른 MFA 서버 hello 인증 챌린지 실패 합니다. 자세한 내용은 참조 [SMS 추가 tooAzure MFA 서버를 통해 한 번 암호](https://blogs.technet.microsoft.com/enterprisemobility/2015/03/02/one-time-password-over-sms-added-to-azure-mfa-server)합니다.
* **Hello 사용자 포털 및 모바일 앱 웹 서비스의 부하 분산 배포에서 고정 세션 필요한**합니다. 부하 분산 하려는 경우 사용자 포털 MFA hello 및 hello 모바일 앱 웹 서비스, 각 세션 요구 toostay hello에 동일한 서버입니다.

## <a name="high-availability-deployment"></a>고가용성 배포

hello 다음 다이어그램 보여 줍니다 Azure MFA 및 해당 구성 요소 참조에 대 한 ad FS와의 전체 HA 부하 분산 된 구현.

 ![Azure MFA 서버 HA 구현](./media/mfa-server-high-availability/mfa-ha-deployment.png)

다음 hello에 대 한 항목을까지 참고 hello 번호가 hello 다이어그램 앞의 영역을 지정 됩니다.

1. 두 Azure MFA 서버 (MFA1 및 MFA2)는 hello을 균형 잡힌된 (mfaapp.contoso.com)를 로드 하는 구성 된 toouse 정적 포트 (4443) tooreplicate hello PhoneFactor.pfdata 데이터베이스. 웹 서비스 SDK hello hello ADFS 서버와 TCP 포트 443 통해 각 hello MFA 서버 tooenable 통신에 설치 됩니다. hello MFA 서버는 상태 비저장 부하 분산 된 구성에 배포 됩니다. 그러나 toouse OTP SMS 통해 하려는 경우 상태 저장 부하 분산 사용 해야 합니다.
   ![Azure MFA 서버 - 앱 서버 HA](./media/mfa-server-high-availability/mfaapp.png)

   > [!NOTE]
   > RPC 동적 포트를 사용 하므로 toohello RPC 사용할 수 있도록 동적 포트 범위를 tooopen 방화벽은 권장 되지 않습니다. 방화벽이 있는 경우 **사이의** MFA 응용 프로그램 서버를 구성 해야 hello와 MFA 서버 toocommunicate hello 복제 트래픽 슬레이브와 마스터 서버 간 및 오픈 해당 포트에 대 한 정적 포트에서 방화벽에 있습니다. DWORD 레지스트리 값을 만들어 hello 정적 포트를 강제할 수 있습니다 ```HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Positive Networks\PhoneFactor``` 호출 ```Pfsvc_ncan_ip_tcp_port``` 및 정적 포트를 사용할 수 있는 tooan hello 값을 설정 합니다. 연결이 항상 hello 종속 MFA 서버 toohello 마스터에서 시작, hello 정적 포트 hello 마스터에만 필요 필요가 없으며 모든 MFA 서버에서 hello 정적 포트를 설정 해야 이후 언제 든 지 종속 toobe hello 마스터 승격할 수 있습니다.

2. hello 두 사용자 포털/MFA 모바일 응용 프로그램 서버 (MFA-위쪽-MAS1 및 MFA-위쪽-MAS2) 부하에 분산 되는 **stateful** (mfa.contoso.com) 구성 합니다. 한다는 점에 유의 하세요 고정 세션 부하 분산 hello MFA 사용자 포털 및 모바일 응용 프로그램 서비스에 대 한 요구 사항입니다.
   ![Azure MFA 서버 - 사용자 포털 및 Mobile App Service HA](./media/mfa-server-high-availability/mfaportal.png)
3. hello ad FS 서버 팜 부하 분산 및 부하 분산 된 ADFS 프록시를 통해 인터넷 toohello hello 경계 네트워크에 게시 됩니다. 각 ad FS 서버 TCP 포트 443 통해 단일 부하 분산 된 URL (mfaapp.contoso.com)를 사용 하 여 Azure MFA 서버 hello로 hello ADFS 에이전트 toocommunicate를 사용 합니다.

## <a name="next-steps"></a>다음 단계

* [Azure MFA 서버 설치 및 구성](multi-factor-authentication-get-started-server.md)

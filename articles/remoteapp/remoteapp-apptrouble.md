---
title: "RemoteApp 문제 해결-aaaAzure 응용 프로그램 실행 및 연결 오류 | Microsoft Docs"
description: "시작 주소와 연결 하는 Azure RemoteApp에서 tooapplications tootroubleshoot 발급 하는 방법에 대해 알아봅니다."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e5cf7171-d1c2-4053-a38b-5af7821305e1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e51d480c9d3fa1f2076f95b63c7a8cd2f6956a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a>Azure RemoteApp 문제 해결 - 응용 프로그램 시작 및 연결 실패
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

Azure RemoteApp에서 호스팅되는 응용 프로그램은 몇 가지 다른 이유로 toolaunch를 실패할 수 있습니다. 이 문서에서는 다양 한 이유를 설명 하 고 오류 메시지 사용자 때 표시 될 수 toolaunch 응용 프로그램을 시도 합니다. 또한 연결 실패에 대해서도 설명합니다. 그러나 Azure RemoteApp 클라이언트 hello에 로그인 할 경우이 문서의 문제를 설명 하지 않습니다.  

Tooapp 시작 및 연결 오류 때문에 일반 오류 메시지에 대 한 내용은 읽습니다.

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a>설정 중입니다... 10분 후에 다시 시도하세요.
이 오류는 Azure RemoteApp의 사용자 toomeet hello 용량 필요 확장은 의미 합니다. Hello 백그라운드에서 더 많은 Azure RemoteApp VM 인스턴스 사용자의 toohandle hello 용량 요구 만들고 있습니다. 일반적으로이 분 정도 걸리지만 too10 분 정도 걸릴 수 있습니다. 경우에 따라 신속하게 진행되지 않아 즉시 리소스가 필요할 수 있습니다. 예를 들어 많은 필요한 toouse 이러한 앱에서 Azure RemoteAppn hello에서 오전 9 시 시나리오 동시 합니다. 설정 가능 tooyou 이런 경우가 발생 하는 경우 **용량 모드** hello에 백 엔드 합니다. 이 열려 있는 한 Azure 지원 티켓 toodo 합니다. 특정 tooinclude hello 요청에서 구독 ID 수입니다.  

![설정 중입니다.](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-tooyour-applications-please-re-launch-your-application"></a>자동으로 다시 연결 하지 못했습니다 tooyour 응용 프로그램을 실행 하세요. 다시 응용 프로그램
Azure RemoteApp을 사용 하 던 하 고 다음 4 시간을 초과 하 여 PC toosleep를 입력 하 고 다음 절전 PC 모드에서 해제 하 고 hello Azure RemoteApp 클라이언트 시도 tooauto 다시 연결 하 고 제한 시간이 초과 되었습니다에 자주이 오류 메시지가 표시 됩니다.  사용자가 toonavigate 백 toohello 응용 프로그램에 지시 하 고 tooopen 시도 hello Azure RemoteApp 클라이언트에서.

![자동으로 다시 연결 하지 못했습니다 tooyour 응용 프로그램](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-hello-temp-profile"></a>임시 프로필 hello에 문제가 있습니다.
이 오류는 사용자 프로필 (사용자 프로필 디스크) toomount를 실패 하 고 hello 사용자 임시 프로필을 받을 때 발생 합니다.  관리자는 hello Azure 포털에서에서 toohello 컬렉션을 이동 하 고 이동 하 여 toohello **세션** 탭 및 너무 시도**로그 오프** hello 사용자입니다. Hello 사용자 세션-오프 전체 로그를 강제로 후 다시 hello 사용자 시도 toolaunch 앱이 있는 합니다. 실패한 경우 Azure 지원에 문의하세요.

## <a name="azure-remoteapp-has-stopped-working"></a>Azure RemoteApp의 작동이 중지되었습니다.
이 오류 메시지는 hello Azure RemoteApp 클라이언트는 문제가 발생 하 고 toobe 다시 시작을 의미 합니다. 사용자가 tooclose 지시: 선택 **프로그램 닫기** 다음 hello Azure RemoteApp 클라이언트를 다시 실행 합니다.  Hello 문제가 열기 및 Azure 지원 티켓을 계속 합니다.

![Azure RemoteApp의 작동이 중지되었습니다.](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-hello-connection-or-contact-your-system-administrator"></a>원격 데스크톱 연결이 이 리소스에 액세스하는 동안 오류가 발생했습니다. Hello 연결을 다시 시도 하거나 시스템 관리자에 게 문의
일반 오류 메시지입니다. 조사할 수 있도록 Azure 지원에 문의하세요. 

![일반 Azure RemoteApp 메시지](./media/remoteapp-apptrouble/ra-apptrouble4.png) 


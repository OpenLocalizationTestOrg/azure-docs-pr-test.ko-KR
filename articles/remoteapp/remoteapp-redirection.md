---
title: "Azure RemoteApp에서 aaaUsing 리디렉션 | Microsoft Docs"
description: "자세한 내용은 방법 RemoteApp에서 사용 하 여 tooconfigure 리디렉션"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a>Azure RemoteApp에서 리디렉션 사용
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

장치 리디렉션 hello 장치 연결 된 tootheir 로컬 컴퓨터, 휴대폰 또는 태블릿을 사용 하 여 원격 응용 프로그램과 상호 작용할 사용자가 수 있습니다. 예를 들어 Azure RemoteApp을 통해 Skype를 제공한 경우 사용자 자신의 PC toowork Skype로에 설치 하는 hello 카메라가 필요 합니다. 프린터, 스피커, 모니터 및 USB로 연결된 다양한 주변 장치의 경우도 마찬가지입니다.

RemoteApp은 hello 프로토콜 RDP (원격 데스크톱)과 RemoteFX tooprovide 리디렉션을 활용합니다.

## <a name="what-redirection-is-enabled-by-default"></a>기본적으로 사용할 수 있는 리디렉션
RemoteApp을 사용 하는 경우 리디렉션을 수행 하는 hello 기본적으로 활성화 됩니다. 괄호 안에 hello 정보 hello RDP 설정을 보여 줍니다.

* Hello 로컬 컴퓨터에서 소리 재생 (**이 컴퓨터에서 재생**). (audiomode:i:0)
* Hello 로컬 컴퓨터와 송신 toohello 원격 컴퓨터에서 오디오 캡처 (**이 컴퓨터에서 레코드**). (audiocapturemode:i:1)
* 인쇄 toolocal 프린터 (redirectprinters:i:1)
* COM 포트(redirectcomports:i:1)
* 스마트 카드 장치(redirectsmartcards:i:1)
* (기능 toocopy 및 붙여넣기) 클립보드 (redirectclipboard:i:1)
* 암호화되지 않은 형식 글꼴 다듬기(allow font smoothing:i:1)
* 지원되는 모든 플러그 앤 플레이 장치 리디렉션 (devicestoredirect:s:*)

## <a name="what-other-redirection-is-available"></a>사용할 수 있는 기타 리디렉션
기본적으로 다음 두 가지 리디렉션 옵션은 사용하지 않도록 설정되어 있습니다.

* 드라이브의 리디렉션을 (드라이브 매핑): 로컬 컴퓨터의 드라이브 될 hello 원격 세션에서 매핑된 드라이브입니다. Hello 원격 세션에서 작업 하는 동안 저장 하면 또는 로컬 드라이브에서 열려 있는 파일 있습니다.
* USB 리디렉션을: hello 원격 세션 내에서 hello USB 장치 연결 된 tooyour 로컬 컴퓨터를 사용할 수 있습니다.

## <a name="change-your-redirection-settings-in-remoteapp"></a>RemoteApp에서 리디렉션 설정 변경
SDK와 Microsoft Azure PowerShell hello를 사용 하 여 컬렉션에 대 한 hello 장치 리디렉션 설정을 변경할 수 있습니다. 설치한 후 새 PowerShell 및 SDK hello, 먼저에 설명 된 구독 toomanage 구성 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

그런 다음 다음 RDP 속성이 사용자 지정 tooset hello 명령 비슷한 toohello를 사용 합니다.

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

(유의  *`n*  개별 속성 사이의 구분 기호로 사용 됩니다.)

tooget RDP 속성 사용자 지정 구성 된 목록을 hello 다음 cmdlet을 실행 합니다. 만 사용자 지정 속성 출력 결과 표시 되 고 기본 속성을 hello 하지 note:  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

사용자 지정 속성을 설정 하는 경우 모든 사용자 지정 속성을 지정 해야 때마다; 그렇지 않으면 hello 설정을 toodisabled가 되돌립니다.   

### <a name="common-examples"></a>일반적인 예
다음 cmdlet tooenable 드라이브 리디렉션 hello를 사용 합니다.  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

이 cmdlet tooenable를 사용 하 여 USB 및 드라이브 모두 리디렉션:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

이 cmdlet toodisable 클립보드 공유를 사용 합니다.  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> 있는지 toocompletely 로그 오프 hello 컬렉션의 모든 사용자 수 (및 뿐 아니라 연결 끊기) hello 변경을 테스트 하기 전에. tooensure 사용자가 로그 오프, 이동 toohello 완전히 **세션** hello Azure 포털의에서 hello 컬렉션에 탭을 분리 하거나 로그인 모든 사용자를 로그 오프 합니다. 경우에 따라이 지나야 hello 로컬 드라이브 tooshow 몇 초 정도 탐색기에서 hello 세션 내에서.
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a>Windows 클라이언트에서 USB 리디렉션 설정 변경
TooRemoteApp 연결 하는 컴퓨터에서 USB 리디렉션을 toouse를 원하는 경우 toohappen 해야 하는 두 작업을 합니다. 1-관리자는 Azure PowerShell을 사용 하 여 tooenable USB 리디렉션을 hello 컬렉션 수준에서 필요 합니다. 2-toouse USB 리디렉션을 원하는 각 장치에서 tooenable에서 허용 하는 그룹 정책이 필요 합니다. 이 단계는 toobe toouse USB 리디렉션을가 하는 각 사용자에 대해 수행 해야 합니다.

> [!NOTE]
> Azure RemoteApp을 사용한 USB 리디렉션은 Windows 컴퓨터에서만 지원됩니다.
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a>Hello RemoteApp 컬렉션에 대 한 USB 리디렉션을 사용 하도록 설정
Hello cmdlet tooenable USB 리디렉션을 hello 모음 수준에서 다음을 사용 합니다.

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a>Hello 클라이언트 컴퓨터에 대 한 USB 리디렉션을 사용 하도록 설정
컴퓨터에 tooconfigure USB 리디렉션 설정:

1. 열기 hello 로컬 그룹 정책 편집기 (GPEDIT 합니다. MSC)입니다. 명령 프롬프트에서 gpedit.msc를 실행하면 됩니다.
2. **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**을 엽니다.
3. **이 컴퓨터에서 지원되는 기타 RemoteFX USB 장치의 RDP 리디렉션 허용**을 두 번 클릭합니다.
4. 선택 **Enabled**를 선택한 후 **hello RemoteFX USB 리디렉션을 액세스 권한에서에서 관리자와 사용자**합니다.
5. 관리자 권한으로 명령 프롬프트를 열고 hello 다음 명령을 실행 합니다.
   
        gpupdate /force
6. Hello 컴퓨터를 다시 시작 합니다.

그룹 정책 관리 도구 toocreate hello를 사용 하 여 하 고 도메인의 모든 컴퓨터에 대 한 hello USB 리디렉션 정책을 적용할 수도 있습니다.

1. 도메인 관리자에 게도 hello 도메인 컨트롤러에 로그인 합니다.
2. Hello 그룹 정책 관리 콘솔을 엽니다. **시작 > 관리 도구 > 그룹 정책 관리**를 클릭하면 됩니다.
3. Toohello 도메인 또는 조직 구성 단위 toocreate hello 정책 원하는 이동 합니다.
4. **기본 도메인 정책**을 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다.
5. **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**을 엽니다.
6. **이 컴퓨터에서 지원되는 기타 RemoteFX USB 장치의 RDP 리디렉션 허용**을 두 번 클릭합니다.
7. 선택 **Enabled**를 선택한 후 **hello RemoteFX USB 리디렉션을 액세스 권한에서에서 관리자와 사용자**합니다.
8. **확인**을 클릭합니다.  


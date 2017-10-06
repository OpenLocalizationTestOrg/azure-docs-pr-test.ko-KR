---
title: "aaaRun Azure RemoteApp과 함께 모든 장치에서 모든 Windows 앱 | Microsoft Docs"
description: "자세한 내용은 방법 tooshare Azure RemoteApp을 사용 하 여 사용자와 모든 Windows 앱."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 961d40ca-9673-4977-aa54-d6b22fc61ce1
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 750f3b881e0cb671ff6e8f3e851bccdf2262d156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-any-windows-app-on-any-device-with-azure-remoteapp"></a>Azure RemoteApp을 사용하여 모든 장치에서 Windows 앱 실행
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

어디서든 모든 장치에서 Azure RemoteApp을 사용하여 지금 바로 Windows 응용 프로그램을 실행할 수 있습니다. 10 년 전에 작성 된 사용자 지정 응용 프로그램 또는 Office 앱 여부, 사용자는 더 이상 연결 toobe tooa 특정 운영 체제 (예: Windows XP) 응용 프로그램의 몇 가지가 없습니다.

Azure RemoteApp과 함께 사용자가 자신의 Android 사용할 수도 또는 Apple 장치 및 get hello 환경이 동일 하 고 Windows에서 (또는 Windows phone)를 가져왔습니다. 이렇게 하려면 인터넷이 연결된 어디에서나 액세스 가능한 Azure 기반 Windows 가상 컴퓨터 컬렉션에서 Windows 응용 프로그램을 호스트합니다. 

읽기에 대 한 예제 정확히 어떻게 toodo이 있습니다.

이 문서에서 모든 사용자에 게 액세스 tooshare를 하겠습니다. 그러나 모든 응용 프로그램을 사용할 수 있습니다. Windows Server 2012 R2 컴퓨터에 앱을 설치할 수 있습니다,으로 다음 hello 단계를 사용 하 여 공유할 수 있습니다. Hello를 검토할 수 있습니다 [응용 프로그램 요구 사항](remoteapp-appreqs.md) toomake 있는지 응용 프로그램은 작동 합니다.

하십시오는 액세스 데이터베이스가 고 해당 데이터베이스 toobe 유용한 원하는 때문에 여기서 하 게 될 것 몇 가지 추가 단계 toolet 사용자 참고 hello 액세스 데이터 공유에 액세스 합니다. 응용 프로그램 데이터베이스에 없거나 실행 하 여 사용자가 toobe 수 tooaccess 파일 공유를 필요 하지 않습니다, 하는 경우이 자습서에서는 이러한 단계를 건너뛸 수 있습니다.

> [!NOTE]
> <a name="note"></a>이 자습서는 Azure 계정 toocomplete 필요합니다.
> 
> * 할 수 있습니다 [무료로 Azure 계정을 개설](https://azure.microsoft.com/free/?WT.mc_id=A261C142F): 크레딧을 얻게 유료 Azure 서비스 아웃 tootry 사용할 수 있으며 사용 후에 최대 hello 계정 등에 사용 하 여 웹 사이트와 같은 Azure 서비스를 해제 합니다. 명시적으로 설정을 변경 하 고 청구 toobe 요청 하지 않는 한 신용 카드, 청구 됩니다 하지 않습니다.
> * [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있음: MSDN 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.
> 
> 

## <a name="create-a-collection-in-remoteapp"></a>RemoteApp에서 컬렉션 만들기
먼저 컬렉션을 만듭니다. hello 컬렉션 앱과 사용자에 대 한 컨테이너 역할을 합니다. 각 컬렉션은 이미지를 기반으로 하며, 컬렉션을 직접 만들거나 구독과 함께 제공된 컬렉션을 사용할 수 있습니다. 이 자습서에서는 hello Office 2013 평가판 이미지 사용-tooshare 한다고 hello 앱을 포함 합니다.

1. Hello Azure 포털에서에서 아래로 hello 왼쪽 탐색 트리 RemoteApp 나타날 때까지 합니다. 해당 페이지를 엽니다.
2. **RemoteApp 컬렉션 만들기**를 클릭합니다.
3. **빠른 생성** 을 클릭하고 컬렉션의 이름을 입력합니다.
4. Toouse toocreate 컬렉션을 원하는 hello 지역을 선택 합니다. Hello 최상의 경험에 대 한 지리적으로 가장 가까운 hello 지역을 선택 하면 사용자가 hello 앱에 액세스 하는 toohello 위치입니다. 예를 들어이 자습서에서는 hello 사용자 워싱턴의 레드몬드에서 배치 됩니다. 가장 가까운 Azure 지역을 hello **West US**합니다.
5. 원하는 toouse hello 청구 계획을 선택 합니다. hello 기본 청구 계획 hello 표준 요금제 큰 Azure VM에서 10 명의 사용자가에 있을 때 큰 Azure VM에서 16 명의 사용자가 넣습니다. 일반적인 예로, hello 기본 계획 데이터 항목 유형 워크플로에 대 한 간단 하 게 합니다. Office와 같은 생산성 응용 프로그램에 대 한 hello 표준 계획을 사용할 수 있습니다.
6. 마지막으로 hello Office 2013 Professional 이미지를 선택 합니다. 이 이미지는 Office 2013 앱을 포함합니다. 미리 알림 - 이 이미지는 평가판 컬렉션 및 POC에만 유효합니다. 프로덕션 컬렉션에는 이 이미지를 사용할 수 없습니다.
7. 이제 **RemoteApp 컬렉션 만들기**를 클릭합니다.

![RemoteApp에서 클라우드 컬렉션 만들기](./media/remoteapp-anyapp/ra-anyappcreatecollection.png)

컬렉션을 만드는 시작 하지만 tooan 1 시간 정도 걸릴 수 있습니다.

하면 이제 사용자에 게 준비 tooadd 하 합니다.

## <a name="share-hello-app-with-users"></a>사용자와 공유 hello 앱
컬렉션을 만든 후에 성공적으로, 시간 toopublish 액세스 toousers 이며 액세스 tooit 가져야 하는 hello 사용자를 추가 합니다.

탐색 하면 hello Azure RemoteApp 노드 반대쪽 hello 컬렉션 만들어지는 동안, 이때 tooit hello Azure 홈 페이지에서에서 백업 하 여 시작 합니다.

1. 이전 tooaccess 추가 옵션을 생성 하는 hello 컬렉션을 클릭 하 고 hello 컬렉션을 구성 합니다.
   ![새 RemoteApp 클라우드 컬렉션](./media/remoteapp-anyapp/ra-anyappcollection.png)
2. Hello에 **게시** 탭을 클릭 **게시** hello 화면을 클릭 한 다음 hello 맨 아래에 **게시할 시작 메뉴 프로그램**합니다.
   ![RemoteApp 프로그램 게시](./media/remoteapp-anyapp/ra-anyapppublish.png)
3. Toopublish hello 목록에서 원하는 hello 앱을 선택 합니다. 여기서는 Access를 선택합니다. 페이지 맨 아래에 있는 **완료**을 참조하세요. Hello 앱 toofinish 게시 될 때까지 기다립니다.
   ![RemoteApp에서 Access 게시](./media/remoteapp-anyapp/ra-anyapppublishaccess.png)
4. Hello 앱 게시 완료 되 면 toohello 통해 head **사용자 액세스** tooadd tooyour 앱에 액세스 해야 하는 모든 hello 사용자가 탭 합니다. 사용자의 사용자 이름(메일 주소)을 입력한 다음 **저장**을 클릭합니다.

![사용자가 tooRemoteApp 추가](./media/remoteapp-anyapp/ra-anyappaddusers.png)

1. 시간 tootell는 이제 이러한 새 응용 프로그램에 대 한 사용자와 방법을 tooaccess 해당 합니다. toodo이를 사용자에 게 toohello 원격 데스크톱 클라이언트 다운로드 URL을 가리키는 전자 메일을 보냅니다.
   ![RemoteApp에 대 한 URL을 다운로드 하는 hello 클라이언트](./media/remoteapp-anyapp/ra-anyappurl.png)

## <a name="configure-access-tooaccess"></a>액세스 tooAccess 구성
일부 앱은 RemoteApp을 통해 배포한 이후에 추가 구성이 필요합니다. 특히, 액세스에 대 한 모든 사용자가 액세스할 수 있는 Azure에서 파일 공유는 지속적인 toocreate 하 합니다. (Toodo 않으려면를 만들 수 있습니다는 [하이브리드 컬렉션](remoteapp-create-hybrid-deployment.md) 업체 클라우드 컬렉션] [대신 사용자가 수 있는 파일 및 로컬 네트워크에 대 한 정보에 액세스 합니다.) 그런 다음 해야 tootell 우리의 사용자 toomap 자신의 컴퓨터 toohello Azure 파일 시스템의 로컬 드라이브입니다.

admin 님 안녕하세요도 작업을 수행한 hello 첫 번째 부분입니다. 그런 다음 사용자를 위해 몇 가지 단계를 수행합니다.

1. 게시 hello 명령줄 인터페이스 (cmd.exe)에서 시작 합니다. Hello에 **게시** 탭에서 **cmd**, 클릭 하 고 **게시 > 경로 사용 하 여 게시 프로그램**합니다.
2. Hello 응용 프로그램의 성능과 hello 경로 hello 이름을 입력 합니다. 이러한 목적에 대 한 "파일 탐색기" hello 이름 및 "%SYSTEMDRIVE%\windows\explorer.exe" hello 경로로 사용 합니다.
   ![Hello cmd.exe 파일을 게시 합니다.](./media/remoteapp-anyapp/ra-publishcmd.png)
3. 이제 Azure toocreate 필요한 [저장소 계정](../storage/common/storage-create-storage-account.md)합니다. 우리 "accessstorage" 이름을 따라서 tooyou 의미 있는 이름을 선택 합니다. (toomisquote Highlander, "accessstorage." 하나만 있을 수 있습니다) ![Our Azure 저장소 계정](./media/remoteapp-anyapp/ra-anyappazurestorage.png)
4. 이제 돌아가서 tooyour 대시보드 하므로 hello 경로 tooyour 저장소 (끝점 위치) 발생할 수 있습니다. 한 동안 이 경로를 사용할 것이므로 경로를 다른 곳에 복사해 두세요.
   ![hello 저장소 계정 경로](./media/remoteapp-anyapp/ra-anyappstoragelocation.png)
5. 다음으로 hello 저장소 계정이 생성 된 후에 hello 기본 액세스 키가 필요 합니다. 클릭 **액세스 키 관리**, 및 hello 기본 액세스 키를 복사 합니다.
6. 이제, hello 저장소 계정의 hello 컨텍스트를 설정 하 고 액세스를 위한 새 파일 공유 만들기 합니다. 관리자 권한 Windows PowerShell 창에서 cmdlet 뒤 hello를 실행 합니다.
   
        $ctx=New-AzureStorageContext <account name> <account key>
        $s = New-AzureStorageShare <share name> -Context $ctx
   
    이 공유에 대 한 이러한 기능은 hello cmdlet을 실행 합니다.
   
        $ctx=New-AzureStorageContext accessstorage <key>
        $s = New-AzureStorageShare <share name> -Context $ctx

이제 hello 사용자 설정의 것입니다. 먼저 사용자가 [RemoteApp 클라이언트](remoteapp-clients.md)를 설치해야 합니다. 다음으로 hello 사용자가 자신의 계정 toothat Azure 파일에서에서 드라이브를 공유 사용자가 만든 toomap 필요 하 고 파일의 액세스를 추가 합니다. 작업 방법은 다음과 같습니다.

1. Hello RemoteApp 클라이언트 액세스 hello 앱을 게시 합니다. Hello cmd.exe 프로그램을 시작 합니다.
2. 컴퓨터 toohello 파일 공유에서 다음 명령을 toomap hello 드라이브를 실행 합니다.
   
        net use z: \\<accountname>.file.core.windows.net\<share name> /u:<user name> <account key>
   
    Hello를 설정한 경우 **영구 /** 매개 변수 tooyes hello 매핑된 드라이브 세션 간에 유지 됩니다.
3. 이제, RemoteApp에서 hello 파일 탐색기 앱을 시작 합니다. Toouse hello 공유 앱 toohello 파일 공유에 대 한 액세스 파일을 복사 합니다.
   ![Azure 공유에 Access 파일 넣기](./media/remoteapp-anyapp/ra-anyappuseraccess.png)
4. 마지막으로, Access를 열고 방금 공유 hello 데이터베이스를 엽니다. Hello 클라우드에서 실행 되는 액세스의 데이터 표시 되어야 합니다.
   ![Hello 클라우드에서 실행 되는 실제 Access 데이터베이스](./media/remoteapp-anyapp/ra-anyapprunningaccess.png)

이제 RemoteApp 클라이언트를 설치한 모든 장치에서 Access를 사용할 수 있습니다.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>다음 단계
지금까지 컬렉션을 만드는 방법을 살펴보았으므로 이제 [Office 365를 사용하는 컬렉션](remoteapp-tutorial-o365anywhere.md)을 만들어 보겠습니다. 또는 로컬 네트워크에 액세스할 수 있는 [하이브리드 컬렉션 ](remoteapp-create-hybrid-deployment.md)을 만들 수 있습니다.

<!--Image references-->


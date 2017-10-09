---
title: "aaaDebugging Azure 클라우드 서비스 또는 Visual Studio에서 가상 컴퓨터 | Microsoft Docs"
description: "Visual Studio에서 클라우드 서비스 또는 가상 컴퓨터 디버깅"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 945e06e0-2100-41af-b218-72347367ddab
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 32a326430021ba2ea9317a6a71fa005d4b87c273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-an-azure-cloud-service-or-virtual-machine-in-visual-studio"></a>Visual Studio에서 Azure 클라우드 서비스 또는 가상 컴퓨터 디버깅
Visual Studio는 Azure 클라우드 서비스와 가상 컴퓨터 디버깅에 여러 가지 옵션을 제공합니다.

## <a name="debug-your-cloud-service-on-your-local-computer"></a>로컬 컴퓨터에서 클라우드 서비스 디버그
저장할 수 있습니다 시간과 비용 hello Azure 계산 에뮬레이터 toodebug를 사용 하 여 클라우드 서비스는 로컬 컴퓨터에서. 배포하기 전에 로컬로 서비스를 디버깅하면, 계산 시간이 소요되지 않고 안정성과 성능을 향상할 수 있습니다. 그러나, Azure 자체에서 클라우드 서비스를 실행하는 경우, 일부 오류가 발생할 수 있습니다. 서비스를 게시 한 다음 hello 디버거 tooa 역할 인스턴스를 연결 하는 경우 원격 디버깅을 사용 하는 경우 이러한 오류를 디버그할 수 있습니다.

hello 에뮬레이터 hello Azure 계산 서비스를 시뮬레이션 하 고 테스트 하 고 배포 하기 전에 클라우드 서비스를 디버그할 수 있도록 로컬 환경에서 실행 됩니다. hello 에뮬레이터 핸들의 역할 인스턴스 수명 주기 hello 및 toosimulated 주고받는 로컬 저장소 액세스를 제공 합니다. 를 디버그 하거나 Visual Studio에서 서비스를 실행 하는 경우 자동으로 hello 에뮬레이터를 백그라운드 응용 프로그램으로 시작 하 고 그런 다음 서비스 toohello 에뮬레이터에 배포 합니다. Hello 로컬 환경에서 실행 될 때 서비스 hello 에뮬레이터 tooview을 사용할 수 있습니다. Hello 정식 버전 또는 hello 에뮬레이터의 hello express 버전을 실행할 수 있습니다. (Azure 2.3부터 express 버전의 hello 에뮬레이터 hello hello 기본값입니다.) 참조 [Emulator Express를 사용 하 여 tooRun 및 클라우드 서비스를 로컬로 디버그](https://msdn.microsoft.com/library/dn339018.aspx)합니다.

### <a name="toodebug-your-cloud-service-on-your-local-computer"></a>toodebug 로컬 컴퓨터의 클라우드 서비스
1. Hello 메뉴 모음에서 **디버그**, **디버깅 시작** toorun Azure 클라우드 서비스 프로젝트입니다. F5를 눌러도 디버깅을 시작할 수 있습니다. 계산 에뮬레이터의 hello 메시지를 시작 하는 것을 볼 수 있습니다. Hello 에뮬레이터를 시작할 때 hello 시스템 트레이 아이콘이를 확인 합니다.

    ![Hello 시스템 트레이의 azure 에뮬레이터](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC783828.png)
2. Hello 알림 영역에서 Azure 아이콘 hello에 대 한 hello 바로 가기 메뉴를 열고 hello 계산 에뮬레이터에 대 한 hello 사용자 인터페이스를 표시 한 다음 선택 **계산 에뮬레이터 UI 표시**합니다.

    hello hello UI의 왼쪽된 창에서는 현재 hello 서비스 toohello 계산 에뮬레이터와 hello 역할 인스턴스 각 서비스를 실행 하는 배포를 보여 줍니다. Hello 오른쪽 창에 hello 서비스 또는 역할 toodisplay 수명 주기, 로깅 및 진단 정보를 선택할 수 있습니다. 에 포함 된 창의 위쪽 여백 hello hello 포커스를 둔 toofill hello 오른쪽 창을 확장 됩니다.
3. Hello에 명령을 선택 하 여 hello 응용 프로그램을 통해 단계 **디버그** 메뉴와 사용자 코드에서 중단점을 설정 합니다. Hello 디버거에서 hello 응용 프로그램을 통해 실행할 때는 hello hello 응용 프로그램의 현재 상태와 함께 hello 창이 업데이트 됩니다. 디버깅을 중지 하면 hello 응용 프로그램 배포가 삭제 됩니다. 응용 프로그램에 웹 역할이 포함 하는 경우 hello 시작 작업 속성 toostart hello 웹 브라우저 설정 하면 Visual Studio hello 브라우저에서 웹 응용 프로그램을 시작 합니다. Hello hello 서비스 구성에서 역할의 인스턴스 수를 변경 하면 클라우드 서비스를 중지 하 고 hello 역할의 이러한 새 인스턴스를 디버깅할 수 있도록 디버깅 다시 시작 해야 합니다.

    **참고:** 실행을 중지 하거나 로컬 계산 에뮬레이터 및 저장소 에뮬레이터 hello 서비스, 디버깅 중지 되지 않습니다. Hello 알림 영역에서 해당 작업을 명시적으로 중지 해야 있습니다.

## <a name="debug-a-cloud-service-in-azure"></a>Azure에서 클라우드 서비스 디버그
toodebug 원격 컴퓨터에서 클라우드 서비스를 활성화 해야 해당 기능 명시적으로 필요한 서비스 (예: msvsmon.exe) 역할 인스턴스를 실행 하는 hello 가상 컴퓨터에 설치 되어 있도록 클라우드 서비스를 배포 하는 경우. Hello 서비스를 게시할 때 원격 디버깅을 사용 하지 않은 경우 원격 디버깅 사용 toorepublish hello 서비스를 수 있습니다.

클라우드 서비스에 원격 디버깅을 사용하면, 성능이 저하되거나 추가 요금이 발생하지 않습니다. Hello 서비스를 사용 하는 클라이언트에 문제가 발생할 수 있으므로 프로덕션 서비스에서 원격 디버깅을 사용 하 여이 하지 않아야 합니다.

> [!NOTE]
> Visual Studio에서 클라우드 서비스를 게시할 때 설정할 수 있습니다 **IntelliTrace** 하의 모든 역할 서비스를 해당 대상 hello.NET Framework 4 또는.NET Framework 4.5 hello에 대 한 합니다. 사용 하 여 **IntelliTrace**, hello 과거에 역할 인스턴스에서 발생 한 이벤트를 검토 하 고 그 시점부터 hello 컨텍스트를 재현할 수 있습니다. [IntelliTrace 및 Visual Studio를 사용하여 게시된 클라우드 서비스 디버깅](http://go.microsoft.com/fwlink/?LinkID=623016) 및 [IntelliTrace 사용하기](https://msdn.microsoft.com/library/dd264915.aspx)를 참조하세요.
>
>

### <a name="tooenable-remote-debugging-for-a-cloud-service"></a>원격 디버깅을 클라우드 서비스에 대 한 tooenable
1. Hello Azure 프로젝트에 대 한 hello 바로 가기 메뉴를 연 다음 선택 **게시**합니다.
2. 선택 hello **준비** 환경과 hello **디버그** 구성 합니다.

    단지 지침일 뿐입니다. 프로덕션 환경에서 테스트 환경을 toorun를 선택할 수 있습니다. 그러나 하면 성능이 저하 될 수 hello 프로덕션 환경에서 원격 디버깅을 사용 하는 경우. Hello 릴리스 구성을 선택할 수는 있지만 hello 디버그 구성 하면 디버깅이 훨씬 쉽습니다.

    ![Hello 디버그 구성을 선택 합니다.](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746717.gif)
3. 하지만 select hello hello 일반적인 단계에 따라 **모든 역할에 대해 원격 디버거 사용** hello 확인란 **고급 설정** 탭 합니다.

    ![디버그 구성](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746718.gif)

### <a name="tooattach-hello-debugger-tooa-cloud-service-in-azure"></a>Azure의 tooattach hello 디버거 tooa 클라우드 서비스
1. 서버 탐색기에서 클라우드 서비스에 대 한 hello 노드를 확장 합니다.
2. Hello 역할 또는 역할 인스턴스 toowhich tooattach, 한 다음 선택에 대 한 바로 가기 메뉴를 열고 hello **디버거 연결**합니다.

    역할을 디버깅 하는 경우 hello Visual Studio 디버거에서 해당 역할의 tooeach 인스턴스에 연결 합니다. hello 디버거가 해당 코드 줄을 실행 하 고 해당 중단점의 조건을 충족 하는 hello 첫 번째 역할 인스턴스에 대 한 중단점에서 중단 합니다. 인스턴스를 디버깅할 경우 hello 디버거에서 tooonly 인스턴스와 특정 인스턴스에 해당 코드 줄을 실행 하 고 충족 하는 경우에 중단점에서 중단 중단점의 조건을 hello를 연결 합니다.

    ![디버거 연결](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746719.gif)
3. Hello 디버거가 tooan 인스턴스 연결을 한 후 디버깅 합니다. hello 디버거 사용자의 역할에 대 한 toohello 적절 한 호스트 프로세스를 자동으로 연결 됩니다. 역할은 어떤 hello에 따라, hello 디버거 연결 합니다. toow3wp.exe, WaWorkerHost.exe 또는 WaIISHost.exe 합니다. tooverify hello 프로세스 toowhich hello 디버거가 연결 된 서버 탐색기에서 hello 인스턴스 노드를 확장 합니다. Azure 프로세스에 대한 자세한 내용은 [Azure 역할 아키텍처](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx)를 참조하세요.

    ![코드 형식 선택 대화 상자](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
4. tooidentify hello 프로세스 toowhich hello 디버거를 연결 hello 메뉴 모음, 디버그, Windows, 프로세스를 선택 하 여, 되는 hello 프로세스 대화 상자를 엽니다. (키보드: Ctrl + Alt + Z) toodetach 특정 프로세스를 해당 바로 가기 메뉴를 연 다음 선택 **프로세스 분리**합니다. 또는, 서버 탐색기에서 hello 인스턴스 노드를 찾고, hello 프로세스를 찾을, 해당 바로 가기 메뉴를 연 선택한 후 **프로세스 분리**합니다.

    ![디버그 프로세스](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC690787.gif)

> [!WARNING]
> 원격 디버깅 시 중단점에서 장시간 중지하지 않도록 합니다. Azure를 응답 없음으로 몇 분 이상 중지 되 고 toothat 인스턴스에 트래픽 전송을 중지 하는 프로세스를 처리 합니다. 너무 오랫동안 중지 하면 msvsmon.exe hello 프로세스에서 분리 됩니다.
>
>

인스턴스 또는 역할, 디버그 중이면 디버깅을 하 고 다음을 선택 하는 hello 역할 또는 인스턴스에 대 한 바로 가기 메뉴를 열고 hello에서 모든 프로세스에서 toodetach hello 디버거 **디버거 분리**합니다.

## <a name="limitations-of-remote-debugging-in-azure"></a>Azure에서 원격 디버깅의 제한 사항
Azure SDK 2.3에서 원격 디버깅에 다음과 같은 제한을 hello 있습니다.

* 원격 디버깅을 사용하면 모든 역할에 25개 이상의 인스턴스가 있는 클라우드 서비스를 게시할 수 없습니다.
* hello 디버거는 30400 too30424 포트, 31400 too31424 및 32400 too32424 사용합니다. Toouse, 이러한 포트 중 하나를 수행 하는 경우에 수 toopublish hello 다음과 같은 오류 메시지 중 하나를 사용자가 서비스를은 Azure 용 hello 활동 로그에 표시 됩니다 수 없습니다.

  * Hello.csdef 파일에 대 한 hello.cscfg 파일의 유효성 검사 오류가 발생 했습니다.
    hello에서 이미 정의 된 포트 또는 범위와 겹치는 Microsoft.WindowsAzure.Plugins.RemoteDebugger.Connector 역할 '역할'의 끝점에 대 한 포트 범위 '범위' 예약 되어 있습니다.
  * 할당하지 못했습니다. 나중에 다시 시도, hello VM 크기 또는 역할 인스턴스 수를 줄여 보십시오 하 또는 tooa 다른 지역에 배포 해 보십시오.

## <a name="debugging-azure-virtual-machines"></a>Azure 가상 컴퓨터를 디버깅합니다.
Visual Studio의 서버 탐색기를 사용하여 Azure 가상 컴퓨터에서 실행하는 프로그램을 디버그할 수 있습니다. Azure 가상 컴퓨터에서 원격 디버깅을 사용 하도록 설정 하면 Azure는 hello 가상 컴퓨터에 hello 원격 디버깅 확장을 설치 합니다. 그런 다음 tooprocesses hello 가상 컴퓨터에 연결 하 고 일반적인 방법으로 디버그할 수 있습니다.

> [!NOTE]
> Visual Studio 2015에서 Cloud Explorer를 사용 하 여 hello Azure 리소스 관리자 스택을 통해 만든 가상 컴퓨터를 원격으로 디버깅할 수 있습니다. 자세한 내용은 [클라우드 탐색기를 사용하여 Azure 리소스 관리](http://go.microsoft.com/fwlink/?LinkId=623031)를 참조하세요.
>
>

### <a name="toodebug-an-azure-virtual-machine"></a>toodebug Azure 가상 컴퓨터
1. 서버 탐색기에서 hello 설정할 수 노드 및 toodebug 원하는 hello 가상 컴퓨터의 선택 hello 노드를 확장 합니다.
2. Hello 상황에 맞는 메뉴를 열고 선택 **디버깅 사용**합니다. 면 tooenable hello 가상 컴퓨터를 선택에서 디버깅 하려는 경우 확인 메시지가 표시 되 면 **예**합니다.

    Azure 가상 컴퓨터 tooenable 디버깅 hello hello 원격 디버깅 확장을 설치합니다.

    ![가상 컴퓨터 디버깅 사용 명령](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Azure 활동 로그](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
3. 후 hello 원격 디버깅 확장 설치가 완료 되 면, hello 가상 컴퓨터의 상황에 맞는 메뉴를 열고 선택 **디버거 연결...**

    Azure는 hello 가상 컴퓨터에서 hello 프로세스의 목록을 가져오고 hello 연결 tooProcess 대화 상자에서에 표시 합니다.

    ![디버거 연결 명령](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
4. Hello에 **tooProcess 연결** 대화 상자에서 **선택** toolimit hello 결과 목록은 tooshow hello 형식만 toodebug 원하는 코드입니다. 32, 64-비트 관리 코드 및 네이티브 코드 또는 둘 다 디버그할 수 있습니다.

    ![코드 형식 선택 대화 상자](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
5. Hello 프로세스 toodebug hello 가상 컴퓨터를 선택 하 고 선택 하면 선택 **연결**합니다. 예를 들어 toodebug hello 가상 컴퓨터에서 웹 앱을 원하는 경우에 hello w3wp.exe 프로세스를 선택할 수 있습니다. 자세한 내용은 [Visual Studio에서 하나 이상의 프로세스 디버그](https://msdn.microsoft.com/library/jj919165.aspx) 및 [Azure 역할 아키텍쳐](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx)를 참조하세요.

## <a name="create-a-web-project-and-a-virtual-machine-for-debugging"></a>디버깅을 위한 웹 프로젝트 및 가상 컴퓨터 만들기
Azure 프로젝트를 게시 하기 전에 것이 유용한 tootest 디버깅 및 테스트 시나리오를 지원 하 고 테스트 및 모니터링 프로그램을 설치할 수 있는 포함된 된 환경에서 합니다. 이 한 가지 방법은 toodo tooremotely 가상 컴퓨터에서 앱을 디버그 합니다.

Visual Studio ASP.NET 프로젝트 옵션 toocreate 앱 테스트에 사용할 수 있는 편리한 가상 컴퓨터를 제공 합니다. hello 가상 컴퓨터에 PowerShell, 원격 데스크톱 및 WebDeploy와 같은 일반적으로 필요한 끝점이 포함 됩니다.

### <a name="toocreate-a-web-project-and-a-virtual-machine-for-debugging"></a>toocreate 웹 프로젝트와 디버깅에 대 한 가상 컴퓨터
1. Visual Studio에서 새 ASP.NET 웹 응용 프로그램을 만듭니다.
2. Hello Azure 섹션에서에서 hello 새 ASP.NET 프로젝트 대화 상자에서 선택 **가상 컴퓨터** hello 드롭다운 목록 상자에 있습니다. Hello 둡니다 **원격 리소스 만들기** 확인란을 선택 합니다. 선택 **확인** tooproceed 합니다.

    hello **Azure에서 가상 컴퓨터를 만들** 대화 상자가 나타납니다.

    ![ASP.NET 웹 프로젝트 만들기 대화 상자](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746723.png)

    **참고:** 만들라는 메시지가 toosign tooyour Azure 계정에에서 아직 로그인 하는 경우.

1. Hello hello 가상 컴퓨터에 대 한 다양 한 설정을 선택한 다음 선택 **확인**합니다. 자세한 내용은 [가상 컴퓨터](http://go.microsoft.com/fwlink/?LinkId=623033) 를 참조하세요.

    DNS 이름에 대해 입력 한 hello 이름이 hello 가상 컴퓨터의 이름을 hello 됩니다.

    ![Azure 대화 상자에 가상 컴퓨터 만들기](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746724.png)

    Azure는 hello 가상 컴퓨터 프로 비전 한 다음 만들고 원격 데스크톱 및 웹 배포와 같은 hello 끝점 구성
2. Hello 가상 컴퓨터를 완전히 구성 되어 서버 탐색기에서 hello 가상 컴퓨터의 노드를 선택 합니다.
3. Hello 상황에 맞는 메뉴를 열고 선택 **디버깅 사용**합니다. 면 tooenable hello 가상 컴퓨터를 선택에서 디버깅 하려는 경우 확인 메시지가 표시 되 면 **예**합니다.

    Azure는 hello 원격 디버깅 확장 toohello 가상 컴퓨터 tooenable 디버깅을 설치합니다.

    ![가상 컴퓨터 디버깅 사용 명령](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Azure 활동 로그](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
4. [Visual Studio의 One-Click 게시를 사용하여 웹 프로젝트 배포 방법](https://msdn.microsoft.com/library/dd465337.aspx)을 따라 프로젝트를 게시합니다. Hello에서 hello 가상 컴퓨터에 toodebug 것 이므로 **설정** hello 페이지 **웹 게시** 선택 마법사 **디버그** hello 구성으로 합니다. 이 작업은 디버깅하는 동안 코드 기호를 사용할 수 있게 해줍니다.

    ![게시 설정](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718349.png)
5. Hello에 **파일 게시 옵션**선택, **대상에서 추가 파일 제거** hello 프로젝트는 이전에 이미 배포 된 경우.
6. 서버 탐색기에서 hello 가상 컴퓨터의 상황에 맞는 메뉴에 hello 프로젝트를 게시 한 후 선택 **디버거 연결...**

    Azure는 hello 가상 컴퓨터에서 hello 프로세스의 목록을 가져오고 hello 연결 tooProcess 대화 상자에서에 표시 합니다.

    ![디버거 연결 명령](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
7. Hello에 **tooProcess 연결** 대화 상자에서 **선택** toolimit hello 결과 목록은 tooshow hello 형식만 toodebug 원하는 코드입니다. 32, 64-비트 관리 코드 및 네이티브 코드 또는 둘 다 디버그할 수 있습니다.

    ![코드 형식 선택 대화 상자](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
8. Hello 프로세스 toodebug hello 가상 컴퓨터를 선택 하 고 선택 하면 선택 **연결**합니다. 예를 들어 toodebug hello 가상 컴퓨터에서 웹 앱을 원하는 경우에 hello w3wp.exe 프로세스를 선택할 수 있습니다. 자세한 내용은 [Visual Studio의 하나 이상의 프로세스 디버그](https://msdn.microsoft.com/library/jj919165.aspx) 를 참조하세요.

## <a name="next-steps"></a>다음 단계
* 사용 하 여 **Intellitrace** toocollect 호출 및 이벤트를 릴리스 하는 서버에서의 로그입니다. [IntelliTrace 및 Visual Studio를 사용하여 게시된 클라우드 서비스 디버깅](http://go.microsoft.com/fwlink/?LinkID=623016)을 참조하세요.
* 사용 하 여 **Azure 진단** toolog 자세한 코드 내에서 실행할 역할 정보를 hello 역할이 hello 개발 환경에서 또는 Azure에서 실행 되는 여부. [Azure 진단을 사용하여 로깅 데이터 수집](http://go.microsoft.com/fwlink/p/?LinkId=400450)을 참조하세요.

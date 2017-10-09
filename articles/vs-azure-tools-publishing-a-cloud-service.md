---
title: "aaaPublishing hello Azure 도구를 사용 하 여 클라우드 서비스 | Microsoft Docs"
description: "Visual Studio를 사용 하 여 Azure toopublish 서비스 프로젝트 클라우드 하는 방법에 대해 알아봅니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1a07b6e4-3678-4cbf-b37e-4520b402a3d9
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/14/2017
ms.author: kraigb
ms.openlocfilehash: 31ede8308146de2bb128b768f23f64eb85bc7548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publishing-a-cloud-service-using-hello-azure-tools"></a>Hello Azure Tools를 사용 하 여 클라우드 서비스 게시
Hello Azure Tools for Microsoft Visual Studio를 사용 하 여 Visual Studio에서 직접 Azure 응용 프로그램을 게시할 수 있습니다. 통합 하는 visual Studio 지원 hello 준비 또는 프로덕션 환경의 클라우드 서비스의 hello tooeither 게시 합니다.

Azure 응용 프로그램을 게시하기 전에 Azure 구독이 있어야 합니다. 응용 프로그램에서 사용 되는 클라우드 서비스와 저장소 계정 toobe를 설정 해야 합니다. 설정할 수 있습니다 이러한 hello에 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다.

> [!IMPORTANT]
> 게시 하면 클라우드 서비스에 대 한 hello 배포 환경을 선택할 수 있습니다. 또한 사용 되는 toostore hello 응용 프로그램 패키지 배포에 대 한 저장소 계정을 선택 해야 합니다. 배포 후 hello 응용 프로그램 패키지는 hello 저장소 계정에서 제거 됩니다.
> 
> 

개발 하 고 Azure 응용 프로그램을 테스트 하는 경우 웹 역할에 대 한 증분 toopublish 변경 웹 배포를 사용할 수 있습니다. 응용 프로그램 tooa 배포 환경에 게시 한 후 웹 배포 하면 toohello 가상 컴퓨터가 hello 웹 역할을 실행 중인를 직접 변경 내용을 배포. Toopackage 했으며 전체 Azure 응용 프로그램 웹 역할 tootest hello 변경 내용을 tooupdate 려 할 때마다 게시지 않습니다. 이 방법을 사용 hello 테스트용으로 클라우드에 toohave 대기 하지 않고 응용 프로그램 게시 된 tooa 배포 환경에서 사용할 수 있는 웹 역할 변경 내용을 사용할 수 있습니다.

웹 배포를 사용 하 여 Azure 응용 프로그램 및 웹 역할 tooupdate 프로시저 toopublish 다음 hello를 사용 합니다.

* Visual Studio에서 Azure 응용 프로그램 게시 또는 패키지 작성
* Hello 개발 및 테스트 주기 중 웹 역할 업데이트

## <a name="publish-or-package-an-azure-application-from-visual-studio"></a>Visual Studio에서 Azure 응용 프로그램 게시 또는 패키지 작성
Azure 응용 프로그램을 게시 하면 hello 다음 작업 중 하나를 수행할 수 있습니다.

* 서비스 패키지 만들기:이 패키지 및 hello 서비스 구성 파일 toopublish hello에서 응용 프로그램 tooa 배포 환경을 사용할 수 있습니다 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다.
* Visual Studio에서 Azure 프로젝트 게시: toopublish 응용 프로그램 사용 tooAzure, 직접 hello 게시 마법사. 자세한 내용은 [Azure 응용 프로그램 게시 마법사](vs-azure-tools-publish-azure-application-wizard.md)를 참조하세요.

### <a name="toocreate-a-service-package-from-visual-studio"></a>toocreate Visual Studio에서 서비스 패키지
1. 준비 toopublish 있을 때는 응용 프로그램 hello 사용자 역할이 포함 된 Azure 프로젝트에 대 한 바로 가기 메뉴를 열고 hello 솔루션 탐색기를 열고 게시를 선택 합니다.
2. 서비스 패키지 toocreate만 다음이 단계를 따르십시오.  
   
   1. Azure hello에 대 한 hello 바로 가기 메뉴에서 프로젝트를 선택 **패키지**합니다.
   2. Hello에 **Azure 응용 프로그램 패키지** 대화 상자에서 toocreate 원하는 hello 서비스 구성 패키지를 선택 하 고 hello 빌드 구성을 선택 합니다.
   3. 게시 한 후, 선택 hello hello 클라우드 서비스에 대 한 원격 데스크톱 (선택 사항) tooturn **모든 역할에 원격 데스크톱 사용** 확인란을 선택한 다음 선택 **설정을** tooconfigure 원격 데스크톱입니다. 원할 경우 toodebug 클라우드 서비스 게시 한 후을 선택 하 여 원격 디버깅 설정 **모든 역할에 대해 원격 디버거 사용**합니다.
      
      자세한 내용은 [Azure 역할로 원격 데스크톱 사용](vs-azure-tools-remote-desktop-roles.md)을 참조하세요.
   4. toocreate hello hello 선택, 패키지 **패키지** 링크 합니다.
      
      파일 탐색기의 패키지를 새로 만든 hello hello 파일 위치를 표시 합니다. Hello에서 사용할 수 있도록이 위치에 복사할 수 있습니다 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다.
   5. toopublish이 패키지 tooa 배포 환경으로 클라우드 서비스를 만들고이 패키지 tooan 환경을 hello로 배포 하는 경우 패키지 위치를 hello이 위치를 사용 해야 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다.
3. (선택 사항) toocancel hello 배포 프로세스 hello 활동 로그에서 품목 hello에 대 한 hello 바로 가기 메뉴에서 선택 **취소 및 제거**합니다. Hello 배포 프로세스를 중지 하 고 Azure에서 hello 배포 환경이 삭제 합니다.
   
   > [!NOTE]
   > 그 뒤에이 배포 환경 된 tooremove 배포 hello를 사용 해야 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다.
   > 
   > 
4. (선택 사항) 사용자의 역할 인스턴스가 시작 된 후 Visual Studio 자동으로 표시 hello 배포 환경 hello **클라우드 서비스** 서버 탐색기에서 노드. 여기에서는 hello 개별 역할 인스턴스의 hello 상태를 볼 수 있습니다. 참조 [Cloud Explorer를 사용 하 여 Azure 리소스](vs-azure-tools-resources-managing-with-cloud-explorer.md)그림 다음.hello 중일 때 여전히 hello Initializing 상태인 hello 역할 인스턴스를 보여 줍니다.
   
    ![VST_DeployComputeNode](./media/vs-azure-tools-publishing-a-cloud-service/IC744134.png)

## <a name="update-a-web-role-as-part-of-hello-development-and-testing-cycle"></a>Hello 개발 및 테스트 주기 웹 역할 업데이트
앱의 백 엔드 인프라가 안정적 이지만 웹 역할 hello 더욱 자주 업데이트 해야 하는 경우 웹 배포 tooupdate는 웹 역할 프로젝트에서 사용할 수 있습니다. 웹 역할이 여러 개인 경우 tooupdate hello 웹 역할 중 하나에 원하는 또는 toorebuild 원하고 hello 백 엔드 작업자 역할을 다시 배포 하지 않는 경우에 유용 합니다.

### <a name="requirements"></a>요구 사항
다음 hello 요구 사항 toouse 웹 배포 tooupdate 웹 역할은:

* **개발 및 테스트 목적 으로만:** hello 변경 내용이 직접 toohello 가상 컴퓨터 hello 웹 역할이 실행 되 고 있습니다. 이 가상 컴퓨터에는 재활용 toobe, 게시 hello 원래 패키지 hello 역할에 대 한 사용 되는 toorecreate hello 가상 컴퓨터 이므로 hello 변경 내용이 손실 됩니다. 응용 프로그램 tooget hello 최신 변경 내용을 hello 웹 역할에 대 한 다시 게시 해야 합니다.
* **웹 역할만 업데이트 가능:** 작업자 역할은 업데이트할 수 없습니다. 또한 web role.cs에서 RoleEntryPoint hello를 업데이트할 수 없습니다.
* **웹 역할의 단일 인스턴스만 지원할 수 있음:** 배포 환경의 웹 역할에 여러 인스턴스가 허용되지 않습니다. 하지만 각각의 웹 역할에 하나의 인스턴스만 있는 경우는 지원됩니다.
* **원격 데스크톱 연결을 사용 하도록 설정 해야:** 이것이 필요 hello 사용자 및 암호 tooconnect toohello 가상 컴퓨터 toodeploy hello 변경 toohello 실행 중인 서버에 인터넷 정보 서비스 (IIS) 웹 배포를 사용할 수 있도록 합니다. 또한 tooconnect toohello 가상 컴퓨터 tooadd이 가상 컴퓨터에 신뢰할 수 있는 인증서 tooIIS 할 수 있습니다. (이렇게 하면 웹 배포에서 사용 되는 IIS에 대 한 원격 연결 hello 안전 합니다.)

hello 다음 절차에서는 가정 hello를 사용 하는 **Azure 응용 프로그램 게시** 마법사.

### <a name="tooenable-web-deploy-when-you-publish-your-application"></a>tooEnable 웹 때 하면 게시 응용 프로그램 배포
1. tooenable hello **웹 배포 사용** 모든 웹 역할 확인란에 대해 먼저 원격 데스크톱 연결을 구성 해야 합니다. 선택 **원격 데스크톱 사용** 모든 역할 및 다음 hello에 원격으로 사용 되는 tooconnect 될 공급 hello 자격 증명에 대 한 **원격 데스크톱 구성** 나타나는 상자. 자세한 내용은 [Azure 역할로 원격 데스크톱 사용](vs-azure-tools-remote-desktop-roles.md) 을 참조하세요.
2. 웹 배포 tooenable 모든 hello 응용 프로그램의 웹 역할에 대 한 선택 **모든 웹 역할에 대해 웹 배포 사용**합니다.
   
    노란색 경고 삼각형이 나타납니다. 웹 배포는 기본적으로 신뢰할 수 없는 자체 서명 인증서를 사용하며, 이 인증서는 민감한 데이터를 업로드하는 데 적합하지 않습니다. Toosecure이이 프로세스에 필요한 중요 한 데이터를 웹 배포 연결에 사용 되는 SSL 인증서 toobe를 추가할 수 있습니다. 이 인증서는 신뢰할 수 있는 인증서 toobe가 되어야합니다. 방법에 대 한 정보에 대 한 toodo이 hello 섹션을 참조 **웹 배포를 안전 tooMake** 이 항목의 뒷부분에 나오는 합니다.
3. 선택 **다음** tooshow hello **요약** 화면에서 선택한 후 **게시** toodeploy hello 클라우드 서비스입니다.
   
    hello 클라우드 서비스가 게시 됩니다. 생성 된 hello 가상 컴퓨터 다시 게시 하지 않고 원격 연결 웹 배포 사용된 tooupdate 될 수 있도록 IIS에 사용할 웹 역할에 있습니다.
   
   > [!NOTE]
   > 웹 역할에 대해 구성 된 둘 이상의 인스턴스가 있는 경우 각 웹 역할에서 만들어진 toopublish 응용 프로그램 hello 패키지에만 제한 tooone 인스턴스 될 것 이라는 경고 메시지가 나타납니다. 선택 **확인** toocontinue 합니다. Hello 요구 사항 섹션에 나와 있는 것 처럼 수 둘 이상의 단일 웹 역할 있지만 각 역할의 인스턴스가 하나만 있습니다.
   > 
   > 

### <a name="tooupdate-your-web-role-by-using-web-deploy"></a>tooUpdate 웹 배포를 사용 하 여 사용자 웹 역할
1. 웹 배포 toouse toopublish을 원하는 한 다음 솔루션에서이 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 너무 가리킨 Visual Studio에서 코드 변경 내용을 toohello 프로젝트는 모든 웹 역할에 대 한 확인**게시**합니다. hello **웹 게시** 대화 상자가 나타납니다.
2. (선택 사항) IIS에 대 한 원격 연결에 대 한 신뢰할 수 있는 SSL 인증서 toouse를 추가한 경우 hello를 지울 수 있습니다 **신뢰할 수 없는 인증서 허용** 확인란 합니다. 어떻게 tooadd 웹 배포 인증서 toomake 보호에 대 한 내용은 hello 섹션을 참조 하십시오. **웹 배포를 안전 tooMake** 이 항목의 뒷부분에 나오는 합니다.
3. 웹 배포 toouse, hello 게시 메커니즘 hello 사용자 이름과 암호를 설정한 원격 데스크톱 연결에 대 한 hello 패키지를 처음 게시할 때 필요 합니다.
   
   1. **사용자 이름**, hello 사용자 이름을 입력 합니다.
   2. **암호**, hello 암호를 입력 합니다.
   3. (선택 사항) 이 프로필에서이 암호 toosave 하려는 경우 선택 **암호 저장**합니다.
4. toopublish hello 변경 tooyour 웹 역할을 선택 **게시**합니다.
   
    hello 상태 표시줄 표시 **게시 시작**합니다. Hello 게시 완료 되 면 **게시 했습니다** 나타납니다. 이제 hello 변경 내용은 가상 컴퓨터에 배포 된 toohello 웹 역할 이었습니다. 지금 변경 내용을 hello Azure 환경 tootest에서 Azure 응용 프로그램를 시작할 수 있습니다.

### <a name="toomake-web-deploy-secure"></a>웹 배포를 안전 tooMake
1. 웹 배포는 기본적으로 신뢰할 수 없는 자체 서명 인증서를 사용하며, 이 인증서는 민감한 데이터를 업로드하는 데 적합하지 않습니다. Toosecure이이 프로세스에 필요한 중요 한 데이터를 웹 배포 연결에 사용 되는 SSL 인증서 toobe를 추가할 수 있습니다. 이 인증서는 신뢰할 수 있는 인증서는 CA (인증 기관)에서 가져올 toobe가 되어야 합니다.
   
    toomake 웹 배포는 각 웹 역할에 대 한 각 가상 컴퓨터에 대 한 보안을 웹 toohello 배포에 대 한 않겠다고 toouse hello 신뢰할 수 있는 인증서를 업로드 해야 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다. 이렇게 하면 해당 hello 인증서가 응용 프로그램을 게시할 때 hello 웹 역할에 대해 만들어진 toohello 가상 컴퓨터를 추가 합니다.
2. 원격 연결에 대 한 신뢰할 수 있는 SSL 인증서 tooIIS toouse tooadd 다음이 단계를 따르십시오.
   
   1. hello 웹 역할에서 hello 웹 역할의 선택 hello 인스턴스를 실행 중인 tooconnect toohello 가상 컴퓨터 **클라우드 탐색기** 또는 **서버 탐색기**를 선택한 후 hello **사용 하 여 연결 원격 데스크톱** 명령입니다. 방법에 대 한 자세한 단계 tooconnect toohello 가상 컴퓨터를 참조 [Azure 역할과 함께 원격 데스크톱 사용 하 여](vs-azure-tools-remote-desktop-roles.md)합니다.
      
      브라우저를 묻습니다 toodownload는 합니다. RDP 파일입니다.
   2. tooadd, SSL 인증서를 IIS 관리자에서 열기 hello 관리 서비스입니다. IIS 관리자에서 SSL을 사용 하도록 설정 열어 hello 여 **바인딩** hello에 대 한 링크 **동작** 창. hello **사이트 바인딩 추가** 대화 상자가 나타납니다. 선택 **추가**, 다음 hello에서 HTTPS를 선택 하 고 **형식** 드롭다운 목록입니다. Hello에 **SSL 인증서** 목록에서 선택 hello SSL 인증서는 CA에서 서명 되 고 toohello 업로드할 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다. 자세한 내용은 참조 [hello 관리 서비스에 대 한 연결 설정 구성](http://go.microsoft.com/fwlink/?LinkId=215824)합니다.
      
      > [!NOTE]
      > Hello에 hello 노란색 경고 삼각형이 더 이상 나타나지 신뢰할 수 있는 SSL 인증서를 추가 하는 경우 **게시 마법사**합니다.
      > 
      > 

## <a name="include-files-in-hello-service-package"></a>Hello 서비스 패키지에서에서 파일을 포함
역할에 대해 만들어진 hello 가상 컴퓨터에서 사용할 수 있도록 서비스 패키지에서 tooinclude 특정 파일을 할 수 있습니다. 예를 들어.exe 또는.msi 파일은 시작 스크립트 tooyour 서비스 패키지에서 사용 되는 tooadd를 사용할 수 있습니다. 또는 tooadd 웹 역할 또는 작업자 역할 프로젝트에 필요한 어셈블리를 할 수 있습니다. Azure 응용 프로그램에 대 한 toohello 솔루션을 추가 하는 tooinclude 파일 이어야 합니다.

### <a name="tooinclude-files-in-hello-service-package"></a>hello 서비스 패키지의 tooinclude 파일
1. tooadd 어셈블리 tooa 서비스 패키지 단계를 수행 하는 hello를 사용 합니다.
   
   1. **솔루션 탐색기** 열기 hello 프로젝트 프로젝트 노드를 hello에 hello 참조 어셈블리는 없습니다.
   2. tooadd hello 어셈블리 toohello 프로젝트 hello에 대 한 바로 가기 메뉴를 열고 hello **참조** 폴더를 선택한 후 **참조 추가**합니다. hello 참조 추가 대화 상자가 나타납니다.
   3. Hello 참조 tooadd 원하고 hello를 눌러 선택 **확인** 단추입니다.
      
      hello 참조가 hello 아래의 toohello 목록에 추가 될 **참조** 폴더입니다.
   4. 사용자가 추가한 hello 어셈블리에 대 한 hello 바로 가기 메뉴를 열고 **속성**합니다. hello **속성** 창이 나타납니다.
      
      hello에 tooinclude hello 서비스에서이 어셈블리 패키지 **로컬 복사 목록** 선택 **True**합니다.
2. **솔루션 탐색기** 열기 hello 프로젝트 프로젝트 노드를 hello에 hello 참조 어셈블리는 없습니다.
3. tooadd hello 어셈블리 toohello 프로젝트 hello에 대 한 바로 가기 메뉴를 열고 hello **참조** 폴더를 선택한 후 **참조 추가**합니다. hello **참조 추가** 대화 상자가 나타납니다.
4. Hello 참조 tooadd 원하고 hello를 눌러 선택 **확인** 단추입니다.
   
    hello 참조가 hello 아래의 toohello 목록에 추가 될 **참조** 폴더입니다.
5. 사용자가 추가한 hello 어셈블리에 대 한 hello 바로 가기 메뉴를 열고 **속성**합니다. hello 속성 창이 나타납니다.
6. hello에 tooinclude hello 서비스에서이 어셈블리 패키지 **로컬 복사** 목록에서 선택 **True**합니다.
7. tooyour 웹 역할 프로젝트에 추가 된 hello 서비스 패키지의 tooinclude 파일 hello 파일에 대 한 hello 바로 가기 메뉴를 연 다음 선택 **속성**합니다. Hello에서 **속성** 창 선택 **콘텐츠** hello에서 **빌드 작업** 목록 상자입니다.
8. tooyour 작업자 역할 프로젝트에 추가 된 hello 서비스 패키지의 tooinclude 파일 hello 파일에 대 한 hello 바로 가기 메뉴를 연 다음 선택 **속성**합니다. Hello에서 **속성** 창 선택 **변경 된 내용만 복사** hello에서 **복사 toooutput 디렉터리** 목록 상자입니다.

## <a name="next-steps"></a>다음 단계
Visual Studio에서 게시 tooAzure에 대 한 자세한 toolearn 참조 [Azure 응용 프로그램 게시 마법사](vs-azure-tools-publish-azure-application-wizard.md)합니다.


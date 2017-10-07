---
title: "aaaBottle 및 Python Tools 2.2 for Visual Studio를 사용 하 여 Azure에서 Azure 테이블 저장소"
description: "어떻게 toouse hello Python Tools toocreate Visual Studio에 대 한 Azure 테이블 저장소에 데이터를 저장 하는 Bottle 응용 프로그램 학습과 hello 웹 응용 프로그램 tooAzure 앱 서비스 웹 앱을 배포 합니다."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: f075124b-db79-4e51-b394-09187dd6c634
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 25b9eb002b8748483d5b9458b7b5860a958b4bb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a>Azure의 Bottle 및 Azure 테이블 저장소와 Python Tools 2.2 for Visual Studio
이 자습서에서는 [Python Tools for Visual Studio] toocreate 단순 hello PTVS 샘플 템플릿 중 하나를 사용 하 여 웹 앱을 폴링합니다. 이 자습서는 [비디오](https://www.youtube.com/watch?v=GJXDGaEPy94)로도 제공됩니다.

hello 설문 웹 응용 프로그램 저장소 (메모리 내에서 Azure 테이블 저장소 MongoDB)의 서로 다른 유형을 쉽게 전환할 수 있도록 해당 저장소에 대 한 추상화를 정의 합니다.

어떻게 toocreate Azure 저장소 계정, tooconfigure hello 웹 앱 toouse Azure 테이블 저장소, 방법 등에 대해 배워 봅니다 우리 toopublish 웹 앱이 너무 hello[Azure 앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714)합니다.

Hello 참조 [Python 개발자 센터] Bottle를 사용 하 여 ptvs Azure 앱 서비스 웹 앱의 개발을 설명 하는 다른 문서 플라스 및 Django 웹 프레임 워크, MongoDB, Azure 테이블 저장소, MySQL 및 SQL 데이터베이스 서비스입니다. 개발 하는 경우 hello 단계는 유사 하지만이 문서에서는 앱 서비스, [Azure 클라우드 서비스]합니다.

## <a name="prerequisites"></a>필수 조건
* Visual Studio 2015
* [Python Tools 2.2 for Visual Studio]
* [VSIX Visual Studio 샘플에 대 한 Python Tools 2.2]
* [Azure SDK Tools for VS 2015]
* [Python 2.7 32비트] 또는 [Python 3.4 32비트]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

## <a name="create-hello-project"></a>Hello 프로젝트 만들기
이 섹션에서는 샘플 템플릿을 사용하여 Visual Studio 프로젝트를 만듭니다. 가상 환경을 만들고 필요한 패키지를 설치합니다. 다음 hello 기본 메모리 저장소를 사용 하 여 로컬로 hello 응용 프로그램을 실행 합니다.

1. Visual Studio에서 **파일**, **새 프로젝트**를 선택합니다.
2. 프로젝트 템플릿 hello에서 hello [VSIX Visual Studio 샘플에 대 한 Python Tools 2.2] 아래에서 사용할 수 있는 **Python**, **샘플**합니다. 선택 **설문 Bottle 웹 프로젝트** 확인 toocreate hello 프로젝트를 클릭 합니다.
   
     ![새 프로젝트 대화 상자](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. 외부 패키지 입력 정보 요청된 tooinstall 됩니다. **가상 환경에 설치**를 선택합니다.
   
     ![외부 패키지 대화 상자](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. 선택 **Python 2.7** 또는 **Python 3.4** hello 기본 해석기로 합니다.
   
     ![가상 환경 추가 대화 상자](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. Hello 응용 프로그램 키를 눌러 작동 하는지 확인 `F5`합니다. 기본적으로 hello 응용 프로그램에는 구성이 필요 하지 않습니다는 메모리 내 저장소를 사용 합니다. Hello 웹 서버를 중지 하는 경우 모든 데이터가 손실 됩니다.
6. **Create Sample Polls**를 클릭하고 poll and vote를 클릭합니다.
   
     ![웹 브라우저](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a>Azure 저장소 계정 만들기
toouse 저장소 작업을 Azure 저장소 계정이 필요 합니다. 다음 단계에 따라 저장소 계정을 만들 수 있습니다.

1. Hello에 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello 클릭 **새로** hello 위에 표시 아이콘 hello 포털의 왼쪽을 클릭 한 다음 **데이터 + 저장소** > **저장소 계정**합니다.  Hello 클릭 **만들기** 단추 hello 저장소 계정에 고유한 이름을 지정 하 고 새 [리소스 그룹](../azure-resource-manager/resource-group-overview.md) 것에 대 한 합니다.
   
      ![빠른 생성](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    Hello 저장소 계정이 생성 되 면 hello **알림** 단추가 녹색 깜박입니다 **성공** 블레이드 hello 저장소 계정을 열릴 및 tooshow 속하는지 toohello 새 리소스 그룹 만들어집니다.
3. Hello 클릭 **선택키가** hello 저장소 계정의 블레이드에서 부분입니다. Hello 계정 이름 및 key1 기록해 둡니다.
   
      ![구성](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    이 정보 tooconfigure hello 다음 단원의 프로젝트가 필요 합니다.

## <a name="configure-hello-project"></a>Hello 프로젝트 구성
이 섹션에서는 방금 만든 응용 프로그램 toouse hello 저장소 계좌를 구성 합니다. 다음 로컬로 hello 응용 프로그램을 실행 합니다.

1. Visual Studio의 솔루션 탐색기에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. Hello 클릭 **디버그** 탭 합니다.
   
     ![프로젝트 디버그 설정](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. Hello에 hello 응용 프로그램에서 요구 하는 환경 변수 값 설정 **서버 명령은 디버그**, **환경**합니다.
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   이렇게 하면 hello 환경 변수 설정 됩니다 때 있습니다 **디버깅 시작**합니다. Hello 변수 toobe 경우에 설정 하려는 경우 있습니다 **디버깅 하지 않고 시작**, 아래 값을 동일한 집합 hello **서버 명령 실행** 도 합니다.
   
   또는 Windows 제어판 hello를 사용 하 여 환경 변수를 정의할 수 있습니다. 프로젝트 파일 / 원하는 tooavoid 소스 코드에서 자격 증명을 저장 하는 경우 더 나은 옵션입니다. 값은 toobe toohello 사용할 수 있는 응용 프로그램 참고 hello 새 환경에 대 한 toorestart Visual Studio가 필요 합니다.
3. hello Azure 테이블 저장소 리포지토리를 구현 하는 hello 코드는 **models/azuretablestorage.py**합니다. Hello 참조 [설명서] 방법에 대 한 자세한 내용은 toouse Python에서 테이블 서비스입니다.
4. Hello 응용 프로그램을 실행 `F5`합니다. 사용 하 여 만든 설문 **샘플 설문 만들** 투표 제출한 hello 데이터는 Azure 테이블 저장소에 serialize 됩니다.
   
   > [!NOTE]
   > hello Python 2.7 가상 환경에는 Visual Studio에서 예외 나누기가 발생할 수 있습니다.  키를 눌러 `F5` toocontinue hello 웹 프로젝트를 로드 합니다.
   > 
   > 
5. Toohello 찾아보기 **에 대 한** hello 응용 프로그램 페이지 tooverify hello를 사용 하는 **Azure 테이블 저장소** 저장소입니다.
   
     ![웹 브라우저](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a>Hello Azure 테이블 저장소를 탐색 합니다.
쉽게 tooview 이며 클라우드 탐색기를 사용 하 여 Visual Studio에서 저장소 테이블을 편집 합니다. 이 섹션의 hello 여론 조사 응용 프로그램 테이블 내용의 tooview hello 서버 탐색기를 사용 합니다.

> [!NOTE]
> 사용할 수는 설치 된 Microsoft Azure 도구 toobe이 필요 hello의 일부로 [Azure SDK for.NET]합니다.
> 
> 

1. **클라우드 탐색기**를 엽니다. **저장소 계정**, 사용자의 저장소 계정 및 **테이블**을 차례로 확장합니다.
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. Hello에 두 번 클릭 **설문** 또는 **선택** tooview hello 내용의 hello 테이블 추가/제거/편집 엔터티를 비롯 하 여 문서 창에 테이블입니다.
   
     ![테이블 쿼리 결과](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a>Hello 웹 응용 프로그램 tooAzure 앱 서비스를 게시 합니다.
Azure.NET SDK hello 쉽게 toodeploy 웹 앱 tooAzure 앱 서비스를 제공합니다.

1. **솔루션 탐색기**hello 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.
   
     ![웹 게시 대화 상자](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. **Microsoft Azure 웹앱**을 클릭합니다.
3. 클릭 **새로** toocreate 새 웹 앱입니다.
4. Hello 필드 뒤에 입력 하 고 클릭 **만들기**합니다.
   
   * **웹앱 이름**
   * **앱 서비스 계획**
   * **리소스 그룹**
   * **지역**
   * 둡니다 **데이터베이스 서버** 도**데이터베이스가 없습니다.**
5. 다른 모든 기본값을 그대로 적용하고 **게시**를 클릭합니다.
6. 웹 브라우저가 toohello 게시 된 웹 응용 프로그램을 자동으로 열립니다. Hello를 사용 하 여 참조 페이지에 대 한 toohello을 찾아볼 때 **메모리** 저장소, 하지 hello **Azure 테이블 저장소** 저장소입니다.
   
   hello 환경 변수는 설정 되어 있지 않으므로 Azure 앱 서비스의 웹 앱 인스턴스에 hello에 지정 된 hello 기본값을 사용 하므로 **settings.py**합니다.

## <a name="configure-hello-web-apps-instance"></a>Hello 웹 응용 프로그램 인스턴스 구성
이 섹션에서는 hello 웹 앱 인스턴스에 대 한 환경 변수를 구성 합니다.

1. [Azure 포털], 클릭 하 여 hello 웹 앱 블레이드를 열고 **찾아보기** > **응용 프로그램 서비스** > 웹 응용 프로그램 이름입니다.
2. 웹앱 블레이드에서 **모든 설정**을 클릭한 다음 **응용 프로그램 설정**을 클릭합니다.
3. Toohello 아래로 스크롤하여 **앱 설정** 섹션 및 설정에 대 한 hello 값 **리포지토리\_이름**, **저장소\_이름** 및  **저장소\_키** hello에 설명 된 대로 **구성 hello 프로젝트** 위의 섹션.
   
     ![앱 설정](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. **Save**를 클릭합니다. Hello 변경 내용이 적용 된 hello 알림을 받은 후 클릭 **찾아보기** hello 웹 앱 블레이드에서 주입니다.
5. Hello를 사용 하 여 예상 대로 hello 웹 응용 프로그램 작업을 참조 해야 **Azure 테이블 저장소** 저장소입니다.
   
   축하합니다.
   
     ![웹 브라우저](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a>다음 단계
Visual Studio, Bottle 및 Azure 테이블 저장소에 대 한 Python Tools에 대 한 자세한 이러한 링크 toolearn를 따릅니다.

* [Python Tools for Visual Studio 설명서]
  * [웹 프로젝트]
  * [클라우드 서비스 프로젝트]
  * [Microsoft Azure의 원격 디버깅]
* [Bottle 설명서]
* [Azure 저장소]
* [Python용 Azure SDK]
* [어떻게 tooUse hello Python에서 테이블 저장소 서비스]

## <a name="whats-changed"></a>변경된 내용
* 웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Python 개발자 센터]: /develop/python/
[Azure 클라우드 서비스]: ../cloud-services/cloud-services-python-ptvs.md
[설명서]:../cosmos-db/table-storage-how-to-use-python.md
[어떻게 tooUse hello Python에서 테이블 저장소 서비스]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[Azure 포털]: https://portal.azure.com
[Azure SDK for.NET]: http://azure.microsoft.com/downloads/
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[VSIX Visual Studio 샘플에 대 한 Python Tools 2.2]: http://go.microsoft.com/fwlink/?LinkId=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32비트]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32비트]: http://go.microsoft.com/fwlink/?LinkId=517191
[Python Tools for Visual Studio 설명서]: http://aka.ms/ptvsdocs
[Bottle 설명서]: http://bottlepy.org/docs/dev/index.html
[Microsoft Azure의 원격 디버깅]: http://go.microsoft.com/fwlink/?LinkId=624026
[웹 프로젝트]: http://go.microsoft.com/fwlink/?LinkId=624027
[클라우드 서비스 프로젝트]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure 저장소]: http://azure.microsoft.com/documentation/services/storage/
[Python용 Azure SDK]: https://github.com/Azure/azure-sdk-for-python

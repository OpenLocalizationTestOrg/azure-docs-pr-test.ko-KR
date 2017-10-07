---
title: "aaaPrepare toopublish 하거나 Visual Studio에서 Azure 응용 프로그램 배포 | Microsoft Docs"
description: "클라우드 및 저장소 계정 서비스를 hello 프로시저 tooset 알아보고 Azure 응용 프로그램을 구성 합니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 92ee2f9e-ec49-4c7a-900d-620abe5e9d8a
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: b5231d400e2ad9e20c3f21bad48a77c328b1f7a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-toopublish-or-deploy-an-azure-application-from-visual-studio"></a>TooPublish를 준비 하거나 Visual Studio에서 Azure 응용 프로그램 배포
## <a name="overview"></a>개요
클라우드 서비스 프로젝트를 게시 하기 전에 다음 서비스는 hello를 설정 해야 합니다.

* A **클라우드 서비스** toorun hello Azure 환경에서에서 역할
* A **저장소 계정** toohello Blob, 큐 및 테이블 서비스 액세스를 제공 하는 합니다.

이러한 서비스를 프로시저 tooset 다음 hello를 사용 하 고 응용 프로그램 구성

## <a name="create-a-cloud-service"></a>클라우드 서비스 만들기
클라우드 서비스 tooAzure toopublish 먼저 만들어야 합니다 hello Azure 환경에서에서 역할을 실행 하는 클라우드 서비스를 합니다. Hello에 클라우드 서비스를 만들 수 있습니다 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)hello 섹션에 설명 된 대로 **toocreate 클라우드 서비스를 사용 하 여 hello Azure 클래식 포털**이 항목의 뒷부분에 나오는 합니다. Hello 게시 마법사를 사용 하 여 Visual Studio에서 클라우드 서비스를 만들 수 있습니다.

### <a name="toocreate-a-cloud-service-by-using-visual-studio"></a>toocreate Visual Studio를 사용 하 여 클라우드 서비스
1. Hello Azure 프로젝트에 대 한 hello 바로 가기 메뉴를 열고 **게시**합니다.

    ![VST_PublishMenu](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/vst-publish-menu.png)
2. 로그인 하지 않은, 경우 hello Microsoft 계정 또는 조직 계정을 연결 된 Azure 구독에 대 한 사용자 이름 및 암호를 사용 하 여 로그인 합니다.
3. Hello 선택 **다음** 단추 tooadvance toohello **설정을** 페이지.

    ![게시 마법사 일반 설정](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/publish-settings-page.png)
4. Hello에 **클라우드 서비스** 목록에서 선택 **새로 만들기**합니다. hello **Azure 서비스 만들기** 대화 상자가 나타납니다.
5. 클라우드 서비스의 hello 이름을 입력 합니다. hello 이름은 서비스에 대 한 hello URL의 일부를 형성 하며 전역적으로 고유 해야 합니다. hello 이름이 대/소문자 구분 않습니다.

### <a name="toocreate-a-cloud-service-by-using-hello-azure-classic-portal"></a>toocreate hello Azure 클래식 포털을 사용 하 여 클라우드 서비스
1. Toohello 로그인 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkId=253103) hello Microsoft 웹 사이트에 있습니다.
2. (선택 사항) 클라우드 서비스를 이미 만들었으면 목록이 toodisplay hello hello 페이지의 왼쪽에 hello 클라우드 서비스 링크를 선택 합니다.
3. Hello 선택 ** + ** hello 왼쪽 아래에서에서 아이콘 아래를 선택한 후 **클라우드 서비스** 나타나는 hello 메뉴에 있습니다. 두 옵션을 사용하는 다른 화면인 **빠른 생성** 및 **사용자 지정 만들기**가 나타납니다. 선택 하면 **빠른 생성**, 여기서 물리적으로 호스팅됩니다 해당 URL과 hello 영역을 지정 하 여 클라우드 서비스를 만들 수 있습니다. **사용자 지정 만들기**를 선택하는 경우, 패키지(.cspkg 파일), 구성 (.cscfg) 파일 및 인증서를 지정하여 클라우드 서비스를 즉시 게시할 수 있습니다. 가져오려는 경우 toopublish 클라우드 서비스 hello를 사용 하 여 사용자 지정 만들기는 필요 없습니다 **게시** Azure 프로젝트에 명령 합니다. hello **게시** 명령은 Azure 프로젝트에 대 한 hello 바로 가기 메뉴에 있습니다.
4. 선택 **빠른 생성** toolater Visual Studio를 사용 하 여 클라우드 서비스를 게시 합니다.
5. 클라우드 서비스의 이름을 지정합니다. hello 전체 URL에는 다음 toohello 이름 표시 됩니다.
6. Hello 목록에서 대부분의 사용자가 위치한 hello 지역을 선택 합니다.
7. Hello 창의 hello 맨 아래에 선택 hello **클라우드 서비스 만들기** 링크 합니다.

## <a name="create-a-storage-account"></a>저장소 계정 만들기
저장소 계정 액세스 toohello Blob, 큐 및 테이블 서비스를 제공합니다. Visual Studio 또는 hello를 사용 하 여 저장소 계정을 만들 수 있습니다 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkId=253103)합니다.

### <a name="toocreate-a-storage-account-by-using-visual-studio"></a>Visual Studio를 사용 하 여 저장소 계정 toocreate
1. **솔루션 탐색기**개방형 hello에 대 한 바로 가기 메뉴를 hello **저장소** 노드를 선택한 후 **저장소 계정 만들기**합니다.

    ![새 Azure 저장소 계정 만들기](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/IC744166.png)
2. 선택 또는 입력 hello hello에 새 저장소 계정에 대 한 정보를 다음 hello **저장소 계정 만들기** 대화 상자.

   * hello Azure 구독 toowhich tooadd hello 저장소 계정입니다.
   * hello 이름 toouse hello 새 저장소 계정에 대 한입니다.
   * hello 지역 또는 선호도 그룹 (예: 미국 서 부 또는 아시아의 경우).
   * 형식 hello 복제 원하는 toouse 지리적 중복 같은 hello 저장소 계정에 대 한 합니다.
3. 완료 되 면 선택 **만들기**hello에.hello 새 저장소 계정을 표시 **저장소** 목록에 **서버 탐색기**합니다.

### <a name="toocreate-a-storage-account-by-using-hello-azure-classic-portal"></a>toocreate hello Azure 클래식 포털을 사용 하 여 저장소 계정
1. Toohello 로그인 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkId=253103) hello Microsoft 웹 사이트에 있습니다.
2. (선택 사항) tooview 저장소 계정이 선택 hello **저장소** hello hello 페이지의 왼쪽에 hello 패널에 링크 합니다.
3. Hello hello 페이지의 왼쪽 아래 모서리에 hello 선택 ** + ** 아이콘입니다.
4. 표시 되는 hello 메뉴에서 선택 **저장소**를 선택한 후 **빠른 생성**합니다.
5. Hello 저장소 계정에 이름을 고유한 url를 발생 시킵니다.
6. 이름을 클라우드 서비스에 지정합니다. hello 전체 URL에는 다음 toohello 이름 표시 됩니다.
7. 영역의 hello 목록에서 대부분의 사용자가 위치한 지역을 선택 합니다.
8. Tooenable 지리적 복제 하는지 여부를 지정 합니다. 지리적 복제를 사용 하면 데이터 손실 가능성이 hello 여러 물리적 위치 tooreduce에 저장 됩니다. 이 기능을 사용 하면 저장소 비용이 많이 드는 하지만 hello 기능을 나중에 추가 하는 대신 hello 저장소 계정을 만들 때 지리적 위치를 사용 하 여 hello 비용을 줄일 수 있습니다. 자세한 내용은 [지역에서 복제](http://go.microsoft.com/fwlink/?LinkId=253108)를 참조하세요.
9. Hello 창의 hello 맨 아래에 선택 hello **저장소 계정 만들기** 링크 합니다.

저장소 계정을 만든 후 hello Url hello Azure 저장소 서비스의 각 tooaccess 리소스를 사용할 수 있으며 사용자 계정에 대 한 기본 및 보조 액세스 키를 hello도 표시 됩니다. 이러한 사용 tooauthenticate 요청 hello 저장소 서비스에 대 한 키입니다.

> [!NOTE]
> hello 보조 액세스 키 제공 hello 동일 hello 기본 액세스 키로 tooyour 저장소 계정에 액세스 하 고 기본 액세스 키를 노출 해야 백업으로 생성 됩니다. 또한 정기적으로 액세스 키를 다시 생성하는 것이 좋습니다. 수정할 수 있습니다 연결 문자열 설정을 toouse hello 보조 키 hello 기본 키를 다시 생성 하는 동안 수정할 수 있습니다 toouse 다시 생성 하는 hello에 대 한 기본 키 hello 보조 키를 다시 생성 하는 동안 다음.
>
>

## <a name="configure-your-app-toouse-services-provided-by-hello-storage-account"></a>Hello 저장소 계정에서 제공 하 여 응용 프로그램 toouse 서비스 구성
저장소 서비스 toouse hello Azure 저장소 서비스 사용자가 만든 액세스 하는 모든 역할을 구성 해야 합니다. toodo이 Azure 프로젝트에 대 한 여러 서비스 구성을 사용할 수 있습니다. 기본적으로, 이 두 가지 구성은 Azure 프로젝트에서 생성됩니다. 여러 서비스 구성을 사용 하 여 동일한 연결 문자열에 코드를 있지만 각 서비스 구성에서 연결 문자열에 대해 다른 값을 포함 하는 hello를 사용할 수 있습니다. 예를 들어 하나의 서비스 구성 toorun 사용 하 고 응용 프로그램 tooAzure hello Azure 저장소 에뮬레이터 및 다른 서비스 구성 toopublish를 사용 하 여 로컬로 응용 프로그램을 디버그할 수 있습니다. 서비스 구성에 대한 자세한 내용은 [여러 서비스 구성을 사용하여 Azure 프로젝트 구성](vs-azure-tools-multiple-services-project-configurations.md)을 참조하세요.

### <a name="tooconfigure-your-application-toouse-services-that-hello-storage-account-provides"></a>tooconfigure 저장소 계정 hello 하는 응용 프로그램 toouse 서비스 제공
1. Visual Studio에서 Azure 솔루션을 엽니다. 솔루션 탐색기에서 hello 저장소 서비스에 액세스 하는 Azure 프로젝트에서 각 역할에 대 한 hello 바로 가기 메뉴를 열고 선택한 **속성**합니다. Hello 역할의 hello 이름의 페이지 hello Visual Studio 편집기에 표시 됩니다. hello에 대 한 hello 필드를 표시 하는 hello 페이지 **구성** 탭 합니다.
2. Hello 역할에 대 한 hello 속성 페이지에서 선택 **설정을**합니다.
3. Hello에 **서비스 구성** 목록에서 원하는 tooedit hello 서비스 구성의 hello 이름을 선택 합니다. 이 역할에 대 한 hello 서비스 구성의 변경 내용을 tooall toomake를 원하는 경우 선택할 수 있습니다 **모든 구성**합니다.  Tooupdate 구성을 서비스 하는 방법에 대 한 자세한 내용은 hello 섹션을 참조 하십시오. **저장소 계정에 대 한 연결 문자열 관리** hello 항목의 [Visual Studio와 함께 Azure 클라우드 서비스에 대 한 hello 역할을 구성 합니다. ](vs-azure-tools-configure-roles-for-cloud-service.md).
4. toomodify 모든 연결 문자열 설정을 선택 hello **...** 다음 toohello 설정 단추를 클릭 합니다. hello **저장소 연결 문자열 만들기** 대화 상자가 나타납니다.
5. 아래 **사용 하 여 연결**, hello 선택 **구독** 옵션입니다.
6. Hello에 **구독** 목록에서 구독을 선택 합니다. 원하는 hello hello 구독 목록에 없으면 선택 hello **게시 설정 다운로드** 링크 합니다.
7. Hello에 **계정 이름** 목록에서 저장소 계정 이름을 선택 합니다. Azure Tools hello.publishsettings 파일을 사용 하 여 저장소 계정 자격 증명을 자동으로 가져옵니다. 저장소 계정 자격 증명을 수동으로 toospecify 선택 hello **수동으로 입력 한 자격 증명** 옵션을 선택한 후이 절차를 계속 합니다. Hello에서 저장소 계정 이름과 기본 키를 얻을 수 있습니다 [Azure 클래식 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)합니다. Toospecify 못하도록 하려는 경우 저장소 계정 설정을 hello를 수동으로 선택 **확인** 단추 tooclose hello 대화 상자.
8. Hello 선택 **저장소 계정을 입력** 자격 증명 링크 합니다.
9. Hello에 **계정 이름** 상자 hello 저장소 계정 이름을 입력 합니다.

   > [!NOTE]
   > Hello에 로그인 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885), 선택한 후 hello **저장소** 단추입니다. hello 포털 저장소 계정 목록을 보여 줍니다. 계정을 선택하면 그에 대한 페이지가 열립니다. 이 페이지에서 hello hello 저장소 계정의 이름으로 복사할 수 있습니다. 이전 버전의 hello 클래식 포털을 사용 하는 경우 hello 저장소 계정에에서 나타나는지 hello **저장소 계정은** 보기. 이 이름 toocopy, hello에서 강조 표시 **속성** 이 창 고 hello Ctrl + C 키를 선택 합니다. Visual Studio에 toopaste hello 이름을 선택 hello **계정 이름** 텍스트 상자의 및 hello Ctrl + V 키를 선택 합니다.
   >
   >
10. Hello에 **계정 키** 상자 기본 키를 입력 하거나 복사 한 hello에서 붙여 넣을 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다.
     이 키 toocopy:

    1. Hello 적절 한 저장소 계정에 대 한 hello 페이지의 hello 맨 아래에 선택 hello **키 관리** 단추입니다.
    2. Hello에 **키 액세스 관리** 페이지 hello 기본 액세스 키의 hello 텍스트를 선택 하 고 hello Ctrl + C 키를 선택 합니다.
    3. Azure Tools의 hello에 hello 키를 붙여 **계정 키** 상자입니다.
    4. Hello 옵션 toodetermine 다음 중 하나를 선택 해야 hello 서비스가 hello 저장소 계정에 액세스 하는 방법:

       * **HTTP 사용**. Hello 표준 옵션입니다. 예: `http://<account name>.blob.core.windows.net`.
       * **HTTPS 사용** . 예: `https://<accountname>.blob.core.windows.net`.
       * **사용자 지정 끝점 지정** hello 세 서비스 각각에 대해 합니다. 그런 다음 hello 특정 서비스에 대 한 hello 필드에 이러한 끝점을 입력할 수 있습니다.

         > [!NOTE]
         > 사용자 지정 끝점을 만들면 더 복잡한 연결 문자열을 만들 수 있습니다. 이 문자열 형식을 사용 하는 경우에 저장소 계정의 Blob 서비스 hello로 등록 된 사용자 지정 도메인 이름을 포함 하는 저장소 서비스 끝점을 지정할 수 있습니다. 또한 공유 액세스 서명을 통해 단일 컨테이너의 tooblob 리소스에만 액세스를 부여할 수 있습니다. 방법에 대 한 자세한 내용은 toocreate 사용자 지정 끝점 참조 [Azure 저장소 연결 문자열 구성](storage/common/storage-configure-connection-string.md)합니다.
         >
         >
11. toosave 이러한 연결 문자열 변경 사항을 선택 hello **확인** 단추를 선택한 후 hello **저장** hello 도구 모음에서 단추입니다. 이러한 변경 내용을 저장 한 후 발생할 수 있습니다이 연결 문자열의 hello 값 코드를 사용 하 여 [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx)합니다. 응용 프로그램 tooAzure를 게시할 때 hello Azure 저장소 계정 연결 문자열 hello에 대 한 포함 된 hello 서비스 구성을 선택 합니다. 응용 프로그램을 게시 한 후 hello 응용 hello Azure 저장소 서비스에 대해 예상 대로 작동 하는지 확인

## <a name="next-steps"></a>다음 단계
Visual Studio에서 앱 tooAzure 게시에 대 한 더 toolearn 참조 [hello Azure Tools를 사용 하 여 클라우드 서비스 게시](vs-azure-tools-publishing-a-cloud-service.md)합니다.

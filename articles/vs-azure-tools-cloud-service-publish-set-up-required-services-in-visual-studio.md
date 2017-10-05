---
title: "Visual Studio에서 Azure 응용 프로그램 게시 또는 배포 준비 | Microsoft Docs"
description: "클라우드 및 저장소 계정 서비스를 설정하고 Azure 응용 프로그램을 구성하는 절차에 대해 알아봅니다."
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
ms.openlocfilehash: cc4fb87e559f554634ae062a59bee31f0831da64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="prepare-to-publish-or-deploy-an-azure-application-from-visual-studio"></a>Visual Studio에서 Azure 응용 프로그램 게시 또는 배포 준비
## <a name="overview"></a>개요
클라우드 서비스 프로젝트를 게시하기 전에 다음 서비스를 설정해야 합니다.

* Azure 환경에서 역할을 실행하는 **클라우드 서비스**
* Blob, 큐 및 테이블 서비스에 대한 액세스를 제공하는 **저장소 계정** .

다음 절차를 사용하여 이러한 서비스를 설정하고 응용 프로그램 구성

## <a name="create-a-cloud-service"></a>클라우드 서비스 만들기
Azure에 클라우드 서비스를 게시하려면 먼저 Azure 환경에서 사용자 역할을 실행하는 클라우드 서비스를 만들어야 합니다. 이 항목 뒷부분에 나오는 [Azure 클래식 포털을 사용하여 클라우드 서비스를 만들려면](http://go.microsoft.com/fwlink/?LinkID=213885)섹션에서 설명하는 대로 **Azure 클래식 포털**에서 클라우드 서비스를 만들 수 있습니다. 또한 게시 마법사를 사용하여 Visual Studio에서 클라우드 서비스를 만들 수 있습니다.

### <a name="to-create-a-cloud-service-by-using-visual-studio"></a>Visual Studio를 사용하여 클라우드 서비스 만들기
1. Azure 프로젝트의 바로 가기 메뉴를 열고, **게시**를 선택합니다.

    ![VST_PublishMenu](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/vst-publish-menu.png)
2. 로그인하지 않은 경우 Azure 구독과 연결된 Microsoft 계정 또는 조직 계정에 대한 사용자 이름 및 암호를 사용하여 로그인합니다.
3. **다음** 단추를 선택하여 **설정** 페이지로 이동합니다.

    ![게시 마법사 일반 설정](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/publish-settings-page.png)
4. **클라우드 서비스** 목록에서 **새로 만들기**를 선택합니다. **Azure 서비스 만들기** 대화 상자가 나타납니다.
5. 클라우드 서비스의 이름을 입력합니다. 이름은 서비스에 대한 URL의 일부를 형성하므로 전역적으로 고유해야 합니다. 이름은 대/소문자를 구분하지 않습니다.

### <a name="to-create-a-cloud-service-by-using-the-azure-classic-portal"></a>Azure 클래식 포털
1. Microsoft 웹 사이트의 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkId=253103) 에 로그인합니다.
2. (선택 사항) 이미 만든 클라우드 서비스의 목록을 표시하려면 페이지의 왼쪽에서 클라우드 서비스 링크를 선택합니다.
3. 왼쪽 아래 모퉁이에서 **+** 아이콘을 선택한 다음 나타나는 메뉴에서 **클라우드 서비스**를 선택합니다. 두 옵션을 사용하는 다른 화면인 **빠른 생성** 및 **사용자 지정 만들기**가 나타납니다. **빠른 생성**을 선택하는 경우, 물리적으로 호스트되는 URL과 해당 지역을 지정하여 클라우드 서비스를 만들 수 있습니다. **사용자 지정 만들기**를 선택하는 경우, 패키지(.cspkg 파일), 구성 (.cscfg) 파일 및 인증서를 지정하여 클라우드 서비스를 즉시 게시할 수 있습니다. Azure 프로젝트의 **게시** 명령을 사용하여 클라우드 서비스를 게시하려는 경우 사용자 지정 만들기는 필요하지 않습니다. **게시** 는 Azure 프로젝트에 대한 바로 가기 메뉴에서 사용할 수 있는 명령입니다.
4. **빠른 생성** 을 선택하여 나중에 Visual Studio를 사용하여 클라우드 서비스를 게시합니다.
5. 클라우드 서비스의 이름을 지정합니다. 전체 URL이 이름 옆에 나타납니다.
6. 목록에서 대부분의 사용자가 위치한 지역을 선택합니다.
7. 창의 아래쪽에서 **클라우드 서비스 만들기** 링크를 선택합니다.

## <a name="create-a-storage-account"></a>저장소 계정 만들기
저장소 계정은 Blob, 큐 및 테이블 서비스에 대한 액세스를 제공합니다. Visual Studio 또는 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkId=253103)을 사용하여 저장소 계정을 만들 수 있습니다.

### <a name="to-create-a-storage-account-by-using-visual-studio"></a>Visual Studio를 사용하여 저장소 계정을 만들려면
1. **솔루션 탐색기**에서 **저장소** 노드에 대한 바로 가기 메뉴를 연 다음 **저장소 계정 만들기**를 선택합니다.

    ![새 Azure 저장소 계정 만들기](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/IC744166.png)
2. **저장소 계정 만들기** 대화 상자에서 새 저장소 계정에 대한 다음의 정보를 선택 또는 입력합니다.

   * 저장소 계정을 추가할 Azure 구독입니다.
   * 새 저장소 계정에 대해 사용하려는 이름입니다.
   * 지역 또는 선호도 그룹 (예: 미국 서부 또는 동아시아)입니다.
   * 저장소 계정에 대해 사용하려는 복제의 유형입니다 – 예: 지역 중복.
3. 완료되면 **만들기**를 선택합니다. 새 저장소 계정이 **서버 탐색기**의 **저장소** 목록에 나타납니다.

### <a name="to-create-a-storage-account-by-using-the-azure-classic-portal"></a>Azure 클래식 포털을 사용하여 저장소 계정을 만들려면
1. Microsoft 웹 사이트의 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkId=253103) 에 로그인합니다.
2. (선택 사항) 저장소 계정을 보려면 페이지의 왼쪽에서 패널의 **저장소** 링크를 선택합니다.
3. 페이지의 왼쪽 아래 모퉁이에서 **+** 아이콘을 선택합니다.
4. 나타나는 메뉴에서 **저장소**를 선택한 다음 **빠른 생성**을 선택합니다.
5. 고유 url이 될 이름을 저장소 계정에 지정합니다.
6. 이름을 클라우드 서비스에 지정합니다. 전체 URL이 이름 옆에 나타납니다.
7. 지역 목록에서 대부분의 사용자가 위치한 지역을 선택합니다.
8. 지리적 복제를 사용하도록 설정하는지 여부를 지정합니다. 지리적 복제를 사용하도록 설정하면 손실의 가능성을 줄일 수 있는 여러 물리적 위치에 저장됩니다. 이 기능을 사용하면 저장소 비용이 많이 듭니다. 하지만 나중에 기능을 추가 하는 대신 저장소 계정을 만들 때 지리적 위치를 사용하여 비용을 줄일 수 있습니다. 자세한 내용은 [지역에서 복제](http://go.microsoft.com/fwlink/?LinkId=253108)를 참조하세요.
9. 창의 아래쪽에서 **저장소 계정 만들기** 링크를 선택합니다.

저장소 계정을 만든 후에 Azure 저장소 서비스 및 사용자 계정에 대한 기본 및 보조 액세스 키의 각 리소스에 액세스하는 데 사용할 수 있는 Url이 표시 됩니다. 이러한 키를 사용하여 저장소 서비스에 대해 수행된 요청을 인증합니다.

> [!NOTE]
> 보조 액세스 키는 기본 액세스 키로서 저장소 계정에 대한 동일한 액세스를 제공하며 기본 액세스 키가 손상되는 경우 백업으로 생성됩니다. 또한 정기적으로 액세스 키를 다시 생성하는 것이 좋습니다. 기본 키를 다시 생성하는 동안 보조 키를 사용하기 위한 연결 문자열 설정을 수정한 다음, 보조 키를 다시 생성하는 동안 기본 키를 다시 생성하기 위해 문자열 설정을 수정할 수 있습니다.
>
>

## <a name="configure-your-app-to-use-services-provided-by-the-storage-account"></a>앱을 구성하여 저장소 계정에서 제공하는 서비스를 사용합니다.
사용자가 만든 Azure 저장소 서비스를 사용하여 저장소 서비스에 액세스하는 모든 역할을 구성해야 합니다. 이렇게 하면 Azure 프로젝트에 대한 여러 서비스 구성을 사용할 수 있습니다. 기본적으로, 이 두 가지 구성은 Azure 프로젝트에서 생성됩니다. 여러 서비스 구성을 사용 하면 코드에서 동일한 연결 문자열을 사용할 수 있지만 각 서비스 구성에서 연결 문자열에 대해 다른 값을 가질 수 있습니다. 예를 들어, Azure 저장소 에뮬레이터를 사용하여 로컬에서 응용 프로그램을 실행 및 디버깅하는 서비스 구성을 사용할 수 있으며 Azure에 응용 프로그램을 게시하는 다른 서비스 구성을 사용할 수 있습니다. 서비스 구성에 대한 자세한 내용은 [여러 서비스 구성을 사용하여 Azure 프로젝트 구성](vs-azure-tools-multiple-services-project-configurations.md)을 참조하세요.

### <a name="to-configure-your-application-to-use-services-that-the-storage-account-provides"></a>저장소 계정이 제공하는 서비스를 사용하도록 응용 프로그램을 구성하려면
1. Visual Studio에서 Azure 솔루션을 엽니다. 솔루션 탐색기에서 저장소 서비스에 액세스 하는 Azure 프로젝트의 각 역할에 대한 바로 가기 메뉴를 열고 **속성**을 선택합니다. 역할의 이름이 있는 페이지가 Visual Studio 편집기에 표시됩니다. 페이지에 **구성** 탭에 대한 필드가 표시됩니다.
2. 역할에 대한 속성 페이지에서 **설정**을 선택합니다.
3. **서비스 구성** 목록에서 편집할 서비스 구성의 이름을 선택합니다. 이 역할에 대한 모든 서비스 구성을 변경하려는 경우 **모든 구성**을 선택할 수 있습니다.  서비스 구성을 업데이트하는 방법에 대한 자세한 내용은 **Visual Studio를 사용하여 Azure 클라우드 서비스에 대한 역할 구성** .항목의 [저장소 계정에 대한 연결 문자열 관리](vs-azure-tools-configure-roles-for-cloud-service.md)섹션을 참조하세요.
4. 연결 문자열 설정을 수정하려면 설정 옆에 있는 **...** 단추를 선택합니다. **저장소 연결 문자열 만들기** 대화 상자가 나타납니다.
5. **연결 사용**아래에서 **구독** 옵션을 선택합니다.
6. **구독** 목록에서 구독을 선택합니다. 구독 목록에 원하는 구독이 없으면 **게시 설정 다운로드** 링크를 선택합니다.
7. **계정 이름** 목록에서 저장소 계정 이름을 선택합니다. Azure Tools은.publishsettings 파일을 사용하여 자동으로 저장소 계정 자격 증명을 가져옵니다. 저장소 계정 자격 증명을 수동으로 지정하려면 **수동으로 입력한 자격 증명** 옵션을 선택한 다음 이 절차를 계속합니다. [Azure 클래식 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)에서 저장소 계정 이름과 기본 키를 얻을 수 있습니다. 저장소 계정 설정을 수동으로 지정하지 않으려면 **확인** 단추를 선택하여 대화 상자를 닫습니다.
8. **저장소 계정 입력** 자격 증명 링크를 선택합니다.
9. **계정 이름** 상자에 저장소 계정의 이름을 입력합니다.

   > [!NOTE]
   > [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)에 로그인한 다음 **저장소** 단추를 선택합니다. 포털에서는 저장소 계정 목록을 보여줍니다. 계정을 선택하면 그에 대한 페이지가 열립니다. 이 페이지에서 저장소 계정의 이름을 복사할 수 있습니다. 이전 버전의 클래식 포털을 사용하는 경우에는 저장소 계정 이름이 **저장소 계정** 보기에 나타납니다. 이 이름을 복사하려면 이 보기의 **속성** 창에서 강조 표시한 다음 Ctrl-C 키를 선택합니다. 이름을 Visual Studio을 붙여넣으려면 **계정 이름** 텍스트 상자를 선택한 다음 Ctrl+V 키를 선택합니다.
   >
   >
10. **계정 키** 상자에서 기본 키를 입력하거나 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)에서 기본 키를 복사하고 붙여넣습니다.
     이 키를 복사하려면:

    1. 적절한 저장소 계정에 대한 페이지의 맨 아래에서 **키 관리** 단추를 선택합니다.
    2. **키 액세스 관리** 페이지에서 기본 액세스 키의 텍스트를 선택하고 Ctrl+C 키를 선택합니다.
    3. Azure Tools에서 **계정 키** 상자에 키를 붙여넣습니다.
    4. 서비스가 저장소 계정에 액세스하는 방식을 결정하려면 다음 옵션 중 하나를 선택해야 합니다.

       * **HTTP 사용**. 표준 옵션입니다. 예: `http://<account name>.blob.core.windows.net`
       * **HTTPS 사용** . 예: `https://<accountname>.blob.core.windows.net`
       * **사용자 지정 끝점 지정** . 그런 다음 특정 서비스에 대한 필드에 이러한 끝점을 입력할 수 있습니다.

         > [!NOTE]
         > 사용자 지정 끝점을 만들면 더 복잡한 연결 문자열을 만들 수 있습니다. 이 문자열 형식을 사용할 때 BLOB 서비스를 통해 저장소 계정에 등록한 사용자 지정 도메인 이름을 포함하는 저장소 서비스 끝점을 지정할 수 있습니다. 또한 공유 액세스 서명을 통해 단일 컨테이너의 BLOB 리소스에만 액세스를 부여할 수 있습니다. 사용자 지정 끝점을 만드는 방법에 대한 자세한 내용은 [Azure Storage 연결 문자열 구성](storage/common/storage-configure-connection-string.md)을 참조하세요.
         >
         >
11. 이러한 연결 문자열 변경 사항을 저장하려면 **확인** 단추를 선택한 다음 도구 모음의 **저장** 단추를 선택합니다. 이러한 변경 내용을 저장한 후 [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx)를 사용하여 사용자의 코드의 연결 문자열의 값을 가져올 수 있습니다. Azure에 응용 프로그램을 게시하는 경우 연결 문자열에 대한 Azure 저장소 계정이 포함된 서비스 구성을 선택합니다. 응용 프로그램을 게시한 후, 응용 프로그램이 Azure 저장소 서비스에 대해 예상 대로 작동하는지 확인합니다.

## <a name="next-steps"></a>다음 단계
Visual Studio에서 Azure에 앱을 게시하는 방법에 대한 자세한 내용은 [Azure Tools를 사용하여 클라우드 서비스 게시](vs-azure-tools-publishing-a-cloud-service.md)를 참조하세요.

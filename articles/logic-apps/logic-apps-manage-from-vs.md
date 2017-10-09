---
title: "Visual Studio-Azure 논리 앱에서에서 aaaManage 논리 앱 | Microsoft Docs"
description: "Visual Studio 클라우드 탐색기를 사용하여 Logic Apps 및 기타 Azure 자산 관리"
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a>Visual Studio 클라우드 탐색기를 사용하여 Logic Apps 관리

하지만 hello [Azure 포털](https://portal.azure.com/) toodesign 수 있는 좋은 방법 제공 Azure 논리 앱을 관리 하 고, 논리 앱을 포함 하 여 Azure 자산을 관리 하기 위한 Visual Studio 클라우드 탐색기를 사용할 수 있습니다. Visual Studio 클라우드 탐색기를 사용하면 게시된 논리 앱을 찾아보기, 관리, 편집 및 다운로드할 수 있습니다. 관리 작업에는 실행 기록의 보기, 활성화 및 비활성화가 포함됩니다. 

먼저 이러한 Azure Logic Apps용 Visual Studio Tools를 설치하고 구성해야 Visual Studio에서 논리 앱에 액세스하고 관리할 수 있습니다. 

## <a name="prerequisites"></a>필수 조건

* [Visual Studio 2015 또는 Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* [최신 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 이상)
* [Visual Studio 클라우드 탐색기](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* 액세스 toohello 웹 hello 포함 된 디자이너를 사용 하는 경우

## <a name="install-visual-studio-tools-for-logic-apps"></a>Logic Apps용 Visual Studio 도구 설치

Hello 필수 구성 요소를 설치한 후 다운로드 하 고 Visual Studio 용 hello Azure 논리 앱 도구를 설치 합니다.

1. Visual Studio를 엽니다. Hello에 **도구** 메뉴 선택 **확장명 및 업데이트**합니다.
2. Hello 확장 **온라인** 범주 온라인 hello Visual Studio 갤러리에서에서 검색할 수 있도록 합니다.
3. **Visual Studio용 Azure Logic Apps 도구**를 찾을 때까지 **Logic Apps**을 찾아보거나 검색합니다.
4. toodownload 및 설치 hello 확장 클릭 **다운로드**합니다.
5. 설치 후 Visual Studio를 다시 시작합니다.

> [!NOTE]
> toodownload hello Azure 논리 앱 Tools for Visual Studio를 이동한 다음 toohello [Visual Studio 마켓플레이스](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9)합니다.

## <a name="browse-for-logic-apps-in-cloud-explorer"></a>클라우드 탐색기에서 논리 앱 찾아보기

1.  hello에 클라우드 탐색기 tooopen **보기** 메뉴 선택 **클라우드 탐색기**합니다.
2.  리소스 그룹 또는 리소스 유형별로 논리 앱을 찾아봅니다. 

    * Azure 구독을 선택, hello 확장을 리소스 유형에 따라 이동 하는 경우 **논리 앱** 섹션을 논리 앱을 선택 합니다. 
    * 리소스 그룹으로 이동 하는 경우 논리 앱 없는 hello 리소스 그룹을 확장 하 고 논리 앱을 선택 합니다.

    tooview 명령을 논리 앱에 대 한 논리 앱을 마우스 오른쪽 단추로 클릭 하거나 클라우드 탐색기 hello 맨 아래에 선택 hello에서 **동작** 메뉴.

    ![논리 앱 찾아보기](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a>Logic Apps 디자이너로 논리 앱 편집

클라우드 탐색기에서 hello에 현재 배포 된 논리 앱을 열 수 있습니다 hello Azure 포털에서에서 사용 하는 동일한 디자이너입니다. 

* tooedit 클라우드 탐색기에서 논리 앱, 논리 앱을 마우스 오른쪽 단추로 클릭 하 고 선택 **논리가 응용 프로그램 편집기 열기**합니다. 

* toopublish 업데이트 toohello 클라우드 선택 **게시**합니다. 

* 새 실행 toostart 선택 **트리거 실행**합니다.

![논리 앱 디자이너](./media/logic-apps-manage-from-vs/designer.png)

Hello 디자이너에서 수도 있습니다 **다운로드** 논리 앱. 이 작업은 자동으로 hello 논리 앱 정의 매개 변수화 하 고 Azure 리소스 관리자 배포 템플릿으로 hello 정의 저장 합니다. 이 배포 템플릿 tooyour Azure 리소스 그룹 프로젝트를 추가할 수 있습니다.

## <a name="browse-your-logic-app-run-history"></a>논리 앱 실행 기록 찾아보기

실행 논리 앱에 대 한 기록이 tooview hello 논리 앱을 마우스 오른쪽 단추로 클릭 하 고 선택 **열기 실행 기록이**합니다. tooreorder hello 속성 선택 하 여 표시 된 hello 열 머리글 중 하나에 실행된 기록을 기반으로 합니다.

![실행 기록](media/logic-apps-manage-from-vs/runs.png)

hello 실행 hello 입 / 출력에서 각 단계를 포함 하 여 결과 검토할 수 있도록 실행 인스턴스에 대 한 기록이 tooshow hello는 인스턴스를 실행 하는 hello 중 하나를 두 번 클릭 합니다.

![단계에서 기록 결과, 입력 및 출력 실행](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a>다음 단계

* [첫 번째 논리 앱 만들기](logic-apps-create-a-logic-app.md)
* [Visual Studio에서 Logic Apps 디자인, 빌드 및 배포](logic-apps-deploy-from-vs.md)
* [일반적인 예제 및 시나리오 보기](logic-apps-examples-and-scenarios.md)
* [동영상: Azure Logic Apps를 사용하여 비즈니스 프로세스 자동화](http://channel9.msdn.com/Events/Build/2016/T694)
* [동영상: Azure Logic Apps와 시스템 통합](http://channel9.msdn.com/Events/Build/2016/P462)

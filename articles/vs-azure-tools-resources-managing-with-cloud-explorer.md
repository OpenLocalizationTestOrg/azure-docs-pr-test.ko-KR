---
title: "aaaManaging Azure 클라우드 탐색기를 사용 하 여 리소스 | Microsoft Docs"
description: "자세한 방법을 toouse 클라우드 탐색기 toobrowse 및 Visual Studio 내에서 Azure 리소스를 관리 합니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a>Visual Studio 클라우드 탐색기에서 Azure 계정에 연결 된 hello 리소스 관리
클라우드 탐색기를 사용 하면 tooview 하 여 Azure 리소스 및 해당 속성을 검사 하 고 Visual Studio 내에서 키 개발자 진단 작업을 수행 하는 리소스 그룹입니다. 

Hello 처럼 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040), 클라우드 탐색기 hello Azure 리소스 관리자 스택에서 만들어집니다. 따라서 클라우드 탐색기는 Azure 리소스 그룹과 같은 리소스 및 논리 앱과 API 앱과 같은 Azure 서비스를 이해하고 RBAC([역할 기반 액세스 제어](active-directory/role-based-access-control-configure.md))를 지원합니다. 

## <a name="prerequisites"></a>필수 조건
- [Visual Studio 2017](https://www.visualstudio.com/downloads/) hello로 **Azure 워크 로드** 선택 또는 이전 버전의 Visual Studio hello로 [Microsoft Azure SDK for.NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657)합니다.
- Microsoft Azure 계정 - 계정이 없는 경우 [평가판을 등록](http://go.microsoft.com/fwlink/?LinkId=623901)하거나 [Visual Studio 구독자 혜택을 활성화](http://go.microsoft.com/fwlink/?LinkId=623901)할 수 있습니다.

> [!NOTE]
> 클라우드 탐색기 tooview 선택 **보기** > **클라우드 탐색기** hello 메뉴 모음에서 합니다.   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a>Azure 계정 tooCloud 탐색기 추가
Azure 계정에 연결 된 tooview hello 리소스 먼저 hello 계정 tooCloud 탐색기 추가 해야 합니다. 

1. **클라우드 탐색기**에서 **Azure 계정 설정**을 선택합니다.

    ![클라우드 탐색기 Azure 계정 설정 아이콘](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. **새 계정 추가**를 선택합니다. 

    ![클라우드 탐색기 계정 추가 링크](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. Azure 계정 원하는 리소스가 toohello 로그인 toobrowse 합니다. 

1. Tooan Azure 계정에에서 로그인을 해당 계정과 연결 된 hello 구독 표시 합니다. 선택 hello toobrowse 한 다음 선택 hello 계정 구독에 대 한 확인란 **적용**합니다. 
 
    ![클라우드 탐색기: toodisplay Azure 구독 선택](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. 원하는 리소스가 hello 구독을 선택한 후 toobrowse, 해당 구독 및 리소스 hello 클라우드 탐색기에에서 표시 합니다.

    ![Azure 계정에 대한 클라우드 탐색기 리소스 목록](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a>클라우드 탐색기에서 Azure 계정 제거 

1. **클라우드 탐색기**에서 **Azure 계정 설정**을 선택합니다.

    ![클라우드 탐색기 Azure 계정 설정 아이콘](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. 다음 toohello 계정을 tooremove, 원하는 선택 **제거**합니다.

    ![클라우드 탐색기 Azure 계정 설정 아이콘](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a>리소스 종류 또는 리소스 그룹 보기
tooview에서는 Azure 리소스를 직접 선택할 수 있습니다 **리소스 종류** 또는 **리소스 그룹** 보기.

1. **클라우드 탐색기**, 선택 hello 리소스 뷰 드롭다운입니다.

    ![클라우드 탐색기 드롭다운 목록 tooselect hello 원하는 리소스 보기](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. Hello 상황에 맞는 메뉴에서 원하는 hello 보기를 선택 합니다. 

    - **리소스 종류** 뷰-hello에 사용 되는 hello 공용 보기 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040), 웹 응용 프로그램, 저장소 계정 및 가상 컴퓨터 등의 형식에 의해 분류 하 여 Azure 리소스를 보여 줍니다. 
    - **리소스 그룹** 보기-hello Azure 리소스 그룹 자신이 연결 하 여 분류 Azure 리소스입니다. 리소스 그룹은 일반적으로 특정 응용 프로그램에서 사용되는 Azure 리소스 번들입니다. Azure 리소스 그룹에 대해 자세히 toolearn 참조 [Azure 리소스 관리자 개요](./azure-resource-manager/resource-group-overview.md)합니다.

    hello 다음 이미지의 hello 비교 뷰 두 개가 표시 리소스:

    ![클라우드 탐색기 리소스 보기 비교](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a>클라우드 탐색기에서 리소스 보기 및 탐색
toonavigate tooan Azure 리소스와 클라우드 탐색기에서 해당 정보를 볼를 hello 항목의 유형 또는 연결 된 리소스 그룹을 확장 한 다음 hello 리소스를 선택 합니다. 리소스를 선택-hello 두 탭에 정보가 나타납니다 **동작** 및 **속성** -클라우드 탐색기 hello 맨 아래에 있습니다. 

- **작업** 탭-목록 hello 동작을 선택 하는 hello 리소스에 대 한 클라우드 탐색기에서 수행할 수 있습니다. 상황에 맞는 메뉴 리소스 tooview hello를 마우스 오른쪽 단추로 클릭 하 여 이러한 옵션을도 볼 수 있습니다.

- **속성** 탭-hello 리소스와 연관 된 해당 형식, 로캘 및 리소스 그룹과 같은 hello 속성을 보여 줍니다.

hello 다음 이미지 표시에 나타나는 각 탭 응용 프로그램 서비스에 대 한 예제 비교 하 여:

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

모든 리소스에 hello 동작 **포털에서 열기**합니다. 이 작업을 선택 하면 클라우드 탐색기에에서 표시 됩니다 hello 선택한 리소스 hello [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다. hello **포털에서 열기** 기능은 toodeeply 중첩 리소스를 탐색 하는 데 편리 합니다.

추가 작업 및 속성 값 hello Azure 리소스에 따라도 나타날 수 있습니다. 예를 들어, 웹 앱 및 논리 앱에도 있는 hello 동작 **브라우저에서 열기** 및 **디버거를 연결** 또한 너무**포털에서 열기**합니다. 저장소 계정 blob, 큐 또는 테이블을 선택 하면 작업 tooopen 편집기가 나타납니다. Azure 앱에는 **URL** 및 **상태** 속성이 있으며, 저장소 리소스에는 키와 연결 문자열 속성이 있습니다.

## <a name="find-resources-in-cloud-explorer"></a>클라우드 탐색기에서 리소스 찾기
hello에 hello 이름을 입력 하는 Azure 계정 가입에 특정 이름 가진 toolocate 리소스 **검색** 클라우드 탐색기에서 상자입니다.

![클라우드 탐색기에서 리소스 찾기](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

Hello에 문자를 입력할 때 **검색** hello 리소스 트리에 상자에서는 이러한 문자를 일치 하는 리소스에만 표시 합니다.

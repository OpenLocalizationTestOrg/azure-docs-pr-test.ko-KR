---
title: "Visual Studio 게시 Azure 응용 프로그램 마법사 aaaUsing hello | Microsoft Docs"
description: "Tooconfigure hello Visual Studio Azure 응용 프로그램 게시 마법사에서에서 다양 한 설정을 hello 하는 방법에 대해 알아봅니다"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d8f1ac9-e439-47e0-a183-0642c4ea1920
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3f0b580d0054cc246372597660d8ae317d9b8686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-visual-studio-publish-azure-application-wizard"></a>Hello Visual Studio Azure 응용 프로그램 게시 마법사를 사용 하 여
Visual Studio에서 웹 응용 프로그램을 개발한 후 hello를 사용 하 여 해당 응용 프로그램 tooan Azure 클라우드 서비스를 게시할 수 있습니다 **Azure 응용 프로그램 게시** 마법사. 

> [!NOTE]
> 이 항목은 서비스 toocloud 하지 tooweb 사이트 배포에 대 한 합니다. Tooweb 사이트를 배포 하는 방법에 대 한 정보를 참조 하십시오. [어떻게 tooDeploy Azure 웹 사이트](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false)합니다.
> 
> 

## <a name="accessing-hello-publish-azure-application-wizard"></a>Hello Azure 응용 프로그램 게시 마법사에 액세스

Visual Studio 프로젝트의 hello 형식에 따라 두 가지 방법으로 hello Azure 응용 프로그램 게시 마법사를 액세스할 수 있습니다.

**Azure 클라우드 서비스 프로젝트가 있는 경우:**

1. Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.

1. **솔루션 탐색기**, hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고, hello 상황에 맞는 메뉴에서 선택 **게시**합니다.

**Azure에서 사용되지 않는 웹 응용 프로그램 프로젝트가 있는 경우:**

1. Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.

1. **솔루션 탐색기**, hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고, hello 상황에 맞는 메뉴에서 선택 **변환** > **tooAzure 클라우드 서비스 프로젝트를 변환**합니다. 

1. **솔루션 탐색기**, hello 새로 만든 Azure 프로젝트를 마우스 오른쪽 단추로 클릭 하 고, hello 상황에 맞는 메뉴에서 선택 **게시**합니다.

## <a name="sign-in-page"></a>로그인 페이지

![로그인 페이지](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

**계정** -계정을 선택 하거나 선택 **계정 추가** hello 계정 드롭다운 목록에서 합니다.

**구독 선택** -배포에 대 한 구독 toouse hello를 선택 합니다.
   
## <a name="settings-page---common-settings-tab"></a>설정 페이지 - 일반 설정 탭   

![일반 설정](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

**클라우드 서비스** -hello 드롭다운을 선택 하 여 하거나 기존 클라우드 서비스 또는 선택  **&lt;새로 만들기 >**, 클라우드 서비스를 만듭니다. hello 데이터 센터는 각 클라우드 서비스에 대 한 괄호 안에 표시 됩니다. 데이터 센터 위치 hello hello 클라우드 서비스 수에 대 한 hello 동일 hello 저장소 계정 (고급 설정)에 대 한 데이터 센터 위치 hello로 것이 좋습니다.  

**환경** - **프로덕션** 또는 **스테이징** 중 하나를 선택합니다. 테스트 환경에서 스테이징 환경 toodeploy 하려는 경우 hello 응용 프로그램을 선택 합니다. 

**빌드 구성** - **디버그** 또는 **릴리스** 중 하나를 선택합니다.

**서비스 구성** - **클라우드** 또는 **로컬** 중 하나를 선택합니다.
   
**모든 역할에 대 한 원격 데스크톱 사용** -toobe 수 tooremotely 하려는 경우이 옵션의 선택을 toohello 서비스를 연결 합니다. 이 옵션은 주로 문제 해결을 위해 사용됩니다. 이 확인란을 선택 하면 hello **원격 데스크톱 구성** 대화 상자가 나타납니다. Hello 선택 **설정을** 링크 toochange hello 구성 합니다.
   
**모든 웹 역할에 대해 웹 배포 사용** -이 옵션을 hello 서비스에 대 한 tooenable 웹 배포를 확인 합니다. Hello를 선택 해야 **모든 역할에 원격 데스크톱 사용** 이 기능은 toouse 옵션입니다. 자세한 내용은 [[Visual Studio를 사용하여 Azure 클라우드 서비스 게시](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx)를 참조하세요. 

## <a name="settings-page---advanced-settings-tab"></a>설정 페이지 - 고급 설정 탭

![고급 설정](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

**배포 레이블** -hello 기본 이름을 그대로 적용 하거나 사용자가 선택 하는 이름을 입력 합니다. tooappend hello 날짜 toohello 배포 레이블, leave hello 확인란을 선택 합니다. 
   
**저장소 계정** -선택이 배포에 대 한 저장소 계정 toouse hello * *&lt;새로 만들기 > toocreate 저장소 계정입니다. hello 데이터 센터는 각 저장소 계정에 대 한 괄호 안에 표시 됩니다. 데이터 센터 위치 hello hello 저장소 계정 수에 대 한 hello 동일 hello 클라우드 서비스 (일반 설정)에 대 한 데이터 센터 위치 hello로 것이 좋습니다.  
   
Azure 저장소 계정 hello hello 응용 프로그램 배포에 대 한 hello 패키지를 저장합니다. Hello 응용 프로그램 배포 된 후 hello 패키지가 hello 저장소 계정에서 제거 됩니다.

**실패 시 배포 삭제** -게시 하는 동안 오류가 발생 하는 경우 삭제 되는이 옵션 toohave hello 배포를 선택 합니다. 이 선택 취소 해야 클라우드 서비스에 대 한 toomaintain 일정 한 가상 IP 주소를 선택 합니다.

**배포 업데이트** -toodeploy 구성 요소에만 업데이트 하려는 경우이 옵션을 선택 합니다. 이 유형의 배포는 전체 배포보다 빠를 수 있습니다. 클라우드 서비스에 대 한 toomaintain 일정 한 가상 IP 주소를 사용 하려는 경우이 확인 해야 합니다. 

**배포 업데이트-설정** -이 대화 상자를 사용 toofurther hello 역할 toobe 업데이트 하려는 방식을 지정 합니다. 선택 하면 **증분 업데이트**, 해당 hello 응용 프로그램은 항상 사용할 수 있도록 응용 프로그램의 각 인스턴스는 서로 하나씩 업데이트 합니다. 선택 하면 **동시 업데이트**, hello에 응용 프로그램의 모든 인스턴스가 업데이트 됩니다 동시 합니다. 동시 업데이트는 속도가 더 있지만 hello 업데이트 과정 인해 서비스를 사용할 수 있습니다. 

![배포 설정](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

**IntelliTrace를 활성화** -tooenable IntelliTrace 여부를 지정 합니다. IntelliTrace를 사용하여 Azure에서 실행할 때 역할 인스턴스에 대한 광범위한 정보를 기록할 수 있습니다. IntelliTrace 로그 toostep hello Azure에서 실행 중인 경우에 따라 toofind hello 원인을 해야 할 경우 Visual Studio에서 코드를 통해 사용할 수 있습니다. IntelliTrace 사용에 대한 자세한 내용은 [IntelliTrace 및 Visual Studio를 사용하여 게시된 Azure 클라우드 서비스 디버깅](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)을 참조하세요. 

**프로 파일링 사용** -tooenable 성능 프로 파일링 하려는 경우를 지정 합니다. Visual Studio 프로파일러 hello tooget을 hello 클라우드 서비스가 실행 되는 어떻게 계산 측면을 자세히 분석할 수 있습니다. Hello Visual Studio 프로파일러를 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [Azure 클라우드 서비스의 hello 성능을 테스트](./vs-azure-tools-performance-profiling-cloud-services.md)합니다.

**모든 역할에 원격 디버거 사용** -tooenable 원격 디버깅 하려는 경우를 지정 합니다. Visual Studio를 사용하여 클라우드 서비스를 디버그하는 방법에 대한 자세한 내용은 [Visual Studio에서 Azure 클라우드 서비스 또는 가상 컴퓨터 디버깅](./vs-azure-tools-debug-cloud-services-virtual-machines.md)을 참조하세요.

## <a name="diagnostics-settings-page"></a>진단 설정 페이지

![진단 설정](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

진단을 사용 tootroubleshoot Azure 클라우드 서비스 (또는 Azure 가상 컴퓨터) 있습니다. 진단에 대한 자세한 내용은 [Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 구성](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)을 참조하세요. Application Insights에 대한 자세한 내용은 [Application Insights란?](./application-insights/app-insights-overview.md)을 참조하세요.

## <a name="summary-page"></a>요약 페이지

![요약](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

**Profile을 대상** -하고자 하는 hello 설정에서 toocreate 게시 프로필을 선택할 수 있습니다. 예를 들어, 테스트 환경에 대한 하나의 프로필을 만들고 프로덕션용으로 다른 하나를 만들 수 있습니다. toosave이 프로필을 선택 hello **저장** 아이콘입니다. hello 마법사 hello 프로필을 만들고 hello Visual Studio 프로젝트에 저장 합니다. toomodify hello 프로필 이름에 열기 hello **profile을 대상** 목록에서 선택한 후 **< 관리... >**합니다.
   
   > [!NOTE]
   > hello 게시 프로필이 나타나고 Visual Studio의 솔루션 탐색기에서 및 hello 프로필 설정이 확장명이.azurePubxml tooa 파일에 기록 됩니다. 설정은 XML 태그의 특성으로 저장됩니다.
   > 
   > 

## <a name="publishing-your-application"></a>응용 프로그램 게시

프로젝트의 배포에 대 한 모든 hello 설정을 구성 하 고 나면 선택 **게시** hello hello 대화 상자 맨 아래에 있습니다. Hello에 hello 프로세스 상태를 모니터링할 수 **출력** Visual Studio의 창.

## <a name="next-steps"></a>다음 단계
- [마이그레이션 및 웹 응용 프로그램 tooan Visual Studio에서 Azure 클라우드 서비스 게시](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)
- [방법: Visual Studio toopublish toouse Azure 클라우드 서비스에 알아봅니다](./vs-azure-tools-publishing-a-cloud-service.md)
- [IntelliTrace 및 Visual Studio를 사용하여 게시된 Azure 클라우드 서비스 디버깅](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)
- [Azure 클라우드 서비스의 hello 성능을 테스트 합니다.](./vs-azure-tools-performance-profiling-cloud-services.md)
- [Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 구성](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) 
- [Application Insights란?](./application-insights/app-insights-overview.md)
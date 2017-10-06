---
title: "Azure 클라우드 서비스 및 가상 컴퓨터에 대 한 진단 aaaConfiguring | Microsoft Docs"
description: "설명 방법을 Azure 클라우드 서비스 및 가상 컴퓨터 (Vm) Visual Studio에서 디버깅을 위해 tooconfigure 진단 정보입니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: e70cd7b4-6298-43aa-adea-6fd618414c26
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 74cdf49413d6d89a84195070dd9d817da2463373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-diagnostics-for-azure-cloud-services-and-virtual-machines"></a>Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 구성
Azure 클라우드 서비스 또는 Azure 가상 컴퓨터 tootroubleshoot를 할 때 Visual Studio를 사용 하 여 Azure 진단을 보다 쉽게 구성할 수 있습니다. Azure 진단 hello 가상 컴퓨터 및 클라우드 서비스를 실행 하는 가상 컴퓨터 인스턴스에서 시스템 데이터 및 로깅 캡처하고 사용자가 선택한 저장소 계정에 해당 데이터를 전송 합니다. Azure에서 진단 로깅에 대한 자세한 내용은 [Azure App Service에서 웹앱에 대한 진단 로깅 설정](app-service-web/web-sites-enable-diagnostic-log.md)을 참조하세요.

이 항목에서는 tooenable 및 Azure 가상 컴퓨터 뿐만 아니라, 배포 전과 후 모두 Visual Studio에서 Azure 진단을 구성 합니다. 또한 표시 방법을 tooselect hello 유형의 진단 정보 toocollect 및 tooview hello 정보 수집 되는 방법입니다.

다음 방법으로 hello에서 Azure 진단을 구성할 수 있습니다.

* Hello 통해 진단 구성 설정을 변경할 수 있습니다 **진단 구성** Visual Studio에서 대화 상자. hello 설정은 diagnostics.wadcfgx (Azure SDK 2.4 또는 이전 버전에 diagnostics.wadcfg) 라는 파일에 저장 됩니다. 또는 hello 구성 파일을 직접 수정할 수 있습니다. Hello 파일을 수동으로 업데이트 hello 클라우드 서비스 tooAzure 또는 hello 에뮬레이터의 hello 실행된 서비스를 배포한 다음 대개 hello 구성 변경 내용을 적용 hello를 사용 합니다.
* 사용 하 여 **클라우드 탐색기** 또는 **서버 탐색기** 실행 중인 클라우드 서비스 또는 가상 컴퓨터에 대 한 Visual Studio toochange hello 진단 설정 합니다.

## <a name="azure-26-diagnostics-changes"></a>Azure 2.6 진단 변경
Visual Studio에서 Azure SDK 2.6 프로젝트에 대 한 변경 내용을 따라 hello 수행 됩니다. (이러한 변경 내용을 적용할 수도 toolater 버전의 Azure SDK.)

* hello 로컬 에뮬레이터는 이제 진단을 지원합니다. 즉, 진단 데이터를 수집 하 고 응용 프로그램은 hello 오른쪽 추적 생성 개발 하 고 Visual Studio에서 테스트 하는 동안 확인 수 있습니다. 연결 문자열 hello `UseDevelopmentStorage=true` hello Azure 저장소 에뮬레이터를 사용 하 여 Visual Studio에서 클라우드 서비스 프로젝트를 실행 하는 동안 진단 데이터 수집을 사용 합니다. Hello (개발 저장소) 저장소 계정에서 모든 진단 데이터 수집 됩니다.
* hello 진단 저장소 계정 연결 문자열 (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) hello 서비스 구성 (.cscfg) 파일에 다시 저장 됩니다. Azure SDK 2.5에서 hello 진단 저장소 계정은 hello diagnostics.wadcfgx 파일에 지정 되었습니다.

Azure SDK 2.4 및 이전 버전 hello 연결 문자열의 작동 방법 및 Azure SDK 2.6 이상 작동 방식에 몇 가지 주목할 만한 차이점 있습니다.

* Azure SDK 2.4 및 이전 버전에서는 hello 연결 문자열이 사용 되었습니다 런타임 hello 진단 플러그 인 tooget hello 저장소 계정 정보로 진단 로그를 전송에 대 한 합니다.
* Azure SDK 2.6 이상 버전에서 게시 하는 동안 hello 적절 한 저장소 계정 정보로 Visual Studio tooconfigure hello 진단 확장에서 hello 진단 연결 문자열이 사용 됩니다. hello 연결 문자열에는 Visual Studio에서 게시할 때 사용할 다른 서비스 구성에 대 한 다른 저장소 계정을 정의할 수 있습니다. 그러나 hello 진단 플러그 인 (Azure SDK 2.5) 한 후 사용할 수 없게 되었기 때문에 hello.cscfg 파일이 자체적으로 hello 진단 확장을 사용할 수 없습니다. Visual Studio 또는 PowerShell과 같은 도구를 통해 개별적으로 tooenable hello 확장 프로그램이 있는 합니다.
* PowerShell을 사용 하 여 hello 진단 확장 구성의 toosimplify hello 프로세스를 Visual Studio의 패키지 출력 hello hello 공용 구성 XML에 대 한 각 역할에 대 한 hello 진단 확장도 포함 됩니다. Visual Studio hello 진단 연결 문자열 toopopulate hello 저장소 계정 정보 hello 공용 구성에 사용합니다. hello 공용 구성 파일은 hello 확장 폴더에 만들어지며 PaaSDiagnostics hello 패턴을 따릅니다. &lt;역할 이름 >. PubConfig.xml 합니다. 모든 PowerShell 기반 배포는 각 구성 tooa 역할 패턴 toomap이 사용할 수 있습니다.
* hello.cscfg 파일에서 연결 문자열 hello를 사용 하 hello [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040) tooaccess hello에 나타날 수 있도록 진단 데이터를 hello **모니터링** 탭 hello 연결 문자열이 필요 tooconfigure hello 서비스 tooshow 자세한 정보 표시 hello 포털에서 데이터를 모니터링 합니다.

## <a name="migrating-projects-tooazure-sdk-26-and-later"></a>마이그레이션 프로젝트 tooAzure SDK 2.6 이상
Azure SDK 2.5 tooAzure SDK 2.6에서에서 마이그레이션 또는 그 이후 버전 hello.wadcfgx 파일에 지정 된 진단 저장소 계정을 사용 했던 경우 다음이 계속 유지 됩니다. 다른 저장소 구성에 대 한 다른 저장소를 사용 하 여 hello 유연성 tootake 활용 계정, toomanually hello 연결 문자열 tooyour 프로젝트에 추가 해야 합니다. Azure SDK 2.4 또는 이전 tooAzure SDK 2.6에서 프로젝트를 마이그레이션하는, 진단 연결 문자열이 유지 됩니다를 hello 합니다. 그러나 hello 변경 내용 처리 방법에 연결 문자열은 Azure SDK 2.6에서 지정 된 대로 hello 이전 단원의 note 하십시오.

### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Visual Studio hello 진단 저장소 계정을 결정 하는 방법
* Hello.cscfg 파일에 진단 연결 문자열이 지정 된, Visual Studio 사용 tooconfigure hello 진단 확장을 게시 하면 및 패키징 시 hello 공용 구성 xml 파일을 생성할 때 합니다.
* 진단 연결 문자열이 없는 hello.cscfg 파일에 지정 된, 다음 Visual Studio를 대신 hello.wadcfgx 파일 tooconfigure hello 진단 확장을 게시 하 고 hello 공개를 생성 하는 경우에 지정 된 toousing hello 저장소 계정 구성 xml 파일 패키징할 때 있습니다.
* hello.cscfg 파일에 진단 연결 문자열 hello hello.wadcfgx 파일의 저장소 계정 hello 보다 우선합니다. 진단 연결 문자열은 hello.cscfg 파일에 지정 된 다음 Visual Studio를 사용 하 고 무시.wadcfgx의 저장소 계정을 hello 됩니다.

### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>"... 개발 저장소 연결 문자열 업데이트" hello 않는 내용 확인란의 기능은 무엇입니까?
에 대 한 확인란 hello **tooMicrosoft Azure에 게시할 때 진단 및 캐싱을 위한 개발 저장소 연결 문자열을 Microsoft Azure 저장소 계정 자격 증명으로 업데이트** 하면 편리 tooupdate 어떤 게시 하는 동안 지정 된 hello Azure 저장소 계정으로 개발 저장소 계정 연결 문자열입니다.

예를 들어이 확인란을 선택 하 고 hello 진단 연결 문자열 지정 `UseDevelopmentStorage=true`합니다. Hello 프로젝트 tooAzure를 게시 하면 Visual Studio hello 게시 마법사에서 지정한 hello 스토리지 계정으로 hello 진단 연결 문자열을 자동으로 업데이트 합니다. 그러나 실제 저장소 계정을 hello 진단 연결 문자열로 지정 된 경우 다음 해당 계정은 대신 사용 됩니다.

## <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Azure SDK 2.4 이하 및 Azure SDK 2.5 이상 간의 진단 기능 차이점
Azure SDK 2.4 tooAzure SDK 2.5 이상에서 프로젝트를 업그레이드 하는 경우에 유의 hello 진단 기능의 차이 다음에 주의 해야 합니다.

* **구성 API가 더 이상 사용되지 않음** – 진단의 프로그래밍 방식 구성은 Azure SDK 2.4 이하 버전에서는 사용할 수 있지만 Azure SDK 2.5 이상 버전에서는 더 이상 사용되지 않습니다. 코드에서 진단 구성에 현재 정의 된 hello 마이그레이션된 프로젝트에서 진단 tookeep 작업에 대 한 처음부터 이러한 설정을 tooreconfigure 필요 합니다. Azure SDK 2.4 용 hello 진단 구성 파일 diagnostics.wadcfg이 고 Azure SDK 2.5 이상 diagnostics.wadcfgx 됩니다.
* **클라우드 서비스 응용 프로그램에 대 한 진단 hello 인스턴스 수준이 아닌 hello 역할 수준에서 구성할 수만 있습니다.**
* **Hello 진단 구성이 업데이트 될 때마다 응용 프로그램을 배포한** -서버 탐색기에서 진단 구성을 변경한 다음 응용 프로그램을 다시 배포 하는 경우이 패리티 문제가 발생할 수 있습니다.
* **크래시 덤프 코드에 없는 hello 진단 구성 파일에서 구성 된 Azure SDK 2.5 이상 버전에서는** -코드에 구성 된 크래시 덤프를 설정한 경우 toomanually 전송 hello 구성 코드 toohello 구성 파일에서 hello 크래시 덤프 때문에 hello 마이그레이션 tooAzure SDK 2.6 하는 동안 전송 되지 않습니다.

## <a name="enable-diagnostics-in-cloud-service-projects-before-deploying-them"></a>배포 전에 클라우드 서비스 프로젝트에서 진단을 사용하도록 설정
Visual Studio에서 배포 하기 전에 hello 에뮬레이터의 hello 서비스를 실행 하는 경우 Azure에서 실행 되는 역할에 대 한 toocollect 진단 데이터를 선택할 수 있습니다. Visual Studio의 모든 변경 내용을 toodiagnostics 설정 hello diagnostics.wadcfgx 구성 파일에 저장 됩니다. 이러한 구성 설정은 클라우드 서비스를 배포할 때 진단 데이터가 저장 되는 hello 저장소 계정을 지정 합니다.

[!INCLUDE [cloud-services-wad-warning](../includes/cloud-services-wad-warning.md)]

### <a name="tooenable-diagnostics-in-visual-studio-before-deployment"></a>배포 하기 전에 Visual Studio에서 tooenable 진단
1. Hello 관심 있는 hello 역할에 대 한 바로 가기 메뉴를 선택 **속성**, hello 선택 **구성** hello 역할 탭 **속성** 창.
2. Hello에 **진단** 섹션에, 해당 hello 반드시 **진단 사용** 확인란을 선택 합니다.
   
    ![Hello 진단 사용 옵션 액세스](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796660.png)
3. 저장 된 hello 진단 데이터 toobe 저장할 hello 줄임표 (...) 단추 toospecify hello 저장소 계정을 선택 합니다. 선택한 hello 저장소 계정은 진단 데이터가 저장 되는 hello 위치 됩니다.
   
    ![저장소 계정 toouse hello를 지정 합니다.](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796661.png)
4. Hello에 **저장소 연결 문자열 만들기** 대화 상자를 원하는 tooconnect hello Azure 저장소 에뮬레이터, Azure 구독을 사용 하 여 연결 하거나 수동으로 입력 한 자격 증명 있는지를 지정 합니다.
   
    ![저장소 계정 대화 상자](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796662.png)
   
   * Hello 연결 문자열이 tooUseDevelopmentStorage 설정 될 hello Microsoft Azure 저장소 에뮬레이터 옵션을 선택 하면 = true입니다.
   * Hello 구독 옵션을 선택한 경우에 hello toouse 및 hello 계정 이름을 사용 하려는 Azure 구독을 선택할 수 있습니다. 계정 관리 hello 단추 toomanage Azure 구독을 선택할 수 있습니다.
   * Hello 수동으로 입력 한 자격 증명 옵션을 선택 하는 경우 증명된 tooenter hello 이름 및 키의 hello toouse를 원하는 Azure 계정.
5. Hello 선택 **구성** 단추 tooview hello **진단 구성** 대화 상자. **일반** 및 **로그 디렉터리**를 제외한 각 탭은 수집할 수 있는 진단 데이터 원본을 나타냅니다. hello 기본 탭 **일반**, 진단 데이터 수집 옵션 다음 hello 제공: **오류만**, **모든 정보**, 및 **사용자 지정 계획** . 기본 옵션인 hello **오류만**, 경고 또는 추적 메시지를 전송 하지 않기 때문에 최소한의 저장소를 hello 합니다. 따라서 모든 정보 옵션 전송을 대부분의 정보를 hello 및 이면 hello 저장소 측면에서 가장 비용이 많이 드는 옵션을 hello 합니다.
   
    ![Azure 진단 및 구성 사용](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
6. 이 예에서는 선택 hello **사용자 지정 계획** 옵션 hello 데이터를 사용자 지정할 수 있도록 수집 합니다.
7. hello **디스크 할당량 (MB)** 상자 진단 데이터에 대 한 tooallocate에서 원하는 공간 저장소 계정을 지정 합니다. 원하는 경우 hello 기본값을 변경할 수 있습니다.
8. 원하는 toocollect, 진단 데이터의 각 탭에서 해당 **전송 사용 <log type>**  확인란 합니다. 예를 들어 toocollect 응용 프로그램 로그를 선택 hello **응용 프로그램 로그 전송 사용** hello 확인란 **응용 프로그램 로그** 탭 합니다. 또한 각 진단 데이터 형식에 필요한 기타 정보를 지정합니다. Hello 섹션을 참조 **진단 데이터 원본을 구성** 이 항목 뒷부분의 각 탭에 구성 정보에 대 한 합니다.
9. 원하는 모든 hello 진단 데이터의 컬렉션을 활성화 한 후 선택 hello **확인** 단추입니다.
10. 평상시처럼 Visual Studio에서 Azure 클라우드 서비스 프로젝트를 실행합니다. 응용 프로그램을 사용 하 여 지정한 toohello Azure 저장소 계정은 사용 하도록 설정한 hello 로그 정보에 저장 됩니다.

## <a name="enable-diagnostics-in-azure-virtual-machines"></a>Azure 가상 컴퓨터에서 진단 사용
Visual Studio에서 Azure 가상 컴퓨터에 대 한 toocollect 진단 데이터를 선택할 수 있습니다.

### <a name="tooenable-diagnostics-in-azure-virtual-machines"></a>Azure 가상 컴퓨터에서 tooenable 진단
1. **서버 탐색기**, hello Azure 노드를 선택 하 고 다음 연결 되어 있지 않은 경우 tooyour Azure 구독을 연결 합니다.
2. Hello 확장 **가상 컴퓨터** 노드. 새 가상 컴퓨터를 만들거나 이미 있는 가상 컴퓨터를 선택할 수 있습니다.
3. Hello 관심 있는 hello 가상 컴퓨터에 대 한 바로 가기 메뉴에서 선택 **구성**합니다. Hello 가상 컴퓨터 구성 대화 상자를 표시 합니다.
   
    ![Azure 가상 컴퓨터 구성](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796663.png)
4. 설치 되어 있지 않은 경우 hello Microsoft 모니터링 에이전트 진단 확장을 추가 합니다. 이 확장 프로그램에서는 hello Azure 가상 컴퓨터에 대 한 진단 데이터를 수집할 수 있습니다. Hello 설치 된 확장 목록의 hello Select는 사용 가능한 확장 드롭다운 메뉴를 선택 하 고 Microsoft 모니터링 에이전트 진단을 선택 합니다.
   
    ![Azure 가상 컴퓨터 확장 설치](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766024.png)
   
   > [!NOTE]
   > 다른 진단 확장은 가상 컴퓨터에 대해 사용할 수 있습니다. 자세한 내용은 Azure VM 확장 및 기능을 참조하세요.
   > 
   > 
5. Hello 선택 **추가** tooadd hello 확장과 보기 단추 해당 **진단 구성** 대화 상자.
6. Hello 선택 **구성** 단추 toospecify 저장소 계정을 선택한 후 hello **확인** 단추입니다.
   
    **일반** 및 **로그 디렉터리**를 제외한 각 탭은 수집할 수 있는 진단 데이터 원본을 나타냅니다.
   
    ![Azure 진단 및 구성 사용](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
   
    hello 기본 탭 **일반**, 진단 데이터 수집 옵션 다음 hello 제공: **오류만**, **모든 정보**, 및 **사용자 지정 계획** . 기본 옵션인 hello **오류만**, 경고 또는 추적 메시지를 전송 하지 않기 때문에 최소한의 저장소를 hello 합니다. hello **모든 정보** 옵션 전송 hello 대부분의 정보를 따라서 hello 가장 비용이 많이 드는 옵션 저장소를 기준으로 합니다.
7. 이 예에서는 선택 hello **사용자 지정 계획** 옵션 hello 데이터를 사용자 지정할 수 있도록 수집 합니다.
8. hello **디스크 할당량 (MB)** 상자 진단 데이터에 대 한 tooallocate에서 원하는 공간 저장소 계정을 지정 합니다. 원하는 경우 hello 기본값을 변경할 수 있습니다.
9. 원하는 toocollect, 진단 데이터의 각 탭에서 해당 **전송 사용 <log type>**  확인란 합니다.
   
    예를 들어 toocollect 응용 프로그램 로그를 선택 hello **응용 프로그램 로그 전송 사용** hello 확인란 **응용 프로그램 로그** 탭 합니다. 또한 각 진단 데이터 형식에 필요한 기타 정보를 지정합니다. Hello 섹션을 참조 **진단 데이터 원본을 구성** 이 항목 뒷부분의 각 탭에 구성 정보에 대 한 합니다.
10. 원하는 모든 hello 진단 데이터의 컬렉션을 활성화 한 후 선택 hello **확인** 단추입니다.
11. 업데이트 하는 hello 프로젝트를 저장 합니다.
    
     Hello에 메시지가 표시 됩니다 **Microsoft Azure 활동 로그** 가상 컴퓨터를 hello 창 업데이트 되었습니다.

## <a name="configure-diagnostics-data-sources"></a>진단 데이터 원본 구성
진단 데이터 수집을 활성화 한 후에 정확히 toocollect 및 수집 되는 정보를 원하는 데이터 소스를 선택할 수 있습니다. hello 다음은 hello 탭 목록과 **진단 구성** 대화 상자와 각 구성 옵션을 의미 합니다.

### <a name="application-logs"></a>응용 프로그램 로그
**응용 프로그램 로그** 는 웹 응용 프로그램에서 생성된 진단 정보를 포함합니다. Toocapture 응용 프로그램 로그를 사용 하도록 하려는 경우 선택 hello **응용 프로그램 로그 전송 사용** 확인란 합니다. 늘리거나 hello hello 응용 프로그램 로그는 전송 될 때 분 수를 줄일 수 hello를 변경 하 여 저장소 계정 tooyour **전송 기간 (분)** 값입니다. Hello hello 로그 수준 값을 설정 하 여 hello 로그에 캡처되는 정보의 양을 변경할 수도 있습니다. 예를 들어 선택할 수 있습니다 **Verbose** tooget 자세한 정보를 선택할지 **위험** toocapture 심각한 오류. 응용 프로그램 로그를 내보내는 특정 진단 공급자가 있으면 hello 공급자 GUID toohello를 추가 하 여 캡처할 수 있습니다 **공급자 GUID** 상자입니다.

  ![응용 프로그램 로그](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758145.png)

  응용 프로그램 로그에 대한 자세한 내용은 [Azure App Service에서 웹앱에 대한 진단 로깅 설정](app-service-web/web-sites-enable-diagnostic-log.md)을 참조하세요.

### <a name="windows-event-logs"></a>Windows 이벤트 로그
Toocapture Windows 이벤트 로그를 사용 하도록 하려는 경우 선택 hello **Windows 이벤트 로그 전송 사용** 확인란 합니다. 늘리거나 hello hello 이벤트 로그는 전송 될 때 분 수를 줄일 수 hello를 변경 하 여 저장소 계정 tooyour **전송 기간 (분)** 값입니다. Hello hello 유형의 tootrack 원하는 이벤트에 대 한 확인란을 선택 합니다.

  ![이벤트 로그](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796664.png)

Azure SDK 2.6 이상을 사용 하는 사용자 지정 데이터 원본 toospecify 원하는 경우 hello에 입력  **<Data source name>**  텍스트 상자를 선택한 후 hello **추가** 다음 tooit 단추입니다. hello 데이터 원본은 toohello diagnostics.cfcfg 파일에 추가 됩니다.

Azure SDK 2.5를 사용 하는 사용자 지정 데이터 원본 toospecify 원하는 하는 경우 추가할 수 있습니다 toohello `WindowsEventLog` hello 다음 예제와 같이 hello diagnostics.wadcfgx의 섹션 파일입니다.

```
<WindowsEventLog scheduledTransferPeriod="PT1M">
   <DataSource name="Application!*" />
   <DataSource name="CustomDataSource!*" />
</WindowsEventLog>
```
### <a name="performance-counters"></a>성능 카운터
성능 카운터 정보는 시스템 병목 지점을 찾고 시스템 및 응용 프로그램 성능을 미세하게 조정하는 데 도움이 될 수 있습니다. 자세한 내용은 [Azure 응용 프로그램에서 성능 카운터 만들기 및 사용](https://msdn.microsoft.com/library/azure/hh411542.aspx) 을 참조하세요. Toocapture 성능 카운터를 사용 하도록 하려는 경우 선택 hello **성능 카운터 전송 사용** 확인란 합니다. 늘리거나 hello hello 이벤트 로그는 전송 될 때 분 수를 줄일 수 hello를 변경 하 여 저장소 계정 tooyour **전송 기간 (분)** 값입니다. Hello 성능 카운터에 대 tootrack 원하는 hello 확인란을 선택 합니다.

  ![성능 카운터](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758147.png)

tootrack 나열 되지 않은 성능 카운터를 사용 하 여 입력 제안 된 구문을 hello를 선택한 후 hello **추가** 단추입니다. hello 가상 컴퓨터에서 운영 체제 hello 추적할 수 있는 성능 카운터를 결정 합니다. 구문에 대한 자세한 내용은 [카운터 경로 지정](https://msdn.microsoft.com/library/windows/desktop/aa373193.aspx)을 참조하세요.

### <a name="infrastructure-logs"></a>인프라 로그
Hello Azure 진단 인프라, RemoteAccess 모듈 hello 및 hello RemoteForwarder 모듈에 대 한 정보를 포함 하는 toocapture 인프라 로그 선택 hello **인프라로그전송사용**확인란 합니다. 늘리거나 hello hello 로그는 전송 될 때 분 수를 줄일 수 hello 전송 기간 (분) 값을 변경 하 여 tooyour 저장소 계정입니다.

  ![진단 인프라 로그](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758148.png)

  자세한 내용은 [Azure 진단을 사용하여 로깅 데이터 수집](https://msdn.microsoft.com/library/azure/gg433048.aspx) 을 참조하세요.

### <a name="log-directories"></a>로그 디렉터리
인터넷 정보 서비스 (IIS) 요청에 대 한 로그 디렉터리에서 수집 된 데이터가 들어 있는 toocapture 로그 디렉터리를 실패 한 요청 또는 사용자가 선택 하는 폴더 선택 hello **로그디렉터리전송사용**확인란 합니다. 늘리거나 hello hello 로그는 전송 될 때 분 수를 줄일 수 hello를 변경 하 여 저장소 계정 tooyour **전송 기간 (분)** 값입니다.

Hello 상자와 같은 toocollect, 원하는 hello 로그를 선택할 수 있습니다 **IIS 로그** 및 **실패 한 요청** 로그 합니다. 기본 저장소 컨테이너 이름이 제공 되지만 원하는 경우 hello 이름을 변경할 수 있습니다.

또한 모든 폴더에서 로그를 캡처할 수 있습니다. Hello에 hello 경로 지정 **절대 디렉터리의 로그** 섹션 선택한 후 hello **디렉터리 추가** 단추입니다. hello 로그 캡처됩니다 toohello 컨테이너를 지정 합니다.

  ![로그 디렉터리](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796665.png)

### <a name="etw-logs"></a>ETW 로그
사용 하는 경우 [Windows 용 이벤트 추적](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx) (ETW) 및 선택 hello toocapture ETW 로그 **ETW 로그 전송 사용** 확인란 합니다. 늘리거나 hello hello 로그는 전송 될 때 분 수를 줄일 수 hello를 변경 하 여 저장소 계정 tooyour **전송 기간 (분)** 값입니다.

지정한 이벤트 매니페스트와 이벤트 원본에서 hello 이벤트가 캡처됩니다. hello에 이름을 입력 하는 이벤트 소스를 toospecify **이벤트 소스** 섹션 고 hello를 눌러 **이벤트 원본 추가** 단추입니다. 마찬가지로, hello에서 이벤트 매니페스트를 지정할 수 있습니다 **이벤트 매니페스트** 섹션 선택한 후 hello **이벤트 매니페스트 추가** 단추입니다.

  ![ETW 로그](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766025.png)

  hello ETW 프레임 워크는 hello [System.Diagnostics.aspx] (https://msdn.microsoft.com/library/system.diagnostics (v = vs.110) 네임 스페이스의 클래스를 통해 ASP.NET에서 지원 됩니다. 상속 하 고 [System.Diagnostics.aspx] (https://msdn.microsoft.com/library/system.diagnostics (v = vs.110) 클래스를 사용 하면 hello 사용 [System.Diagnostics.aspx] (표준 확장 hello Microsoft.WindowsAzure.Diagnostics 네임 스페이스 https://msdn.microsoft.com/library/system.diagnostics (v = vs.110) hello Azure 환경에서에서 로깅 프레임 워크입니다. 자세한 내용은 [Microsoft Azure에서 로깅 및 추적 관리](https://msdn.microsoft.com/magazine/ff714589.aspx) 및 [Azure Cloud Services 및 Virtual Machines에서 진단 사용](cloud-services/cloud-services-dotnet-diagnostics.md)을 참조하세요.

### <a name="crash-dumps"></a>크래시 덤프
역할 인스턴스가 충돌할 경우에 대 한 toocapture 정보를 원할 경우 선택 hello **크래시 덤프 전송 사용** 확인란 합니다. ASP.NET에서는 대부분의 예외를 처리하기 때문에 이는 일반적으로 작업자 역할에 대해서만 유용합니다. 늘리거나 hello 비율의 저장소를 줄일 수 공간 할당 되어 hello를 변경 하 여 toohello 크래시 덤프 **디렉터리 할당량 (%)** 값입니다. 여기서 hello 크래시 덤프가 저장 되 고 toocapture 할지 여부를 선택할 수 있습니다 hello 저장소 컨테이너를 변경할 수는 **전체** 또는 **미니** 덤프 합니다.

현재 추적 중인 hello 프로세스가 나열 됩니다. Hello toocapture hello 프로세스에 대 한 확인란을 선택 합니다. tooadd 다른 프로세스 toohello 목록 hello 프로세스 이름을 입력 하 고 hello를 눌러 **프로세스 추가** 단추입니다.

  ![크래시 덤프](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766026.png)

  자세한 내용은 [Microsoft Azure에서 로깅 및 추적 관리](https://msdn.microsoft.com/magazine/ff714589.aspx) 및 [Microsoft Azure 진단 4부: 사용자 지정 로깅 구성 요소 및 Azure 진단 1.3 변경 내용](http://justazure.com/microsoft-azure-diagnostics-part-4-custom-logging-components-azure-diagnostics-1-3-changes/)(영문)을 참조하세요.

## <a name="view-hello-diagnostics-data"></a>Hello 진단 데이터 보기
클라우드 서비스 또는 가상 컴퓨터에 대 한 hello 진단 데이터를 수집 했으면를 볼 수 있습니다.

### <a name="tooview-cloud-service-diagnostics-data"></a>tooview 클라우드 서비스 진단 데이터
1. 일반적인 방법으로 클라우드 서비스를 배포하고 실행합니다.
2. 저장소 계정에 Visual Studio에서 생성 하는 보고서 또는 테이블에서 hello 진단 데이터를 볼 수 있습니다. tooview hello 보고서의에서 데이터를 열고 **클라우드 탐색기** 또는 **서버 탐색기**을, 관심 있는 hello 역할에 대 한 hello 노드의 hello 바로 가기 메뉴를 열고 다음 선택 **진단 데이터 보기** .
   
    ![진단 데이터 보기](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748912.png)
   
    Hello 사용 가능한 데이터를 표시 하는 보고서에 표시 됩니다.
   
    ![Visual Studio에서 Microsoft Azure 진단 보고서](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796666.png)
   
    Hello 가장 최근 데이터가 표시 되지 않으면 전송 기간 tooelapse hello에 대 한 toowait을 할 수 있습니다.
   
    Hello 선택 **새로 고침** tooimmediately 업데이트 hello 데이터를 연결 하거나 hello에서 선택 하는 간격 **자동 새로 고침** 드롭다운 목록 상자 toohave hello 데이터 자동으로 업데이트 합니다. tooexport hello 오류 데이터 선택 hello **tooCSV 내보내기** 단추 toocreate 쉼표로 구분 된 값 파일 스프레드시트에서 열 수 있습니다.
   
    **클라우드 탐색기** 또는 **서버 탐색기**, hello 배포와 관련 된 hello 저장소 계정을 엽니다.
3. Hello 테이블 뷰어에 hello 진단 테이블을 열고 hello 수집한 데이터를 검토 합니다. IIS 로그 및 사용자 지정 로그인 경우 BLOB 컨테이너를 열 수 있습니다. 다음 표에서 hello를 검토 하 여 관심 있는 hello 데이터를 포함 하는 hello 테이블 또는 blob 컨테이너를 찾을 수 있습니다. 또한 toohello 데이터에 대 한 로그 파일, hello 테이블 항목 포함 EventTickCount, DeploymentId, 역할 및 가상 컴퓨터 및 역할을 식별 하는 RoleInstance toohelp hello 데이터 생성 및 시기. 
   
   | 진단 데이터 | 설명 | 위치 |
   | --- | --- | --- |
   | 응용 프로그램 로그 |Hello System.Diagnostics.Trace 클래스의 메서드를 호출 하 여 코드를 생성 하는 로그입니다. |WADLogsTable |
   | 이벤트 로그 |Hello 가상 컴퓨터의 hello Windows 이벤트 로그에서이 데이터는입니다. 이러한 로그에 정보를 저장 하는 Windows 있지만 응용 프로그램 및 서비스 수도 tooreport 오류를 사용 하거나 정보를 기록 합니다. |WADWindowsEventLogsTable |
   | 성능 카운터 |Hello 가상 컴퓨터에서 사용할 수 있는 성능 카운터에서 데이터를 수집할 수 있습니다. hello 운영 체제 메모리 사용량 및 프로세서 시간 등의 여러 통계를 포함 하는 성능 카운터를 제공 합니다. |WADPerformanceCountersTable |
   | 인프라 로그 |이러한 로그는 hello 진단 인프라 자체에서 생성 됩니다. |WADDiagnosticInfrastructureLogsTable |
   | IIS 로그 |이러한 로그는 웹 요청을 기록합니다. 클라우드 서비스에서 상당한 양의 트래픽을 가져오는 경우 이러한 로그가 매우 길어질 수 있으므로 필요할 때만 이 데이터를 수집 및 저장해야 합니다. |Wad-iis-failedreqlogs 해당 배포, 역할 및 인스턴스에 대 한 경로 아래의 blob 컨테이너 hello에에서 실패 한 요청 로그를 찾을 수 있습니다. 전체 로그는 wad-iis-logfiles 아래에서 찾을 수 있습니다. 각 파일에 대 한 항목은 WADDirectories 테이블 hello에서에서 이루어집니다. |
   | 크래시 덤프 |이 정보는 클라우드 서비스 프로세스의 이진 이미지를 제공합니다(일반적으로 작업자 역할). |wad-crush-dumps BLOB 컨테이너 |
   | 사용자 지정 로그 파일 |미리 정의된 데이터의 로그입니다. |저장소 계정에 사용자 지정 로그 파일의 코드 hello 위치에 지정할 수 있습니다. 예를 들어, 사용자 지정 BLOB 컨테이너를 지정할 수 있습니다. |
4. 모든 형식의 데이터가 잘린 경우 해당 데이터 형식이 나 줄이기 hello hello 가상 컴퓨터 tooyour 저장소 계정에서 데이터의 전송 간격에 대 한 증가 hello 버퍼를 시도할 수 있습니다.
5. (선택 사항) Hello 저장소에서 데이터 제거를 고려한 가끔 tooreduce 전체 저장소 비용입니다.
6. 전체 배포를 수행 하는 경우 hello diagnostics.cscfg 파일 (Azure SDK 2.5 용.wadcfgx)는 Azure에서 업데이트 되 고 모든 변경 내용 tooyour 진단 구성이 클라우드 서비스 선택 합니다. 대신, 기존 배포를 업데이트 하면, Azure에서 hello.cscfg 파일이 업데이트 되지 않습니다. 여전히 진단 설정을 hello 다음 섹션의 hello 단계를 수행 하 여 하지만 변경할 수 있습니다. 전체 배포 및 기존 배포 업데이트에 대한 자세한 내용은 [Azure 응용 프로그램 게시 마법사](vs-azure-tools-publish-azure-application-wizard.md)를 참조하세요.

### <a name="tooview-virtual-machine-diagnostics-data"></a>tooview 가상 컴퓨터 진단 데이터
1. Hello hello 가상 컴퓨터에 대 한 바로 가기 메뉴에서 선택 **진단 데이터 보기**합니다.
   
    ![Azure 가상 컴퓨터에서 진단 데이터 보기](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766027.png)
   
    Hello 열립니다 **진단 요약** 창.
   
    ![Azure 가상 컴퓨터 진단 요약](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796667.png)  
   
    Hello 가장 최근 데이터가 표시 되지 않으면 전송 기간 tooelapse hello에 대 한 toowait을 할 수 있습니다.
   
    Hello 선택 **새로 고침** tooimmediately 업데이트 hello 데이터를 연결 하거나 hello에서 선택 하는 간격 **자동 새로 고침** 드롭다운 목록 상자 toohave hello 데이터 자동으로 업데이트 합니다. tooexport hello 오류 데이터 선택 hello **tooCSV 내보내기** 단추 toocreate 쉼표로 구분 된 값 파일 스프레드시트에서 열 수 있습니다.

## <a name="configure-cloud-service-diagnostics-after-deployment"></a>배포 후 클라우드 서비스 진단 구성
클라우드 서비스의 문제를 조사 하려는 해당 이미 실행 되 고, 경우에 원래 배포 된 hello 역할 하기 전에 지정 하지 않은 toocollect 데이터를 할 수 있습니다. 이 경우 시작할 수 있습니다 toocollect 데이터 서버 탐색기에서 hello 설정을 사용 하 여. 열었는지에 따라 hello 진단 구성 대화 상자 hello 인스턴스나 hello 역할에 대 한 hello 바로 가기 메뉴에서 역할의 단일 인스턴스 또는 모든 hello 인스턴스 중 하나에 대 한 진단을 구성할 수 있습니다. Hello 역할 노드를 구성 하는 경우 변경 내용을 tooall 인스턴스에 적용 됩니다. Hello 인스턴스 노드를 구성 하는 경우 변경 내용을 toothat 인스턴스에만을 적용 됩니다.

### <a name="tooconfigure-diagnostics-for-a-running-cloud-service"></a>실행 중인 클라우드 서비스에 대 한 tooconfigure 진단
1. 서버 탐색기에서 확장 hello **클라우드 서비스** 노드를 차례로 노드 toolocate hello 역할 또는 tooinvestigate 또는 둘 다 원하는 인스턴스를 확장 합니다.
   
    ![진단 구성](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748913.png)
2. 인스턴스 노드나 역할 노드에 대 한 hello 바로 가기 메뉴에서 선택 **진단 설정 업데이트**, hello toocollect 원하는 진단 설정을 선택 합니다.
   
    Hello 구성 설정에 대 한 정보를 참조 하십시오. **진단 데이터 원본을 구성** 이 항목의 합니다. Tooview 진단 데이터를 hello 하는 방법에 대 한 정보를 참조 하십시오. **hello 진단 데이터를 볼** 이 항목의 합니다.
   
    **서버 탐색기**에서 데이터 컬렉션을 변경하는 경우 클라우드 서비스를 완전히 다시 배포할 때까지 이 변경 내용이 계속 적용됩니다. 사용 하는 경우 hello 기본 게시 설정, hello 변경 덮어쓰여집니다, 그리고 do 전체적 보다는 tooupdate hello 기존 배포를 설정 하는 hello 기본 게시 때문입니다. 이동 toohello 배포 시 toomake 있는지 hello 설정의 선택을 취소 **고급 설정** hello 게시 마법사 및 지우기 hello 탭 **배포 업데이트** 확인란을 선택 합니다. 확인란의 선택을 취소 하 고 다시 배포 하면, hello 설정을 toothose hello.wadcfgx (또는.wadcfg) 파일에 hello 역할에 대 한 hello 속성 편집기를 통해 집합으로 되돌립니다. 배포를 업데이트 하는 경우 Azure hello 이전 설정을 유지 합니다.

## <a name="troubleshoot-azure-cloud-service-issues"></a>Azure 클라우드 서비스 문제 해결
발생 하는 경우, "사용 중" 상태에서 벗어나지 하는 역할과 같은 클라우드 서비스 프로젝트와 함께 문제가 반복적으로 재활용 되거나 내부 서버 오류를 throw, 도구와 기술을 toodiagnose를 사용 하 고 이러한 문제를 수정할 수 있습니다. 구체적인 예제는 일반적인 문제 및 솔루션, 뿐만 아니라 hello 개념 및 도구에 대해 간략하게 toodiagnose를 사용 하 고 이러한 오류를 수정, 참조 [Azure PaaS 계산 진단 데이터](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)합니다.

## <a name="q--a"></a>질문과 대답
**Hello 버퍼 크기 무엇 이며 어떻게 커야?**

할당량 각 가상 컴퓨터 인스턴스에서 진단 데이터의 양을 hello 로컬 파일 시스템에 저장할 수를 제한 합니다. 또한 사용할 수 있는 진단 데이터의 각 형식에 대해 버퍼 크기를 지정합니다. 이 버퍼 크기는 해당 형식의 데이터에 대해 개별 할당량과 같은 역할을 합니다. Hello 대화 상자 hello 아래를 확인 하면 알 수 전체 할당량 및 남아 있는 메모리 양을 hello hello 합니다. 도달 하 게 더 큰 버퍼 나 더 많은 데이터 형식을 지정 하면 전체 할당량을 hello 합니다. Hello를 변경할 수 있습니다 hello diagnostics.wadcfg/.wadcfgx 구성 파일을 수정 하 여 전체 할당량입니다. hello 진단 데이터에 저장 된 동일한 파일 시스템 응용 프로그램의 데이터를 hello hello을 늘리지 말아야 많은 디스크 공간을 사용 하 여 응용 프로그램 하므로 전체 진단 할당량입니다.

**Hello 전송 기간 이란 무엇 이며 어떻게 길어야?**

hello 전송 기간은 데이터 간의 간격이 경과 캡처하는 시간의 양을 hello입니다. 각 전송 기간 후에 저장소 계정에 가상 컴퓨터 tootables hello 로컬 파일 시스템에서 데이터 이동 됩니다. 전송 기간 hello 종료 하기 전에 hello 할당량을 초과 하는 수집 되는 데이터 양을 hello, 오래 된 데이터를 무시 합니다. 손실 될 데이터 hello 버퍼 크기를 초과 하거나 전체 할당량을 hello toodecrease hello 전송 기간을 할 수 있습니다.

**어떤 시간대가 사용의 타임 스탬프 hello?**

클라우드 서비스를 호스팅하는 hello 데이터 센터의 hello 현지 표준 시간대의 hello 타임 스탬프는 합니다. hello 다음 세 가지 타임 스탬프 열 hello 로그 테이블에 사용 됩니다.

* **PreciseTimeStamp** hello ETW 타임 스탬프 hello 이벤트입니다. 즉, hello 클라이언트로부터 hello 시간 hello 이벤트가 기록 됩니다.
* **타임 스탬프** 는 내림 한 PreciseTimeStamp toohello 업로드 빈도 경계입니다. 따라서 업로드 빈도가 5 분이 hello 이벤트 시간이 00시 17분: 12, 타임 스탬프 00시 15분: 00이 됩니다.
* **타임 스탬프** hello Azure 테이블에에서는 hello 엔터티를 만든 hello 타임 스탬프입니다.

**진단 정보를 수집할 때 비용은 어떻게 관리합니까?**

hello 기본 설정 (**로그 수준** 도**오류** 및 **전송 기간** 도**1 분**) 비용 디자인 된 toominimize 됩니다. 추가 진단 데이터 수집 또는 hello 전송 기간을 감소 하는 경우 계산 비용이 증가 합니다. 필요 없는 경우 toodisable 데이터 수집 유념 하십시오 필요한 것 보다 더 많은 데이터를 수집 하지 않는 합니다. 하면 항상 다시 사용할 수, 런타임에 hello 이전 섹션에 나와 있는 것 처럼 합니다.

**IIS에서 실패한 요청 로그를 수집하려면 어떻게 합니까?**

기본적으로 IIS는 실패한 요청 로그를 수집하지 않습니다. 웹 역할에 대 한 web.config 파일을 편집 하는 경우 hello IIS toocollect을 구성할 수 있습니다.

**OnStart 같은 RoleEntryPoint 메서드에서 추적 정보를 얻을 수 없습니다. 무엇이 문제입니까?**

RoleEntryPoint의 hello 메서드 WAIISHost.exe, 하지 IIS의 hello 컨텍스트에서 호출 됩니다. 따라서 hello web.config의 구성 정보가 해당 일반적으로 추적 기능을 사용 하지 않습니다. tooresolve이이 문제를.config 파일 tooyour 웹 역할 프로젝트를 추가 하 고 hello 파일 toomatch hello 출력 어셈블리 hello RoleEntryPoint 코드가 포함 된 이름을 지정 합니다. Hello 기본 웹 역할 프로젝트에 hello.config 파일의 hello 이름은 waiishost.exe.config가 됩니다 것입니다. 다음 줄 toothis 파일 hello를 추가 합니다.

```
<system.diagnostics>
  <trace>
      <listeners>
          <add name “AzureDiagnostics” type=”Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener”>
              <filter type=”” />
          </add>
      </listeners>
  </trace>
</system.diagnostics>
```

Hello에 이제 **속성** 창, 집합 hello **tooOutput 디렉터리 복사** 속성 너무**항상 복사**합니다.

## <a name="next-steps"></a>다음 단계
Azure에 로그인 하는 진단에 대 한 더 toolearn 참조 [Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 사용](cloud-services/cloud-services-dotnet-diagnostics.md) 및 [Azure 앱 서비스의 웹 앱에 대 한 진단 로깅 사용](app-service-web/web-sites-enable-diagnostic-log.md)합니다.


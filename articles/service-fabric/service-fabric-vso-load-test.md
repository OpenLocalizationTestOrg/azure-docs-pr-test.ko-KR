---
title: "Visual Studio Team Services를 사용 하 여 응용 프로그램을 테스트 하는 aaaLoad | Microsoft Docs"
description: "Toostress Visual Studio Team Services를 사용 하 여 Azure 서비스 패브릭 응용 프로그램을 테스트 하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: fc743585-0d1b-483f-981d-493f4552ac07
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 663cf8db5e8f0a4d0d7f27b585645d7f776392f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-test-your-application-by-using-visual-studio-team-services"></a>Visual Studio Team Services를 사용하여 응용 프로그램 부하 테스트
이 문서에서는 Microsoft Visual Studio 부하 테스트 기능 toostress toouse 응용 프로그램을 테스트 하는 방법을 보여 줍니다. Azure 서비스 패브릭 상태 저장 서비스 백 엔드 및 상태 비저장 서비스 웹 프런트 엔드가 사용됩니다. hello 여기에 예제 응용 프로그램은 비행기 위치 시뮬레이터. 사용자는 항공기 ID, 출발 시간 및 도착 위치를 제공합니다. hello 백 엔드 응용 프로그램의 처리 hello 요청 하 고 hello 프런트 엔드 hello 조건과 일치 하는 지도 hello 비행기에 표시 됩니다.

hello 다음 다이어그램에서는 보여줍니다 hello 서비스 패브릭 응용 프로그램을 테스트 해야 합니다.

![Hello 예제 비행기 위치 응용 프로그램의 다이어그램][0]

## <a name="prerequisites"></a>필수 조건
시작 하기 전에 toodo hello 다음이 필요 합니다.

* Visual Studio Team Services 계정을 가져옵니다. [Visual Studio Team Services](https://www.visualstudio.com)에서 무료로 계정을 등록할 수 있습니다.
* Visual Studio 2013 또는 Visual Studio 2015를 확보하여 설치합니다. 이 문서는 Visual Studio 2015 Enterprise Edition을 사용하지만 Visual Studio 2013 및 기타 버전도 유사하게 작동합니다.
* 스테이징 환경에 응용 프로그램 tooa를 배포 합니다. 참조 [toodeploy 응용 프로그램 tooa 원격 클러스터 Visual Studio를 사용 하는 방법을](service-fabric-publish-app-remote-cluster.md) 이 대 한 정보에 대 한 합니다.
* 응용 프로그램 사용 패턴을 이해합니다. 이 정보는 사용 되는 toosimulate hello 부하 패턴입니다.
* 부하 테스트에 대 한 hello 목표를 이해 합니다. 이 해석 하 고 hello 부하 테스트 결과 분석할 수 있습니다.

## <a name="create-and-run-hello-web-performance-and-load-test-project"></a>만들기 및 hello 웹 성능 및 부하 테스트 프로젝트를 실행 합니다.
### <a name="create-a-web-performance-and-load-test-project"></a>웹 성능 및 부하 테스트 만들기
1. Visual Studio 2015를 엽니다. 선택 **파일** > **새로** > **프로젝트** hello 메뉴 모음 tooopen hello에 **새 프로젝트** 대화 상자.
2. Hello 확장 **Visual C#** 노드 선택 **테스트** > **웹 성능 및 부하 테스트 프로젝트**합니다. Hello 프로젝트 이름을 지정 하 고 hello를 눌러 **확인** 단추입니다.

    ![Hello 새 프로젝트 대화 상자 스크린 샷][1]

    솔루션 탐색기에서 새로운 웹 성능 및 부하 테스트 프로젝트가 표시됩니다.

    ![Hello 새 프로젝트를 나타내는 솔루션 탐색기의 스크린 샷][2]

### <a name="record-a-web-performance-test"></a>웹 성능 테스트 기록
1. 열기 hello.webtest 프로젝트입니다.
2. Hello 선택 **기록 추가** 아이콘 toostart 브라우저에서 세션 기록 합니다.

    ![브라우저에서 hello 기록 추가 아이콘의 스크린 샷][3]

    ![브라우저에서 hello 레코드 단추 스크린 샷][4]
3. Toohello 서비스 패브릭 응용 프로그램을 찾습니다. hello 기록 패널을 hello 웹 요청을 보여 줍니다.

    ![패널을 기록 하는 hello에서 웹 요청의 스크린 샷][5]
4. 일련의 hello 사용자 tooperform 예상 하는 작업을 수행 합니다. 이러한 작업은 패턴 toogenerate hello 부하로 사용 됩니다.
5. 완료 되 면 선택 hello **중지** 단추 toostop 기록 합니다.

    ![Hello 중지 단추 스크린 샷][6]

    Visual Studio에서 hello.webtest 프로젝트는 일련의 요청을 캡처해야 해야 합니다. 동적 매개 변수가 자동으로 대체됩니다. 이 때, 테스트 시나리오에 속하지 않는 중복된 종속 요청 또는 여분의 요청을 제거할 수 있습니다.
6. Hello 프로젝트를 저장 하 고 hello를 눌러 **테스트 실행** 명령 toorun hello 웹 성능 테스트를 로컬로 및 모든 것이 올바르게 작동 하는지 확인 합니다.

    ![테스트 실행 명령 hello 스크린 샷][7]

### <a name="parameterize-hello-web-performance-test"></a>Hello 웹 성능 테스트를 매개 변수화
Tooa 코딩 된 웹 성능 테스트를 변환 하 고 다음 hello 코드를 편집 하 여 hello 웹 성능 테스트 매개 변수화 할 수 있습니다. 대신 hello 테스트 반복 hello 데이터 있도록 hello 웹 성능 테스트 tooa 데이터 목록에 바인딩할 수 있습니다. 참조 [생성 및 코딩 된 웹 성능 테스트를 실행](https://msdn.microsoft.com/library/ms182552.aspx) tooconvert hello 웹 성능 테스트 tooa 테스트를 코딩 하는 방법에 대 한 세부 정보에 대 한 합니다. 참조 [데이터 소스 tooa 웹 성능 테스트 추가](https://msdn.microsoft.com/library/ms243142.aspx) toobind 데이터 tooa 웹 성능 방법에 대 한 정보에 대 한 테스트 합니다.

예를 들어 hello 비행기 ID 생성 된 GUID로 바꿉니다 하 고 더 많은 요청 toosend 내리지 않는 항공편 toodifferent 위치를 추가할 수 있도록 hello 웹 성능 테스트 tooa 코딩 된 테스트를 변환 합니다.

### <a name="create-a-load-test-project"></a>부하 테스트 프로젝트 만들기
부하 테스트 프로젝트는 hello 웹 성능 테스트 및 단위 테스트를 추가로 지정 된 부하 테스트 설정에서 설명 하는 하나 이상의 시나리오가 구성 됩니다. 단계를 수행 하는 hello toocreate 부하 프로젝트를 테스트 하는 방법을 보여 줍니다.

1. Hello 웹 성능 및 부하 테스트 프로젝트의 바로 가기 메뉴에서 선택 **추가** > **부하 테스트**합니다. Hello에 **부하 테스트** 마법사 hello 선택 **다음** tooconfigure hello 테스트 설정 단추입니다.
2. Hello에 **부하 패턴** 섹션에서 원하는 상수 사용자 부하 또는 적은 수의 사용자로 시작 하는 단계 부하 및 증가 시간에 따라 사용자가 hello 여부를 선택 합니다.

    좋은 예측 하는 사용자 부하의 양은 hello toosee hello 현재 시스템 수행 하는 방법을 사용할 경우 수도 **상수 로드**합니다. 여기서의 목표 toolearn hello 시스템 다양 한 로드 상태에서 일관성 있게 수행 하는지 여부를 선택 **단계 부하**합니다.
3. Hello에 **테스트 조합** 섹션에서 hello **추가** tooinclude hello 부하 테스트에 원하는 단추를 선택한 후 hello 테스트 합니다. Hello를 사용할 수 있습니다 **배포** 각 테스트에 대해 실행 되는 총 테스트 백분율로 toospecify hello 열입니다.
4. Hello에 **실행 설정** 섹션 hello 부하 테스트 지속 시간을 지정 합니다.

   > [!NOTE]
   > hello **테스트 반복** 옵션은 Visual Studio를 사용 하 여 로컬로 부하 테스트를 실행할 때에 사용할 수 있습니다.
   >
   >
5. Hello에 **위치** 섹션 **실행 설정**, 부하 테스트 요청이 생성 되는 hello 위치를 지정 합니다. hello 마법사 tooyour Team Services 계정에에서 toolog을 경우도 있습니다. 로그인한 다음 지리적 위치를 선택합니다. 완료 되 면 선택 hello **마침** 단추입니다.
6. Hello 부하 테스트를 만든 후 hello.loadtest 프로젝트를 열고 hello 같은 현재 실행 설정 선택 **실행 설정** > **설정 1 실행 [Active]**합니다. Hello에서 실행 하는 hello 설정을 열립니다 **속성** 창.
7. Hello에 **결과** hello 섹션 **실행 설정** 속성 창, hello **타이밍 정보 저장소** 설정이 있어야 **None** 으로 기본값입니다. 이 값도 변경**모든 개인 정보** tooget hello 부하 테스트 결과에 대 한 자세한 내용은 합니다. 참조 [부하 테스트](https://www.visualstudio.com/load-testing.aspx) tooconnect tooVisual Studio Team Services 및 실행 부하를 테스트 하는 방법에 대 한 자세한 내용은 합니다.

### <a name="run-hello-load-test-by-using-visual-studio-team-services"></a>Visual Studio Team Services를 사용 하 여 hello 부하 테스트 실행
Hello 선택 **부하 테스트 실행** 명령 toostart hello 테스트를 실행 합니다.

![부하 테스트 실행 명령 hello 스크린 샷][8]

## <a name="view-and-analyze-hello-load-test-results"></a>Hello 부하 테스트 결과 확인 및 분석
부하 테스트 진행 됨에 따라 hello로, hello 성능 정보를 그래프로 표현 합니다. 다음 그래프는 다음과 유사한 toohello를 표시 되어야 합니다.

![부하 테스트 결과에 대한 성능 그래프의 스크린샷][9]

1. Hello 선택 **보고서 다운로드** hello 페이지의 hello 위쪽에 링크 합니다. Hello 보고서를 다운로드 한 후 선택 hello **보고서를 볼** 단추입니다.

    Hello에 **그래프** 탭 다양 한 성능 카운터에 대 한 그래프를 확인할 수 있습니다. Hello에 **요약** 탭 hello 전체 테스트 결과가 표시 됩니다. hello **테이블** 탭 hello 성공한 요청과 실패 한 부하 테스트의 총 수를 표시 합니다.
2. Hello에 대 한 hello 숫자 링크 선택 **테스트** > **실패** 및 hello **오류** > **Count** 열 toosee 오류 세부 정보입니다.

    hello **세부** 탭 실패 한 요청에 대 한 가상 사용자 및 테스트 시나리오 정보를 표시 합니다. 이 데이터는 hello 부하 테스트에 여러 시나리오에 포함 된 경우에 유용할 수 있습니다.

참조 [부하 테스트 결과 분석 hello hello 부하 테스트 분석기의 그래프 보기에서에서](https://www.visualstudio.com/load-testing.aspx) 부하 보기에 대 한 자세한 내용은 테스트 결과입니다.

## <a name="automate-your-load-test"></a>부하 테스트 자동화
Visual Studio Team Services 부하 테스트 Api toohelp 부하 테스트를 관리 하는 Team Services 계정에는 결과 분석을 제공 합니다. 자세한 내용은 [클라우드 부하 테스트 REST API(영문)](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) 를 참조하세요.

## <a name="next-steps"></a>다음 단계
* [로컬 컴퓨터 개발 설정에서의 모니터링 및 진단 서비스](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[0]: ./media/service-fabric-vso-load-test/OverviewDiagram.png
[1]: ./media/service-fabric-vso-load-test/NewProjectDialog.png
[2]: ./media/service-fabric-vso-load-test/Project.png
[3]: ./media/service-fabric-vso-load-test/AddRecording.png
[4]: ./media/service-fabric-vso-load-test/AddRecording2.png
[5]: ./media/service-fabric-vso-load-test/ActionSequence.png
[6]: ./media/service-fabric-vso-load-test/StopRecording.png
[7]: ./media/service-fabric-vso-load-test/RunTest.png
[8]: ./media/service-fabric-vso-load-test/RunTest2.png
[9]: ./media/service-fabric-vso-load-test/Graph.png

---
title: "클라우드 서비스의 aaaTesting hello 성능을 | Microsoft Docs"
description: "Hello Visual Studio 프로파일러를 사용 하 여 클라우드 서비스의 hello 성능을 테스트 합니다."
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7a5501aa-f92c-457c-af9b-92ea50914e24
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 98bd775e6ffcf948e737c5ec26399c81f4770fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service"></a>클라우드 서비스의 hello 성능 테스트
## <a name="overview"></a>개요
다음 방법으로 hello에 클라우드 서비스의 hello 성능을 테스트할 수 있습니다.

* 요청 및 연결 및 hello 서비스 고객 관점에서 수행 하는 방법을 보여 주는 tooreview 사이트 통계에 대 한 Azure 진단 toocollect 정보를 사용 합니다. 시작, tooget 참조 [Azure 클라우드 서비스 및 가상 컴퓨터에 대 한 진단 구성](http://go.microsoft.com/fwlink/p/?LinkId=623009)합니다.
* Visual Studio 프로파일러 tooget hello hello 서비스가 실행 되는 어떻게 계산 측면을 자세히 분석할 hello를 사용 합니다. 이 항목에 설명 된 대로 Azure에서 실행 되는 서비스 hello 프로파일러 toomeasure 성능을 사용할 수 있습니다. 서비스로 toouse hello 프로파일러 toomeasure 성능 로컬 계산 에뮬레이터에서 실행 방법에 대 한 정보를 참조 하십시오. [테스트 hello는 Azure 클라우드 서비스에서에서 로컬로의 hello 계산 에뮬레이터를 사용 하 여 hello Visual Studio 프로파일러 성능 ](http://go.microsoft.com/fwlink/p/?LinkId=262845).

## <a name="choosing-a-performance-testing-method"></a>성능 테스트 방법 선택
### <a name="use-azure-diagnostics-toocollect"></a>Azure 진단 toocollect를 사용 합니다.
* 웹 페이지 또는 요청 및 연결 등의 서비스에 대한 통계.
* 역할이 재시작되는 빈도 등의 역할에 대한 통계.
* 전체 메모리 사용량, 가비지 수집기는 hello 또는 메모리를 환영 시간 비율로 hello에 대 한 정보는 실행 중인 역할의 집합입니다.

### <a name="use-hello-visual-studio-profiler-to"></a>Hello Visual Studio 프로파일러를 사용 합니다.
* 어떤 함수는 hello 대부분의 시간을 결정 합니다.
* 계산이 많은 프로그램의 각 부분에는 얼마나 많은 시간이 걸리는지 측정합니다.
* 서비스의 두 버전에 대한 자세한 성능 보고서를 비교합니다.
* 메모리 할당을 개별 메모리 할당 hello 수준 보다 더 자세한 정보에서를 분석 합니다.
* 다중스레드 코드에서 동시성 문제를 분석합니다.

Hello 프로파일러를 사용 하는 경우에 로컬로 또는 Azure에서 클라우드 서비스에서 실행 될 때 데이터를 수집할 수 있습니다.

### <a name="collect-profiling-data-locally-to"></a>로컬로 프로파일링 데이터를 수집합니다.
* 현실적인 시뮬레이션 된 부하를 필요 하지 않은 특정 작업자 역할의 hello 실행 같은 클라우드 서비스의 일부 hello 성능을 테스트 합니다.
* 격리 수준 제어 상태에서 클라우드 서비스의 hello 성능을 테스트 합니다.
* 하기 전에 클라우드 서비스의 hello 성능 테스트 tooAzure 배포 합니다.
* Hello 기존 배포를 방해 하지 않고 클라우드 서비스의 hello 성능을 개인적으로 테스트 합니다.
* Azure에서 실행 하는 데 드는 비용 없이 hello 서비스의 hello 성능을 테스트 합니다.

### <a name="collect-profiling-data-in-azure-to"></a>Azure에서 프로파일링 데이터를 수집하여 다음을 수행합니다.
* 시뮬레이션 된 부 하나 실제 부하에서 클라우드 서비스의 hello 성능을 테스트 합니다.
* 이 항목 뒷부분에 설명 된 대로 프로 파일링 데이터를 수집 하는 hello 계측 방법을 사용 합니다.
* Hello hello 서비스의 hello 성능을 테스트 서비스 hello 프로덕션 환경에서 실행 하는 경우 동일한 환경입니다.

일반적으로 일반 부하 tootest 클라우드 서비스를 시뮬레이션 스트레스 조건 또는 합니다.

## <a name="profiling-a-cloud-service-in-azure"></a>Azure에서 클라우드 서비스 프로파일링
Visual Studio에서 클라우드 서비스를 게시할 때 hello 서비스를 프로 파일링 하 고 hello 프로 파일링 정보를 hello을 제공 하는 설정 지정 수 있습니다. 역할의 각 인스턴스에 대한 프로파일링 세션이 시작됩니다. Toopublish Visual Studio에서 서비스를 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 내용은 [tooan Visual Studio에서 Azure 클라우드 서비스 게시](https://msdn.microsoft.com/library/azure/ee460772.aspx)합니다.

Visual Studio에서 성능 프로 파일링에 대해 자세히 toounderstand 참조 [초보자 가이드 tooPerformance 프로 파일링](https://msdn.microsoft.com/library/azure/ms182372.aspx) 및 [프로 파일링 도구를 사용 하 여 응용 프로그램 성능 분석](https://msdn.microsoft.com/library/azure/z9z62c29.aspx)합니다.

> [!NOTE]
> 응용 프로그램을 게시할 때 IntelliTrace 또는 프로파일링을 사용할 수 있습니다. 둘 다 사용할 수는 없습니다.
> 
> 

### <a name="profiler-collection-methods"></a>프로파일러 컬렉션 방법
프로파일링을 위해 성능 문제에 따라 여러 수집 방법을 사용할 수 있습니다.

* **CPU 샘플링** - 이 방법은 CPU 이용률 문제의 초기 분석에 유용한 응용 프로그램 통계를 수집합니다. CPU 샘플링은 대부분의 성능 조사를 시작 하기 위한 권장 되는 방법을 hello 됩니다. CPU 샘플링 데이터를 수집할 때 프로 파일링 하는 hello 응용 프로그램에 많은 영향을 미치지 않습니다.
* **계측** - 이 방법은 집중된 분석 및 입/출력 성능 문제 분석에 유용한 자세한 타이밍 데이터를 수집합니다. hello 계측 메서드는 프로 파일링 실행 중 모듈의 각 항목, 종료 및 함수 호출의 hello 함수를 기록 합니다. 이 메서드는 코드의 섹션에 대 한 자세한 타이밍 정보를 수집 하 고 입력 및 출력 작업이 응용 프로그램 성능에 미치는 hello 영향을 이해 하는 데 유용 합니다. 이 방법은 32비트 운영 체제를 실행하는 컴퓨터에 사용되지 않습니다. 실행할 때만 hello 클라우드 서비스, 로컬이 아닌 hello 계산 에뮬레이터에서 Azure이이 옵션은 사용할 수 있습니다.
* **.NET 메모리 할당** -이 방법은 hello 샘플링 프로 파일링 방법을 사용 하 여.NET Framework 메모리 할당 데이터를 수집 합니다. hello 수집 된 데이터에 포함 되어 hello 수와 할당 된 개체의 크기입니다.
* **동시성** - 이 방법은 리소스 경합 데이터와 프로세스 및 멀티스레드와 멀티 프로세스 응용 프로그램 분석에 유용한 스레드 실행 데이터를 수집합니다. hello 동시성 방법에 대 한 스레드가 대기 하는 경우 같은 코드의 실행을 차단 해제 하는 액세스 tooan 응용 프로그램 리소스 toobe 잠긴 각 이벤트에 대 한 데이터를 수집 합니다. 이 방법은 멀티스레드 응용 프로그램을 분석하는데 유용합니다.
* 또한 사용할 수 있습니다 **계층 상호 작용 프로 파일링**, 동기 ADO.NET의 hello 실행 시간에 대 한 추가 정보를 제공 하는 하나 이상의와 통신 하는 다중 계층 응용 프로그램의 함수에서 호출 데이터베이스입니다. 프로 파일링 방법 hello를 사용 하 여 계층 상호 작용 데이터를 수집할 수 있습니다. 계층 상호작용 프로파일링에 대한 자세한 내용은 [계층 상호작용 보기](https://msdn.microsoft.com/library/azure/dd557764.aspx)를 참조하십시오.

## <a name="configuring-profiling-settings"></a>프로파일링 설정 구성
그림 에서처럼 방법을 다음 hello tooconfigure hello Azure 응용 프로그램 게시 대화 상자에서 프로 파일링 설정을 합니다.

![프로파일링 설정 구성](./media/vs-azure-tools-performance-profiling-cloud-services/IC526984.png)

> [!NOTE]
> tooenable hello **프로 파일링 사용** 확인란 hello 프로파일러를 사용 하 고 있는지 toopublish 클라우드 서비스는 hello 로컬 컴퓨터에 설치 되어 있어야 합니다. 기본적으로 hello 프로파일러는 Visual Studio를 설치할 때 설치 됩니다.
> 
> 

### <a name="tooconfigure-profiling-settings"></a>tooconfigure 프로 파일링 설정
1. 솔루션 탐색기에서 Azure 프로젝트에 대 한 hello 바로 가기 메뉴를 열고 선택한 후 **게시**합니다. 방법에 대 한 자세한 단계 toopublish 클라우드 서비스 참조 [클라우드에 게시 Azure tools hello 사용 하 여 서비스](http://go.microsoft.com/fwlink/p?LinkId=623012)합니다.
2. Hello에 **Azure 응용 프로그램 게시** 대화 상자에서 선택한 hello **고급 설정** 탭 합니다.
3. 프로 파일링, tooenable 선택 hello **프로 파일링 사용** 확인란 합니다.
4. tooconfigure 프로 파일링 설정을 선택할 hello **설정을** 하이퍼링크입니다. hello 프로 파일링 설정 대화 상자가 나타납니다.
5. Hello에서 **프로 파일링 방법 시겠습니까 toouse** 옵션 단추를 해야 하는 프로 파일링 hello 유형을 선택 합니다.
6. toocollect hello 계층 상호 작용 프로 파일링 데이터를 선택 하는 hello **계층 상호 작용 프로 파일링 사용** 확인란 합니다.
7. toosave hello 설정을 선택 hello **확인** 단추입니다.
   
    이 응용 프로그램을 게시할 때이 설정을 사용 하는 toocreate hello 각 역할에 대 한 세션 프로 파일링 합니다.

## <a name="viewing-profiling-reports"></a>프로파일링 보고서 보기
프로파일링 세션은 클라우드 서비스에서 역할의 각 인스턴스에 대해 생성됩니다. Visual Studio에서 각 세션의 tooview 보고 프로 파일링, hello 서버 탐색기 창을 표시 하 고는 역할 인스턴스가 Azure 계산 노드 tooselect hello를 선택 합니다. 그런 다음 hello hello 다음 그림에에서 나와 있는 것 처럼 프로 파일링 보고서를 볼 수 있습니다.

![Azure에서 프로파일링 보고서 보기](./media/vs-azure-tools-performance-profiling-cloud-services/IC748914.png)

### <a name="tooview-profiling-reports"></a>tooview 프로 파일링 보고서
1. hello 메뉴 모음 보기를 선택, 서버 탐색기에 hello 서버 탐색기 창에서 Visual Studio tooview입니다.
2. Hello Azure 계산 노드를 선택한 다음 Visual Studio에서 게시할 때 tooprofile 선택한 hello 클라우드 서비스에 대 한 hello Azure 배포 노드를 선택 합니다.
3. hello 서비스에서 특정 인스턴스에 대 한 바로 가기 메뉴를 열고 hello hello 역할을 선택 하 고 선택 된 인스턴스에 대 한 보고 tooview 프로 파일링 **프로 파일링 보고서 보기**합니다.
   
    hello 보고서에서.vsp 파일은 이제 Azure에서 다운로드 하 고 hello 다운로드의 hello 상태 hello Azure 활동 로그에에서 나타납니다. Hello 다운로드가 완료 되 면 프로 파일링 보고서 hello 라는 Visual Studio에 대 한 hello 편집기의 탭에 나타납니다 <Role name>  *<Instance Number>*  <identifier>.vsp 합니다. Hello 보고서에 대 한 요약 데이터가 표시 됩니다.
4. hello 현재 보기 목록에서 hello 보고서의 서로 다른 뷰 toodisplay hello 유형의 보기를 선택 합니다. 자세한 내용은 [프로파일링 도구 보고서 보기](https://msdn.microsoft.com/library/azure/bb385755.aspx)를 참조하세요.

## <a name="next-steps"></a>다음 단계
[클라우드 서비스 디버깅](https://msdn.microsoft.com/library/azure/ee405479.aspx)

[게시 tooan Visual Studio에서 Azure 클라우드 서비스](https://msdn.microsoft.com/library/azure/ee460772.aspx)


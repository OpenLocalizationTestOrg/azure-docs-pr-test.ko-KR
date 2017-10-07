---
title: "클라우드 서비스를 로컬로 hello 계산 에뮬레이터에서에서 aaaProfiling | Microsoft Docs"
services: cloud-services
description: "Visual Studio 프로파일러 hello로 클라우드 서비스의 성능 문제를 검토 합니다."
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
tags: 
ms.assetid: 25e40bf3-eea0-4b0b-9f4a-91ffe797f6c3
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: fc37c85dad4db4cc0310f73afad56fc0fe5f3963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a>Hello Azure 계산 에뮬레이터를 사용 하 여 hello Visual Studio 프로파일러에에서 hello 로컬로 클라우드 서비스의 성능 테스트
다양 한 도구와 기술을 클라우드 서비스의 hello 성능 테스트에 사용할 수 있습니다.
클라우드 서비스 tooAzure를 게시 하는 경우에 Visual Studio 프로 파일링 데이터 수집 및 분석 하는 것을 유지할 수 있습니다에 설명 된 대로 로컬 [Azure 응용 프로그램 프로 파일링][1]합니다.
에 설명 된 대로 진단 tootrack 다양 한 성능 카운터를 사용할 수도 있습니다 [성능 카운터를 사용 하 여 Azure에서][2]합니다.
도 toohello 클라우드 배포 하기 전에 hello 계산 에뮬레이터에서 로컬로 응용 프로그램 tooprofile를 지정할 수 있습니다.

이 문서 hello 에뮬레이터에서 로컬로 수행할 수 있는 프로 파일링의 hello CPU 샘플링 방법에 설명 합니다. CPU 샘플링은 주입식이 아닌 프로파일링 방법입니다. 지정 된 샘플링 간격 hello 프로파일러는 hello 호출 스택의 스냅숏을 만듭니다. hello 데이터는 시간 기간 동안 수집 되 고 보고서에 표시 된 것입니다. 이 프로 파일링이 방법을 계산이 많이 필요한 응용 프로그램에서 대부분의 hello CPU 작업이 수행 되는 위치 tooindicate를 경향이 있습니다.  여기서 응용 프로그램은 시간을 소비 hello 대부분 hello "실행 부하 과다 경로"에 기회 toofocus hello 이렇게 하면 됩니다.

## <a name="1-configure-visual-studio-for-profiling"></a>1: 프로파일링을 위해 Visual Studio 구성
먼저 프로파일링 시 유용할 수 있는 몇 가지 Visual Studio 구성 옵션이 있습니다. toomake 의미 hello 프로 파일링 보고서를 응용 프로그램과 시스템 라이브러리에 대 한 기호에 대 한 기호 (.pdb 파일) 필요 합니다. Toomake 있는지 hello 사용할 수 있는 기호 서버를 참조 합니다. toodo hello에이 **도구** Visual Studio에서 메뉴 선택 **옵션**를 눌러 **디버깅**, 다음 **기호**합니다. Microsoft 기호 서버가 **기호 파일(.pdb) 위치**아래에 표시되는지 확인합니다.  추가 기호 파일이 있는 http://referencesource.microsoft.com/symbols를 참조할 수도 있습니다.

![기호 옵션][4]

원하는 경우 단순화할 수 있습니다 hello 보고 내 코드만 옵션을 설정 하 여 해당 hello 프로파일러를 생성 합니다. 내 코드만 사용 함수 호출 스택은 완전히 내부 toolibraries를 호출 하 고.NET Framework hello hello 보고서에서 숨겨진 간소화 됩니다. Hello에 **도구** 메뉴 선택 **옵션**합니다. 다음 hello 확장 **성능 도구** 노드를 선택 하 고 **일반**합니다. 에 대 한 hello 확인란 선택 **내 코드만 사용 프로파일러 보고서에 대 한**합니다.

![내 코드 옵션만][17]

기존 프로젝트나 새 프로젝트에 이러한 지침을 사용할 수 있습니다.  새 프로젝트 tootry hello 아래에 설명 된 기술을 만드는 경우 선택 하는 C# **Azure 클라우드 서비스** 프로젝트를 선택 하 고는 **웹 역할** 및 **작업자 역할**합니다.

![Azure 클라우드 서비스 프로젝트 역할][5]

예를 들어에서는 시간이 많이 걸리고 몇 가지 확실 한 성능 문제를 보여 줍니다.는 몇 가지 코드 tooyour 프로젝트를 추가 합니다. 예를 들어 다음 코드 tooa 작업자 역할 프로젝트 hello를 추가 합니다.

    public class Concatenator
    {
        public static string Concatenate(int number)
        {
            int count;
            string s = "";
            for (count = 0; count < number; count++)
            {
                s += "\n" + count.ToString();
            }
            return s;
        }
    }

Hello hello 작업자 역할의 RoleEntryPoint 파생 클래스에서 RunAsync 메서드에서에서이 코드를 호출 합니다. (동기적으로 실행 하는 hello 방법에 대 한 hello 경고를 무시 합니다.)

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

빌드 및 클라우드 서비스를 로컬로 실행할 (Ctrl + F5)을 디버깅 하지 않고 된 hello 솔루션 구성도**릴리스**합니다. 이렇게 하면 hello 응용 프로그램을 로컬로 실행에 대해 생성 된 모든 파일 및 폴더 및 모든 hello 에뮬레이터 시작 되었는지 확인 합니다. 작업자 역할을 실행 하는 hello 작업 표시줄 tooverify에서 hello 계산 에뮬레이터 UI를 시작 합니다.

## <a name="2-attach-tooa-process"></a>2: tooa 프로세스 연결
Visual Studio 2010 IDE hello에서 시작 하 여 hello 응용 프로그램을 프로 파일링, 대신 프로세스를 실행 하는 hello 프로파일러 tooa를 연결 해야 합니다. 

hello에 tooattach hello 프로파일러 tooa 프로세스 **분석** 메뉴 선택 **프로파일러** 및 **연결/분리**합니다.

![프로필 연결 옵션][6]

작업자 역할에 대 한 hello WaWorkerHost.exe 프로세스를 찾습니다.

![WaWorkerHost 프로세스][7]

프로젝트 폴더는 네트워크 드라이브에 있으면 hello 프로파일러가 묻습니다 tooprovide 프로 파일링 보고서는 다른 위치 toosave hello 합니다.

 TooWaIISHost.exe 연결 하 여 tooa 웹 역할에 추가할 수 있습니다.
Toouse hello processID toodistinguish 필요한 응용 프로그램에 여러 작업자 역할 프로세스가 있는 경우 해당 합니다. Hello 프로세스 개체에 액세스 하 여 hello 나타나지 않지만 processID를 프로그래밍 방식으로 쿼리할 수 있습니다. 예를 들어 hello RoleEntryPoint 파생 클래스의 코드 toohello Run 메서드가이 역할에 추가 하면 수 확인 하면 로그 hello 계산 에뮬레이터 UI tooknow에 어떤 프로세스 tooconnect 합니다.

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

계산 에뮬레이터 UI 시작 hello tooview hello 로그입니다.

![Hello 계산 에뮬레이터 UI를 시작 합니다.][8]

Hello 콘솔 창의 제목 표시줄을 클릭 하 여 hello 계산 에뮬레이터 UI에서에서 hello 작업자 역할 로그 콘솔 창을 엽니다. Hello 로그에 hello 프로세스 ID를 볼 수 있습니다.

![프로세스 ID 보기][9]

응용 프로그램의 UI (필요한 경우) tooreproduce hello 시나리오에서 hello 단계를 수행 하는 하나, 첨부

Toostop 프로 파일링에 하려는 경우 선택 hello **프로 파일링 중지** 링크 합니다.

![프로파일링 중지 옵션][10]

## <a name="3-view-performance-reports"></a>3: 성능 보고서 보기
응용 프로그램에 대 한 hello 성능 보고서가 표시 됩니다.

이 시점에서 hello 프로파일러 실행이 중지 되는 vsp 파일에 데이터를 저장 및이 데이터의 분석을 보여 주는 보고서가 표시 됩니다.

![프로파일러 보고서][11]

String.wstrcpy hello에 표시 되 면 실행 부하 과다 경로 내 코드만 toochange hello 클릭 tooshow 사용자 코드에만 봅니다.  String.Concat 표시 되 면 hello 모든 코드 표시 단추를 누르면 해 보십시오.

Hello Concatenate 메서드와 hello 실행 시간의 많은 부분을 차지 String.Concat 표시 됩니다.

![보고서 분석][12]

이 문서의 hello 문자열 연결 코드를 추가한 경우이 대 한 hello 작업 목록에서에서 경고를 나타납니다. 이 가비지 컬렉션은 생성 되 고 삭제 하는 문자열의 toohello 수 때문에 과도 한 양의 하다는 경고가 나타날 수도 있습니다.

![성능 경고][14]

## <a name="4-make-changes-and-compare-performance"></a>4: 변경 및 성능 비교
또한 코드 변경 전후의 hello 성능을 비교할 수 있습니다.  프로세스를 실행 하는 hello를 중지 하 고 hello 코드 tooreplace hello 문자열 연결 작업 hello 사용과 StringBuilder의 편집:

    public static string Concatenate(int number)
    {
        int count;
        System.Text.StringBuilder builder = new System.Text.StringBuilder("");
        for (count = 0; count < number; count++)
        {
             builder.Append("\n" + count.ToString());
        }
        return builder.ToString();
    }

다른 성능 실행을 수행 하 고 hello 성능을 비교 합니다. 성능 탐색기 hello 경우 hello 실행은의 hello 동일한 세션 수만 두 보고서, hello 바로 가기 메뉴를 열고 선택한 선택 **성능 보고서 비교**합니다. 다른 성능 세션에서 실행 toocompare hello를 열고, **분석** 메뉴 선택 **성능 보고서 비교**합니다. 표시 되는 hello 대화 상자에서 두 파일을 지정 합니다.

![성능 보고서 비교 옵션][15]

hello 보고서 hello 두 실행 간의 차이 강조 표시합니다.

![비교 보고서][16]

축하합니다. Hello 프로파일러와 함께 시작 했으면 합니다.

## <a name="troubleshooting"></a>문제 해결
* 릴리스 빌드를 프로파일링하고 있는지 확인하고 디버깅 없이 시작합니다.
* Hello 연결/분리 옵션 hello 프로파일러 메뉴를 사용 하지 않는 경우 hello 성능 마법사를 실행 합니다.
* 응용 프로그램의 hello tooview hello 상태를 계산 에뮬레이터 UI를 사용 합니다. 
* Hello 에뮬레이터에서 응용 프로그램을 시작 하는 데 문제가 있으면 또는 프로파일러 hello를 연결 하는 경우에 hello 계산 에뮬레이터를 종료 하 고 다시 시작 합니다. Hello 문제가 해결 되지를 다시 부팅 합니다. 계산 에뮬레이터 toosuspend hello를 사용 하 여 실행 중인 배포를 제거 하는 경우이 문제가 발생할 수 있습니다.
* 특히 전역 설정 hello 명령을 명령줄에서 프로 파일링 하는 hello를 모두 사용한 경우에 VSPerfClrEnv /globaloff가 호출 된 및 VsPerfMon.exe 종료 된 있는지 확인 합니다.
* Hello 메시지를 샘플링 하는 경우 표시 되 면 "PRF0025: 데이터가 수집 된" hello toohas CPU 활동을 연결 프로세스를 확인 합니다. 계산 작업을 수행하지 않는 응용 프로그램은 샘플링 데이터를 생성하지 않을 수 있습니다.  해당 수행 된 모든 샘플링 전에 hello 프로세스를 종료할 수 이기도 합니다. 프로 파일링 하는 역할에 대 한 hello Run 메서드가 종료 되지 않는 toosee를 확인 합니다.

## <a name="next-steps"></a>다음 단계
Hello 에뮬레이터에서 Azure 이진 계측는 hello Visual Studio 프로파일러에 지원 되지 않지만 tootest 메모리 할당 하려는 경우 프로 파일링 옵션을 선택할 수 있습니다. 선택할 수도 있습니다 동시성 프로 파일링는 데 도움이 되는 응용 프로그램 계층 간에 상호 작용할 때 성능 문제를 추적 하는 데 도움이 되를 스레드 잠금을 경쟁 하는 시간을 낭비 하 있는지 여부를 결정 하거나 계층 상호 작용 프로 파일링 가장 자주 사이의 hello 데이터 계층 작업자 역할입니다.  응용 프로그램을 생성 하는 hello 데이터베이스 쿼리를 볼 수 있으며 데이터 tooimprove hello database 사용 하 여 프로 파일링 하는 hello를 사용 하 여 있습니다. 계층 상호 작용 프로 파일링 하는 방법에 대 한 내용은 hello 블로그 게시물을 참조 하십시오. [연습: Visual Studio Team System 2010에서 계층 상호 작용 프로파일러 hello를 사용 하 여][3]합니다.

[1]: http://msdn.microsoft.com/library/azure/hh369930.aspx
[2]: http://msdn.microsoft.com/library/azure/hh411542.aspx
[3]: http://blogs.msdn.com/b/habibh/archive/2009/06/30/walkthrough-using-the-tier-interaction-profiler-in-visual-studio-team-system-2010.aspx
[4]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally09.png
[5]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally10.png
[6]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally02.png
[7]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally05.png
[8]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally010.png
[9]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally07.png
[10]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally06.png
[11]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally03.png
[12]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally011.png
[14]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally04.png 
[15]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally013.png
[16]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally012.png
[17]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally08.png

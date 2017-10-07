---
title: "Azure 진단으로 클라우드 서비스 응용 프로그램에서 aaaTrace hello 흐름 | Microsoft Docs"
description: "추가 추적 메시지 tooan Azure 응용 프로그램 toohelp 디버깅, 성능 측정, 모니터링, 트래픽 분석 합니다."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: d2ed7b5997ae1d298115b4ce593bb5051a9a0c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a>Azure 진단으로 클라우드 서비스 응용 프로그램의 hello 흐름 추적
추적은 실행 되는 동안 있습니다 toomonitor hello 응용 프로그램의 실행에 대 한 방법입니다. Hello를 사용할 수 있습니다 [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), 및 [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) toorecord 정보 오류에 대 한 클래스 및 응용 프로그램 로그, 텍스트 파일 또는 향후 분석을 위해 다른 장치에서 실행 합니다. 추적에 대한 자세한 내용은 [응용 프로그램을 추적 및 계측](https://msdn.microsoft.com/library/zs6s4h68.aspx)을 참조하세요.

## <a name="use-trace-statements-and-trace-switches"></a>추적 문 및 추적 스위치 사용
Hello를 추가 하 여 클라우드 서비스 응용 프로그램에서 구현 추적 [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) 하므로 toohello 응용 프로그램 구성 및 tooSystem.Diagnostics.Trace 또는 System.Diagnostics.Debug에 호출 하 여 응용 프로그램 코드입니다. 사용 하 여 hello 구성 파일 *app.config* 작업자 역할과 hello에 대 한 *web.config* 웹 역할에 대 한 합니다. Visual Studio 템플릿을 사용 하 여 새 호스팅된 서비스를 만들 때 Azure 진단이 자동으로 toohello 프로젝트를 추가 및 hello DiagnosticMonitorTraceListener toohello 해당 구성 파일을 추가 하는 hello 역할에 추가 됩니다.

Trace 문 배치에 대 한 정보를 참조 하십시오. [하는 방법: Trace 문 추가 tooApplication 코드](https://msdn.microsoft.com/library/zd83saa2.aspx)합니다.

코드에 [추적 스위치](https://msdn.microsoft.com/library/3at424ac.aspx) 를 배치하여 추적의 발생 여부와 범위를 제어할 수 있습니다. 이렇게 하면 프로덕션 환경에서 응용 프로그램의 hello 상태를 모니터링할 수 있습니다. 여러 컴퓨터에서 실행하는 여러 구성 요소를 사용하는 비즈니스 응용 프로그램에서 특히 중요합니다. 자세한 내용은 [방법: 추적 스위치 구성](https://msdn.microsoft.com/library/t06xyy08.aspx)을 참조하세요.

## <a name="configure-hello-trace-listener-in-an-azure-application"></a>Azure 응용 프로그램에서 hello 추적 수신기를 구성 합니다.
추적, 디버그 및 TraceSource를 사용 해야 "수신자" toocollect 및 전송 되는 레코드 hello 메시지를 설정할 수 있습니다. 수신기는 추적 메시지를 수집, 저장 및 라우팅합니다. 직접 실행 hello 추적 출력 tooan 같은 적절 한 대상, 로그, 창 또는 텍스트 파일입니다. Azure 진단 hello를 사용 하 여 [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) 클래스입니다.

Hello 절차를 완료 하기 전에 hello Azure 진단 모니터를 초기화 해야 합니다. toodo이,이 참조 [Microsoft Azure에서 진단 사용](cloud-services-dotnet-diagnostics.md)합니다.

참고는 Visual Studio에서 제공 되는 hello 템플릿을 사용 하는 경우 hello 수신기의 hello 구성을 자동으로 추가 됩니다 드립니다.

### <a name="add-a-trace-listener"></a>추적 수신기 추가
1. 사용자 역할에 대 한 hello web.config 또는 app.config 파일을 엽니다.
2. 다음 코드 toohello 파일 hello를 추가 합니다. Hello 버전 특성 toouse hello 어셈블리의 버전 번호 hello 참조를 변경 합니다. hello 어셈블리 버전이 변경 되지 않습니다 반드시 각 Azure SDK 릴리스로 업데이트 tooit는 없는 경우.
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > 프로젝트 참조 toohello Microsoft.WindowsAzure.Diagnostics 어셈블리 지정 했는지 확인 합니다. 참조 된 Microsoft.WindowsAzure.Diagnostics 어셈블리를 toomatch hello 버전의 hello 위에 hello xml hello 버전 번호를 업데이트 합니다.
   > 
   > 
3. Hello 구성 파일을 저장 합니다.

수신기에 대한 자세한 내용은 [추적 수신기](https://msdn.microsoft.com/library/4y5y10s7.aspx)를 참조하세요.

Hello 단계 tooadd hello 수신기를 완료 한 후에 추적 문 tooyour 코드를 추가할 수 있습니다.

### <a name="tooadd-trace-statement-tooyour-code"></a>tooadd 추적 문 tooyour 코드
1. 응용 프로그램에 대한 소스 파일을 엽니다. 예를 들어 hello <RoleName>hello 작업자 역할 또는 웹 역할에 대 한.cs 파일입니다.
2. Hello 다음 추가 이미 추가 되지 않은 경우 문을 사용 하 여:
    ```
        using System.Diagnostics;
    ```
3. 응용 프로그램의 hello 상태에 대 한 toocapture 정보를 표시할 위치 추적 문을 추가 합니다. 다양 한 추적 문이 hello tooformat hello 출력 메서드를 사용할 수 있습니다. 자세한 내용은 참조 [하는 방법: Trace 문 추가 tooApplication 코드](https://msdn.microsoft.com/library/zd83saa2.aspx)합니다.
4. Hello 소스 파일을 저장 합니다.


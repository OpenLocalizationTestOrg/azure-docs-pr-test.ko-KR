---
title: "Azure 로그 분석을 사용 하 여 aaaTrack 변경 | Microsoft Docs"
description: "hello 로그 분석에 대 한 변경 내용 추적 솔루션을 사용 하면 소프트웨어 및 사용자 환경에서 발생 하는 Windows 서비스 변경 내용을 식별할 수 있습니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f8040d5d-3c89-4f0c-8520-751c00251cb7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2bb1938caad25101e167927200ac3ef495120fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="track-software-changes-in-your-environment-with-hello-change-tracking-solution"></a>Hello 변경 내용 추적 솔루션으로 환경에서 소프트웨어 변경 내용을 추적합니다

![변경 내용 추적 기호](./media/log-analytics-change-tracking/change-tracking-symbol.png)

이 문서를 사용 하면 사용 하 여 hello 로그 분석 tooeasily에서 변경 내용 추적 솔루션에는 사용자 환경에서의 변경 내용을 식별 합니다. hello 솔루션에는 변경 내용 tooWindows 및 Linux 소프트웨어, Windows 파일 및 레지스트리 키, Windows 서비스 및 Linux 데몬 추적합니다. 구성 변경 내용을 식별하면 운영 문제를 쉽게 특정할 수 있습니다.

설치 된 에이전트의 hello 솔루션 tooupdate hello 유형을 설치 하기. 변경 내용 tooinstalled 소프트웨어, Windows 서비스 및 Linux 데몬 모니터링 hello 서버에서 읽혀집니다. 그런 다음 hello 데이터 처리를 위해 hello 클라우드에서 toohello 로그 분석 서비스에 전송 됩니다. 논리는 수신 적용된 toohello 데이터 및 hello 클라우드 서비스는 hello 데이터를 기록 합니다. Hello 정보 변경 내용 추적 대시보드에 hello 사용 하 여 서버 인프라에서 수행한 hello 변경 내용을 쉽게 확인할 수 있습니다.

## <a name="installing-and-configuring-hello-solution"></a>설치 하 고 hello 솔루션 구성
다음 정보 tooinstall hello를 사용 하 고 hello 솔루션을 구성 합니다.

* 있어야는 [Windows](log-analytics-windows-agents.md), [Operations Manager](log-analytics-om-agents.md), 또는 [Linux](log-analytics-linux-agents.md) toomonitor 변경 하려는 각 컴퓨터에서 에이전트입니다.
* Hello에서 추가 변경 내용 추적 솔루션 tooyour OMS 작업 hello 영역 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ChangeTrackingOMS?tab=Overview)합니다. Hello 정보를 사용 하는 hello 솔루션에 추가할 수 있습니다 또는 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다. 추가 구성은 필요하지 않습니다.

### <a name="configure-linux-files-tootrack"></a>Linux 파일 tootrack 구성
Hello 단계 tooconfigure 파일 tootrack Linux 컴퓨터에서 다음을 사용 합니다.

1. Hello OMS 포털에서 클릭 **설정을** (hello 기어 기호).
2. Hello에 **설정** 페이지 **데이터**, 클릭 하 고 **Linux 파일 추적**합니다.
3. Linux 파일 변경 내용 추적을 tootrack 원하고 hello 클릭 hello 파일의 hello 파일 이름을 포함 하는 hello 전체 경로 입력 **추가** 기호입니다. 예: "/etc/*.conf"
4. **Save**를 클릭합니다.  

> [!NOTE]
> Linux 파일 추적에는 디렉터리 추적, 디렉터리 재귀 및 와일드 카드 추적과 같은 부가 기능이 포함됩니다.

### <a name="configure-windows-files-tootrack"></a>Windows 파일 tootrack 구성
Windows 컴퓨터에서 단계 tooconfigure 파일 tootrack 다음 hello를 사용 합니다.

1. Hello OMS 포털에서 클릭 **설정을** (hello 기어 기호).
2. Hello에 **설정** 페이지 **데이터**, 클릭 하 고 **Windows 파일 추적**합니다.
3. Windows 파일 변경 내용 추적, tootrack 원하고 hello 클릭 hello 파일의 hello 파일 이름을 포함 한 hello 전체 경로 입력 **추가** 기호입니다. 예: C:\Program Files (x86)\Internet Explorer\iexplore.exe or C:\Windows\System32\drivers\etc\hosts
4. **Save**를 클릭합니다.  
   ![Windows 파일 변경 내용 추적](./media/log-analytics-change-tracking/windows-file-change-tracking.png)

### <a name="configure-windows-registry-keys-tootrack"></a>Windows 레지스트리 키 tootrack 구성
Windows 컴퓨터에서 단계 tooconfigure 레지스트리 키 tootrack 다음 hello를 사용 합니다.

1. Hello OMS 포털에서 클릭 **설정을** (hello 기어 기호).
2. Hello에 **설정** 페이지 **데이터**, 클릭 하 고 **Windows 레지스트리 추적**합니다.
3. Windows 레지스트리 변경 내용 추적, 입력 tootrack 원하고 hello를 클릭 한 다음 전체 키 hello **추가** 기호입니다.
4. **Save**를 클릭합니다.  
   ![Windows 레지스트리 변경 내용 추적](./media/log-analytics-change-tracking/windows-registry-change-tracking.png)

### <a name="explanation-of-linux-file-collection-properties"></a>Linux 파일 컬렉션 속성 설명
1. **형식**
   * **File**(보고서 파일 메타데이터 - 크기, 수정 날짜, 해시 등)
   * **Directory**(보고서 디렉터리 메타데이터 - 크기, 수정 날짜 등)
2. **링크** (Linux 처리 symlink tooother 파일 또는 디렉터리에 참조 하는 데 사용)
   * **Ignore** (recurions toonot 중 무시 symlink hello 파일/디렉터리 참조를 포함 하는 데 사용)
   * **에 따라** (재귀 tooalso 하는 동안 다음 hello symlink hello 파일/디렉터리 참조를 포함 하는 데 사용)
   * **관리** (hello symlink 수행 및 alter 반환 내용의 hello 처리)

   > [!NOTE]   
   > 링크 옵션 "Manage" hello 권장 되지 않습니다. 파일 콘텐츠 검색은 지원되지 않습니다.

3. **Recurse** (폴더 수준 반복할지 및 hello 경로 문을 충족 하는 모든 파일을 추적)
4. **Sudo**(sudo 권한이 필요한 액세스 파일 또는 디렉터리 사용)

### <a name="limitations"></a>제한 사항
변경 내용 추적 솔루션 hello hello 다음 항목을 현재 지원 되지 않습니다.

* Windows 파일 추적을 위한 폴더(디렉터리)
* Windows 파일 추적을 위한 재귀
* Windows 파일 추적을 위한 와일드 카드
* 경로 변수
* 네트워크 파일 시스템
* File Content(파일 내용)

기타 제한 사항은 다음과 같습니다.

* hello **최대 파일 크기** 열 및 값은 hello 현재 구현에서 사용 되지 않습니다.
* Hello 30 분 수집 주기에서 2500 개 이상의 파일을 수집 하는 경우 솔루션 성능이 저하 될 수 있습니다.
* 네트워크 트래픽이 많을 때 변경 레코드 걸릴 수 있습니다 tooa를 최대 6 시간 toodisplay의 합니다.
* 컴퓨터를 종료 하는 동안 hello 구성 수정 하면 hello 컴퓨터에 속한 toohello 이전 구성 파일 변경 내용을 게시할 수 있습니다.

## <a name="change-tracking-data-collection-details"></a>변경 내용 추적 데이터 수집 정보
변경 내용 추적 소프트웨어 인벤토리 및 사용 하도록 설정한 hello 에이전트를 사용 하 여 Windows 서비스 메타 데이터를 수집 합니다.

hello 다음 표에서 데이터 수집 방법과 변경 내용 추적에 대 한 데이터 수집 방법에 대 한 기타 세부 정보입니다.

| 플랫폼 | 직접 에이전트 | Operations Manager 에이전트 | Linux 에이전트 | Azure 저장소 | Operations Manager 필요 여부 | 관리 그룹을 통해 전송되는 Operations Manager 에이전트 데이터 | 수집 빈도 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Windows 및 Linux | &#8226; | &#8226; | &#8226; |  |  | &#8226; | 5 분 hello 변경 유형에 따라 too50 분입니다. Hello 테이블에 대 한 자세한 내용은 다음을 참조 하십시오. |


hello 다음 표에 hello 유형의 변경에 대 한 데이터 수집 빈도 hello 있습니다.

| **change type** | **frequency** | **에이전트****가** **차이를 발견한 경우 전송하나요?** |
| --- | --- | --- |
| Windows 레지스트리 | 50분 | 아니요 |
| Windows 파일 | 30분 | 예. 24시간 동안 변경 사항이 없는 경우 스냅숏이 전송됩니다. |
| Linux 파일 | 15분 | 예. 24시간 동안 변경 사항이 없는 경우 스냅숏이 전송됩니다. |
| Windows 서비스 | 30분 | 예, 변경 내용이 발견되는 경우 30분마다 전송됩니다. 변경에 관계없이 24시간마다 스냅숏이 전송됩니다. 따라서 hello 스냅숏도 전송은 변경 내용이 없는 경우. |
| Linux 데몬 | 5분 | 예. 24시간 동안 변경 사항이 없는 경우 스냅숏이 전송됩니다. |
| Windows 소프트웨어 | 30분 | 예, 변경 내용이 발견되는 경우 30분마다 전송됩니다. 변경에 관계없이 24시간마다 스냅숏이 전송됩니다. 따라서 hello 스냅숏도 전송은 변경 내용이 없는 경우. |
| Linux 소프트웨어 | 5분 | 예. 24시간 동안 변경 사항이 없는 경우 스냅숏이 전송됩니다. |

### <a name="registry-key-change-tracking"></a>레지스트리 키 변경 내용 추적

로그 분석 Windows 레지스트리를 모니터링 하 고 hello 변경 내용 추적 솔루션을 사용 하 여 추적을 수행 합니다. hello tooregistry 키 변경 내용을 모니터링의 목적은 제 3 자 코드 및 맬웨어 활성화할 수 toopinpoint 확장성 지점입니다. hello 다음 hello 솔루션에서 추적 되는 각를 추적 및 표시 hello 기본 레지스트리 키를 나열 합니다.

- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Startup
    - 시작 시 실행되는 스크립트를 모니터링합니다.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Shutdown
    - 종료 시 실행되는 스크립트를 모니터링합니다.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run
    - Tootheir Windows 계정에에서 hello 사용자가 로그인 하기 전에 로드 되는 키를 모니터링 합니다. hello 키는 64 비트 컴퓨터에서 실행 중인 32 비트 프로그램에 사용 됩니다.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Active Setup\Installed Components
    - 모니터는 tooapplication 설정을 변경 합니다.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\ShellEx\ContextMenuHandlers
    - Windows 탐색기에 직접 연결되고 일반적으로 Explorer.exe를 사용하여 In Process에서 실행되는 일반적인 자동 시작 항목을 모니터링합니다.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\Shellex\CopyHookHandlers
    - Windows 탐색기에 직접 연결되고 일반적으로 Explorer.exe를 사용하여 In Process에서 실행되는 일반적인 자동 시작 항목을 모니터링합니다.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\Background\ShellEx\ContextMenuHandlers
    - Windows 탐색기에 직접 연결되고 일반적으로 Explorer.exe를 사용하여 In Process에서 실행되는 일반적인 자동 시작 항목을 모니터링합니다.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - 아이콘 오버레이 처리기 등록을 모니터링합니다.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - 64비트 컴퓨터에서 실행되는 32비트 프로그램에 대한 아이콘 오버레이 처리기 등록을 모니터링합니다.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects
    - Internet Explorer에 대한 새 브라우저 도우미 개체 플러그 인을 모니터링합니다. 사용 되는 tooaccess hello hello 현재 페이지와 toocontrol 탐색의 문서 개체 모델 (DOM).
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects
    - Internet Explorer에 대한 새 브라우저 도우미 개체 플러그 인을 모니터링합니다. 사용 되는 tooaccess hello hello 현재 페이지와 toocontrol 탐색의 64 비트 컴퓨터에서 실행 중인 32 비트 프로그램에 대 한 문서 개체 모델 (DOM).
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Internet Explorer\Extensions
    - 사용자 지정 도구 메뉴 및 사용자 지정 도구 모음 단추와 같은 새로운 Internet Explorer 확장을 모니터링합니다.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Internet Explorer\Extensions
    - 64비트 컴퓨터에서 실행되는 32비트 프로그램에 대해 사용자 지정 도구 메뉴 및 사용자 지정 도구 모음 단추와 같은 새로운 Internet Explorer 확장을 모니터링합니다.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    - Wavemapper, wave1 및 wave2, msacm.imaadpcm,.msadpcm,.msgsm610, 및 vidc 관련 된 hello 32 비트 드라이버를 모니터링 합니다. Hello 시스템의에서 비슷한 toohello [drivers] 섹션입니다. INI 파일입니다.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    - 모니터 hello 32 비트 드라이버 wavemapper, 및 관련 된 wave1 및 wave2, msacm.imaadpcm,.msadpcm,.msgsm610, 64 비트 컴퓨터에서 실행 중인 32 비트 프로그램에 대 한 vidc 합니다. Hello 시스템의에서 비슷한 toohello [drivers] 섹션입니다. INI 파일입니다.
- HKEY\_LOCAL\_MACHINE\System\CurrentControlSet\Control\Session Manager\KnownDlls
    - 모니터 hello 알려진 또는 자주 사용 되는 시스템 Dll;의 목록 이 시스템의 시스템 Dll 트로이 목마 버전에서을 삭제 하 여 약한 응용 프로그램 디렉터리 권한을 이용 하지 못하게 하면 됩니다.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify
    - 패키지 수 tooreceive 이벤트 알림 Winlogon, hello Windows 운영 체제에 대 한 hello 대화형 로그온 지원 모델에서에서의 모니터 hello 목록입니다.


## <a name="use-change-tracking"></a>변경 내용 추적 사용
Hello를 사용 하 여 hello 변경 내용 요약을 볼 모니터링 되는 서버에 대 한 수 hello 솔루션이 설치 된 후 **변경 내용 추적** hello 타일 **개요** OMS의 페이지입니다.

![변경 내용 추적 타일의 이미지](./media/log-analytics-change-tracking/change-tracking-tile.png)

변경 내용 tooyour 인프라 및 범주 다음 hello 드릴 인투 세부 사항을 볼 수 있습니다.

* 소프트웨어 및 Windows 서비스에 대한 구성 유형별 변경 내용
* 소프트웨어 변경 tooapplications 및 개별 서버용 업데이트
* 각 응용 프로그램에 대한 전체 소프트웨어 변경 내용 수
* Linux 패키지
* 개별 서버에 대한 Windows 서비스 변경 내용
* Linux 데몬 변경 내용

![변경 내용 추적 대시보드의 이미지](./media/log-analytics-change-tracking/change-tracking-dash01.png)

![변경 내용 추적 대시보드의 이미지](./media/log-analytics-change-tracking/change-tracking-dash02.png)

### <a name="tooview-changes-for-any-change-type"></a>tooview 변경 내용을 유형
1. Hello에 **개요** 페이지에서 hello **변경 내용 추적** 바둑판식으로 배열입니다.
2. Hello에 **변경 내용 추적** 대시보드를 hello hello 변경 유형 블레이드 중 하나의 요약 정보를 검토 한 다음 하나를 클릭 tooview hello에 대 한 정보를 자세히 **로그 검색** 페이지.
3. Hello 로그 검색 페이지에서 자세한 결과 시간과 로그 검색 기록을로 결과 볼 수 있습니다. 패싯 toonarrow hello 결과에서 필터링 할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* 사용 하 여 [로그 분석 검색 로그인](log-analytics-log-searches.md) tooview 변경 내용 추적 데이터를 자세히 설명 합니다.

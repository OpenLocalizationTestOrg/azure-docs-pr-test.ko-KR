---
title: "스냅숏 관리자 사용자 인터페이스 aaaStorSimple | Microsoft Docs"
description: "Hello StorSimple 스냅숏 관리자 사용자 인터페이스를 설명 하 고 설명 어떻게 toouse 것 toomanage 백업 작업 및 hello 카탈로그를 백업 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: c7d91892-2881-41a2-a7a2-908dc3646493
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.custom: 
ms.openlocfilehash: 865520fdaf1b559714b52b428ad136b084d65c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-user-interface-toomanage-backup-jobs-and-backup-catalog"></a>StorSimple 스냅숏 관리자를 사용 하 여 사용자 인터페이스 toomanage 백업 작업 및 백업 카탈로그

## <a name="overview"></a>개요
StorSimple 스냅숏 관리자 hello tootake를 사용 하 고 백업을 관리할 수 있는 직관적인 사용자 인터페이스를 있습니다. 이 자습서에서 소개 toohello 사용자 인터페이스를 제공 하 고 다음 설명 방법을 각 toouse hello 구성 요소입니다. 에 대 한 자세한 설명은 hello StorSimple 스냅숏 관리자를 참조 하세요. [StorSimple 스냅숏 관리자 란?](storsimple-what-is-snapshot-manager.md)

### <a name="console-description"></a>콘솔 설명
tooview hello 사용자 인터페이스를 바탕 화면에 hello StorSimple 스냅숏 관리자 아이콘을 클릭 합니다. hello 다음 그림에에서 나와 있는 것 처럼 hello 콘솔 창이 나타납니다.

![StorSimple 스냅숏 관리자 창](./media/storsimple-use-snapshot-manager/HCS_SSM_gui_panes.png)

hello 콘솔 창에 5 개의 주요 요소가 있습니다. 각 요소에 대 한 전체 설명은 hello 적절 한 링크를 클릭 합니다.

* [메뉴 모음](#menu-bar) 
* [도구 모음](#tool-bar) 
* [범위 창](#scope-pane) 
* [결과 창](#results-pane) 
* [작업 창](#actions-pane) 

StorSimple 스냅숏 관리자 지원 hello 또한 [키보드 탐색 및 바로 가기 키 수가](#keyboard-navigation-and-shortcuts)합니다.

### <a name="console-accessibility"></a>콘솔의 내게 필요한 옵션
hello StorSimple 스냅숏 관리자 사용자 인터페이스는 hello Windows 운영 체제 및 MMC Microsoft Management Console (), hello 뿐만 아니라 일부 StorSimple 스냅숏 관리자 관련 바로 가기 키에서 제공 하는 hello 내게 필요한 옵션 기능을 지원 합니다. 

* Hello Windows 내게 필요한 옵션 기능에 대 한 이동 너무[Windows에 대 한 바로 가기 키](https://support.microsoft.com/kb/126449)합니다. 
* Hello MMC 접근성 기능에 대 한 이동 너무[MMC 3.0에 대 한 내게 필요한 옵션](https://technet.microsoft.com/library/cc766075.aspx)
* Hello StorSimple 스냅숏 관리자 접근성 기능에 대 한 이동 너무[키보드 탐색 및 바로 가기](#keyboard-navigation-and-shortcuts)합니다.

## <a name="menu-bar"></a>메뉴 모음
hello hello 콘솔 창 위쪽에 hello 메뉴 모음에 [파일](#file-menu), [동작](#action-menu), [보기](#view-menu), [즐겨찾기](#favorites-menu), [창 ](#window-menu), 및 [도움말](#help-menu) 메뉴.

해당 메뉴에서 사용할 수 있는 명령 hello 메뉴 모음 toosee 목록에서 임의의 항목을 클릭 합니다. hello 다음 예제에서는 hello **보기** 메뉴 hello 메뉴 모음에서 선택 합니다.

![보기 메뉴 선택](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png)

### <a name="file-menu"></a>파일 메뉴
hello **파일** 메뉴 표준 관리 MMC (Microsoft Console) 명령이 포함 됩니다.

#### <a name="menu-access"></a>메뉴 액세스
tooview hello **파일** 메뉴를 클릭 하 여 **파일** hello 메뉴 모음에서 합니다. 다음 메뉴 hello가 나타납니다.

![StorSimple 스냅숏 관리자 파일 메뉴](./media/storsimple-use-snapshot-manager/HCS_SSM_FileMenu.png) 

#### <a name="menu-description"></a>메뉴 설명
hello 다음 표에 표시 되는 항목에 hello **파일** 메뉴.

| 메뉴 항목 | 설명 |
|:--- |:--- |
| 새로 만들기 |클릭 **새로** toocreate hello StorSimple 스냅숏 관리자를 기반으로 새 콘솔. |
| 열기 |클릭 **열려** tooopen 기존 콘솔. |
| 저장 |클릭 **저장** toosave hello 현재 콘솔. |
| 다른 이름으로 저장 |클릭 **다른 이름으로 저장** toocreate hello 현재 콘솔의 이름이 바뀐된 새 인스턴스를 합니다. 사용 하 여 hello **다른 이름으로 저장** toocustomize 보기 옵션 나중에 검색을 위해 저장 합니다. 예를 들어 해당 지점 toospecific 서버 스냅인 StorSimple 스냅숏 관리자를 만들 수 있습니다. |
| 스냅인 추가/제거 |클릭 **스냅인 추가/제거** tooadd 스냅인 및 tooorganize 제거 또는 노드 hello에 **범위** 창. 자세한 내용은 이동 너무[추가, 제거 및 구성 스냅인 및 MMC 3.0의 확장](https://technet.microsoft.com/library/cc722035.aspx)합니다. |
| 옵션 |클릭 **옵션** toochange hello 콘솔 아이콘 사용자 액세스 모드 및 권한과 지정 하거나 콘솔 파일 tooincrease 사용 가능한 디스크 공간을 삭제 합니다. |
| 파일 경로 목록 |Hello 번호 매기기 목록 tooreopen 최근에 연 파일의에서 경로 클릭 합니다. |
| 끝내기 |클릭 **종료** tooclose hello **파일** 메뉴. |

### <a name="action-menu"></a>동작 메뉴
사용 하 여 hello **동작** 에서 사용할 수 있는 동작 메뉴 tooselect 합니다. hello 항목 사용 가능한 tooyou hello 선택한 hello 내용에 따라 달라 집니다 **범위** 창 또는 **결과** 창.

#### <a name="menu-access"></a>메뉴 액세스
tooview hello **동작** 메뉴, hello 다음 중 하나를 수행 합니다.

* Hello에 있는 항목을 마우스 오른쪽 단추로 클릭 **범위** 창 또는 **결과** 창.
* Hello에서 항목을 선택 **범위** 창 또는 **결과** 창과 클릭 **동작** hello 메뉴 모음에서 합니다. 

예를 들어, hello에 hello 최상위 노드를 선택 하는 경우 **범위** 창에서 다음 마우스 오른쪽 단추로 클릭 하거나 클릭 **동작** hello 메뉴 모음에서 hello 다음과 같은 메뉴가 나타납니다.

![StorSimple 스냅숏 관리자 동작 메뉴](./media/storsimple-use-snapshot-manager/HCS_SSM_Action_menu.png)

hello **작업** hello를 포함 하는 창 (hello 콘솔의 오른쪽 hello)에서 동일한 작업 목록이 hello로 **동작** 메뉴. 또한 hello **동작** 창은 hello **보기** toocreate hello의 사용자 지정 보기를 사용할 수 있는 메뉴 옵션 **결과** 창.

![보기 메뉴가 열린 작업 창](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

#### <a name="menu-description"></a>메뉴 설명
다음 표에 hello 사전순으로 StorSimple 스냅숏 관리자 작업을 포함 합니다. 

* hello **동작** 열 노드 및 결과 대해 수행할 수 있는 작업을 나열 합니다. 
* hello **탐색** 열 toodisplay hello 적절 한 방법을 설명 **동작** 메뉴 hello 동작을 선택할 수 있도록 합니다. 일부 동작에는 여러 **동작** 메뉴가 있습니다. 이러한 작업에 대 한 하나를 선택 **탐색** hello 글머리 기호 목록에서 옵션입니다. 
* hello **설명** 열에 설명 방법을 toouse hello에 각 작업 **동작** 메뉴 또는 작업 창에서 역할에 대해 설명 합니다.

> [!NOTE]
> hello **동작** 창 및 **동작** 메뉴와 같은 추가 옵션을 포함할 **보기**, **여기에서 창 새로 만들기**,  **새로 고침**, **목록 내보내기**, 및 **도움말**합니다. 이러한 옵션 hello MMC의 일부로 사용할 수 있으며 특정 tooStorSimple 스냅숏 관리자 되지 않습니다. hello 테이블에는 이러한 옵션의 설명이 포함 되어 있습니다.
> 
> 

| 동작 | 탐색 | 설명 |
|:--- |:--- |:--- |
| 인증 |Hello 클릭 **장치** 노드를 마우스 오른쪽 단추로 클릭 hello에서 장치 **결과** 창. |클릭 **Authenticate** hello 장치에 대해 구성한 tooenter hello 암호입니다. |
| 복제 |확장 **백업 카탈로그**를 확장 하 고 **클라우드 스냅숏**날짜가 지정 된 백업을 클릭 하 고 다음 hello에서 볼륨을 선택 **결과** 창. |클릭 **복제** toocreate 클라우드 스냅숏 및 복사본 지정 하는 위치에 저장 합니다. |
| 장치 구성 |마우스 오른쪽 단추로 클릭 hello **장치** 노드. |클릭 **장치 구성** tooconfigure 장치를 하나 또는 여러 장치 tooconnect toohello Windows 호스트 합니다. |
| 백업 정책 만들기 |Hello 다음 중 하나를 수행 합니다.<ul><li>**백업 정책**을 마우스 오른쪽 단추로 클릭합니다.</li><li>**볼륨 그룹**을 클릭하거나 확장한 다음 볼륨 그룹을 마우스 오른쪽 단추로 클릭합니다.</li><li>**백업 카탈로그**를 클릭하거나 확장한 다음 볼륨 그룹을 마우스 오른쪽 단추로 클릭합니다.</li></ul> |클릭 **백업 정책 만들기** tooconfigure 볼륨 그룹에 대 한 예약 된 백업입니다. |
| 볼륨 그룹 만들기 |Hello 다음 중 하나를 수행 합니다.<ul><li>Hello 클릭 **볼륨** 노드를 마우스 오른쪽 단추로 hello에서 볼륨을 **결과** 창.</li><li>마우스 오른쪽 단추로 클릭 hello **볼륨 그룹** 노드.</li></ul> |클릭 **볼륨 그룹 만들기** tooassign 볼륨 tooa 볼륨 그룹입니다. |
| 삭제 |노드 또는 결과(여러 **작업** 메뉴 및 **작업** 창에 표시되는 항목)를 클릭합니다. |클릭 **삭제** toodelete hello 노드 또는 결과 선택 합니다. Hello 확인 대화 상자가 표시 될 때 확인 하거나 hello 삭제를 취소 합니다. |
| 세부 정보 |Hello 클릭 **장치** 노드를 마우스 오른쪽 단추로 hello에서 장치 **결과** 창. |클릭 **세부 정보** toosee hello 구성 세부 정보는 장치에 대 한 합니다. |
| 편집 |클릭 **백업 정책**, hello에서 정책을 마우스 오른쪽 단추로 클릭 하 고 **결과** 창. |클릭 **편집** toochange hello 볼륨 그룹에 대 한 백업 일정입니다. |
| 목록 내보내기 |노드 또는 결과(모든 **작업** 메뉴 및 **작업** 창에 표시되는 항목)를 클릭합니다. |클릭 **목록 내보내기** toosave 쉼표로 구분 된 값 (CSV) 파일의 목록입니다. 그런 다음 분석을 위해 이 파일을 스프레드시트 응용 프로그램으로 내보낼 수 있습니다. |
| 도움말 |노드 또는 결과를 클릭합니다. 이 항목은 모든 **작업** 메뉴 및 **작업** 창에 나타납니다. |클릭 **도움말** tooopen 별도 브라우저 창에서 온라인 도움말입니다. |
| 여기에서 창 새로 만들기 |노드 또는 결과(모든 **작업** 메뉴 및 **작업** 창에 표시되는 항목)를 클릭합니다. |클릭 **여기에서 창 새로 만들기** tooopen 새 StorSimple 스냅숏 관리자 창. |
| 새로 고침 |노드 또는 결과(모든 **작업** 메뉴 및 **작업** 창에 표시되는 항목)를 클릭합니다. |클릭 **새로 고침** tooupdate 현재 표시 된 hello StorSimple 스냅숏 관리자 창. |
| 장치 새로 고침 |Hello 클릭 **장치** 노드를 마우스 오른쪽 단추로 클릭 hello에서 장치 **결과** 창. |클릭 **장치 새로 고침** toosynchronize StorSimple 스냅숏 관리자와 같은 특정 연결 된 장치. |
| 장치 새로 고침 |마우스 오른쪽 단추로 클릭 hello **장치** 노드. |클릭 **장치 새로 고침** toosynchronize StorSimple 스냅숏 관리자 연결 된 장치 목록입니다. |
| 볼륨 다시 검사 |마우스 오른쪽 단추로 클릭 hello **볼륨** 노드. |클릭 **볼륨 다시 검사** tooupdate hello 볼륨 목록이 hello에 나타나는 **결과** 창. |
| 복원 |**백업 카탈로그**, 볼륨 그룹, **로컬 스냅숏** 또는 **클라우드 스냅숏**을 차례로 확장한 다음 백업을 마우스 오른쪽 단추로 클릭합니다. |클릭 **복원** tooreplace hello 현재 볼륨 그룹 데이터와 데이터 hello hello 선택한 백업에서 합니다. |
| 백업 수행 |Hello 다음 중 하나를 수행 합니다.<ul><li>**볼륨 그룹**을 확장한 다음 볼륨 그룹을 마우스 오른쪽 단추로 클릭합니다.</li><li>**백업 카탈로그**를 확장한 다음 볼륨 그룹을 마우스 오른쪽 단추로 클릭합니다.</li></ul> |클릭 **백업 수행** toostart 백업 작업을 즉시 합니다. |
| 가져오기 표시 토글 |Hello에서 마우스 오른쪽 단추로 클릭 hello 최상위 노드 **범위** 창 (hello **StorSimple 스냅숏 관리자** hello 예에서 노드). |클릭 **가져오기 표시 토글** tooshow 또는 숨기기 hello 볼륨 그룹 및 연결 된 백업에서 가져온 hello StorSimple 장치 관리자 서비스 대시보드 합니다. |

### <a name="view-menu"></a>보기 메뉴
사용 하 여 hello **보기** 메뉴 toocreate hello의 사용자 지정 보기 **결과** 창 내용입니다. hello **보기** 메뉴에 **열 추가/제거** 및 **사용자 지정** 옵션입니다.

#### <a name="menu-access"></a>메뉴 액세스
Hello에 액세스할 수 있습니다 **보기** hello 또는 hello 메뉴 모음의 메뉴 **동작** 창.

![StorSimple 스냅숏 관리자 보기 메뉴](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png) 

#### <a name="menu-description"></a>메뉴 설명
hello 다음 표에 표시 되는 항목에 hello **보기** 메뉴.

| 메뉴 항목 | 설명 |
|:--- |:--- |
| 열 추가/제거 |클릭 **열 추가/제거** hello의 tooadd / 제거 열 **결과** 창. |
| 사용자 지정 |클릭 **사용자 지정** hello StorSimple 스냅숏 관리자 콘솔 창에 tooshow 또는 숨기기 항목입니다. |

### <a name="favorites-menu"></a>즐겨찾기 메뉴
Hello를 사용 하 여 **즐겨찾기** 메뉴 tooadd 제거 및 페이지 보기 및 자주 사용 하는 작업을 구성 합니다. 

#### <a name="menu-access"></a>메뉴 액세스
Hello에 액세스할 수 있습니다 **즐겨찾기** hello 메뉴 모음의 메뉴입니다.

![StorSimple 스냅숏 관리자 즐겨찾기 메뉴](./media/storsimple-use-snapshot-manager/HCS_SSM_FavoritesMenu.png)

#### <a name="menu-description"></a>메뉴 설명
hello 다음 표에 표시 되는 항목에 hello **즐겨찾기** 메뉴.

| 메뉴 항목 | 설명 |
|:--- |:--- |
| TooFavorites 추가 |클릭 **tooFavorites 추가** tooadd hello 현재 보기 tooyour 즐겨찾기 목록에 있습니다. |
| 즐겨찾기 구성 |클릭 **즐겨찾기 구성** tooorganize hello 내용의 즐겨찾기 폴더에 있습니다. |

### <a name="window-menu"></a>창 메뉴
사용 하 여 hello **창** 메뉴 tooadd 및 다시 정렬 StorSimple 스냅숏 관리자 콘솔 창입니다.

#### <a name="menu-access"></a>메뉴 액세스
Hello에 액세스할 수 있습니다 **창** hello 메뉴 모음의 메뉴입니다.

![StorSimple 스냅숏 관리자 창 메뉴](./media/storsimple-use-snapshot-manager/HCS_SSM_WindowMenu.png)

hello hello 메뉴 맨 아래에 hello 번호 매기기 목록 열려 있는 현재 hello 창이 표시 됩니다. Hello 전경으로 해당 목록 toobring hello 창에서 클릭 합니다. 

#### <a name="menu-description"></a>메뉴 설명
hello 다음 표에 표시 되는 hello 항목 hello 창 메뉴에 있습니다.

| 메뉴 항목 | 설명 |
|:--- |:--- |
| 새 창 |클릭 **새 창** tooopen 더하기 toohello 기존 창에서 새 콘솔 창. |
| 계단식 배열 |클릭 **Cascade** toodisplay hello 열려 있는 콘솔 창을 계단식으로 합니다. |
| 가로 바둑판식 배열 |클릭 **가로 바둑판식 배열** toodisplay hello 열려 있는 콘솔 창을 바둑판 (또는 그리드) 형식입니다. |
| 아이콘 정렬 |여러 개의 콘솔 windows 열고 최소화 한 다음 클릭 바탕 화면에 흩어져 있는 경우 **아이콘 정렬** tooarrange hello 화면 아래쪽에 가로 행에서 해당 합니다. |

### <a name="help-menu"></a>도움말 메뉴
사용 하 여 hello **도움말** 메뉴 tooview 사용 가능한 온라인 도움말 StorSimple 스냅숏 관리자 및 MMC hello에 대 한 합니다. 또한 현재 시스템에 설치 되어 있는 hello MMC 및 StorSimple 스냅숏 관리자 소프트웨어 버전에 대 한 정보를 볼 수 있습니다. 

Hello에 액세스할 수 있습니다 **도움말** hello 메뉴 모음의 메뉴입니다. Hello에서 StorSimple 스냅숏 관리자 도움말 항목에 액세스할 수도 있습니다 **동작** 창.

![StorSimple 스냅숏 관리자 도움말 메뉴](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpMenu.png)

#### <a name="menu-description"></a>메뉴 설명
다음 표에서 hello hello 도움말 메뉴에 표시 되는 항목을 설명 합니다.

| 메뉴 항목 | 설명 |
|:--- |:--- |
| StorSimple 스냅숏 관리자 도움말 |클릭 **StorSimple 스냅숏 관리자에서 도움말** tooopen 별도 창에 StorSimple 스냅숏 관리자 도움말입니다. |
| 도움말 항목 |클릭 **도움말 항목** tooopen 별도 창에서 MMC 온라인 도움말입니다. |
| TechCenter 웹 사이트 |클릭 **TechCenter 웹 사이트** tooopen hello Microsoft TechNet Tech Center 홈페이지 별도 창에서. |
| Microsoft Management Console 정보 |클릭 **Microsoft Management Console 정보** 어떤 버전의 Microsoft Management Console hello toosee 시스템에 설치 됩니다. |
| StorSimple 스냅숏 관리자 정보 |클릭 **StorSimple 스냅숏 관리자에 대 한** toosee 시스템에 설치 된 스냅인 hello의 버전입니다. |

## <a name="tool-bar"></a>도구 모음
hello 메뉴 모음 아래에 있는 hello 도구 모음에 탐색 및 작업 아이콘이 포함 되어 있습니다. 각 아이콘에는 바로 가기 tooa 특정 작업입니다.

### <a name="icon-descriptions"></a>아이콘 설명
hello 다음 표에 나타나는 hello 아이콘 hello 도구 모음에 있습니다. 

| 아이콘 | 설명 |
|:--- |:--- |
| ![왼쪽 화살표](./media/storsimple-use-snapshot-manager/HCS_SSM_LeftArrow.png) |Hello 왼쪽된 화살표 아이콘 tooreturn toohello 이전 페이지를 클릭 합니다. |
| ![오른쪽 화살표](./media/storsimple-use-snapshot-manager/HCS_SSM_RightArrow.png) |Hello 오른쪽 화살표 toogo toohello 다음 페이지를 클릭 (hello 화살표 회색 이면 hello 동작은 사용할 수 없습니다). |
| ![위로 아이콘](./media/storsimple-use-snapshot-manager/HCS_SSM_Up.png) |콘솔 트리에서 hello에서 한 수준 위로 아이콘 toogo hello 클릭 (hello **범위** 창). |
| ![콘솔 트리 표시/숨기기](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowConsoleTree.png) |Hello 표시/숨기기 콘솔 트리 아이콘 tooshow 클릭 또는 hello 숨기기 **범위** 창. |
| ![목록 내보내기](./media/storsimple-use-snapshot-manager/HCS_SSM_ExportListIcon.png) |Hello 내보내기 목록 아이콘 tooexport 지정 하는 목록 tooa CSV 파일을 클릭 합니다. |
| ![도움말 아이콘](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpIcon.png) |Hello 도움말 아이콘 tooopen 온라인 MMC 도움말 항목을 클릭 합니다. |
| ![작업 창 표시/숨기기](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowAction.png) |Hello 표시/숨기기 클릭 **동작** 창 아이콘 tooshow 또는 숨기기 hello **동작** 창. |

## <a name="scope-pane"></a>범위 창
hello **범위** 창이 hello hello StorSimple 스냅숏 관리자 UI에서에서 가장 왼쪽에 있는 창입니다. Hello 콘솔 (또는 노드) 트리가 포함 하 고 StorSimple 스냅숏 관리자에 대 한 hello 기본 탐색 메커니즘입니다. 

### <a name="scope-pane-structure"></a>범위 창 구조
hello **범위** 창 트리 구조로 구성 된 일련의 클릭 가능한 개체 (노드)에 포함 되어 있습니다. 

![범위 창](./media/storsimple-use-snapshot-manager/HCS_SSM_Scope_pane.png) 

* tooexpand 또는 노드를 축소 hello 화살표 아이콘 다음 toohello 노드 이름을 클릭 합니다.
* tooview hello 상태 또는 노드의 내용을 hello 노드 이름을 클릭 합니다. hello에 hello 정보가 표시 **결과** 창. 

hello **범위** 창 hello 노드 뒤에 포함 되어 있습니다. 

* [장치 노드](#devices-node) 
* [볼륨 노드](#volumes-node) 
* [볼륨 그룹 노드](#volume-groups-node) 
* [백업 정책 노드](#backup-policies-node) 
* [백업 카탈로그 노드](#backup-catalog-node) 
* [작업 노드](#jobs-node) 

### <a name="scope-pane-tasks"></a>범위 창 작업
Hello를 사용할 수 있습니다 **범위** 창 toocomplete 특정 노드에 대 한 작업입니다. 작업을 tooselect hello 다음 중 하나를 수행 합니다.

* Hello 노드를 마우스 오른쪽 단추로 클릭 하 고 표시 되는 hello 메뉴에서 hello 작업을 선택 합니다.
* Hello 노드를 클릭 한 다음 클릭 **동작** hello 메뉴 모음에서 합니다. 표시 되는 hello 메뉴에서 hello 작업을 선택 합니다.
* Hello 노드를 선택한 다음 선택 hello 동작 hello에 클릭 **동작** 창.

노드를 선택 하 고 있는 작업 목록이 이러한 메서드 toosee 중 하나를 사용 하 여 해당 노드에서 수행할 수 있는 작업에만 표시 됩니다.

### <a name="devices-node"></a>장치 노드
hello **장치** hello StorSimple 장치 및 연결 된 tooStorSimple 스냅숏 관리자는 StorSimple 가상 장치 노드를 나타냅니다. 이 노드 tooconnect 선택 장치를 구성 하 고 해당 연결 된 볼륨, 볼륨 그룹 및 기존 백업 복사본을 가져옵니다. 여러 장치에 연결 된 tooa 단일 호스트 될 수 있습니다.

* tooexpand hello 노드를 다음 너무 hello 화살표 아이콘을 클릭**장치**합니다.
* 사용할 수 있는 동작 메뉴 toosee hello를 마우스 오른쪽 단추로 클릭 **장치** 노드나 마우스 오른쪽 단추로 클릭 hello에 나타나는 hello 노드의 보기를 확장 합니다.
* 구성 된 장치 목록을 toosee 클릭 **장치** hello에 **범위** 창. hello에 hello 각 장치에 대 한 정보와 함께 장치 목록이 표시 됩니다 **결과** 창.

### <a name="volumes-node"></a>볼륨 노드
hello **볼륨** 노드는 iSCSI 나 장치를 통해 검색 된 것까지 포함 하 여 hello 호스트가 마운트한 toohello 볼륨을 해당 하는 hello 드라이브를 나타냅니다. 이 노드 tooview hello 목록을 사용할 수 있는 볼륨의 사용 및 toovolume 그룹 개별 볼륨을 할당 합니다.

* tooexpand hello 노드를 다음 너무 hello 화살표 아이콘을 클릭**볼륨**합니다.
* 사용할 수 있는 동작 메뉴 toosee hello를 마우스 오른쪽 단추로 클릭 **볼륨** 노드나 마우스 오른쪽 단추로 클릭 hello에 나타나는 hello 노드의 보기를 확장 합니다.
* 볼륨 목록이 toosee 클릭 **볼륨** hello에 **범위** 창. hello에 각 볼륨에 대 한 정보와 함께 볼륨 목록이 hello 표시 **결과** 창.

### <a name="volume-groups-node"></a>볼륨 그룹 노드
볼륨 그룹은 일관성 그룹이라고도 합니다. 각 볼륨 그룹은 백업 작업 중 tooensure 응용 프로그램 일관성에 도움이 되는 응용 프로그램 관련 볼륨의 풀입니다. 사용 하 여 hello **볼륨 그룹** 노드 tooconfigure 이러한 그룹 및 tootake 대화형 백업을 하거나 백업 일정을 만듭니다. 

* tooexpand hello 노드를 다음 너무 hello 화살표 아이콘을 클릭**볼륨 그룹**합니다.
* 사용할 수 있는 동작 메뉴 toosee hello를 마우스 오른쪽 단추로 클릭 **볼륨 그룹** 노드나 마우스 오른쪽 단추로 클릭 hello에 나타나는 hello 노드의 보기를 확장 합니다.
* 볼륨 그룹 목록이 toosee 클릭 **볼륨 그룹** hello에 **범위** 창. hello에 hello 각 볼륨 그룹에 대 한 정보와 함께 볼륨 그룹 목록이 표시 됩니다 **결과** 창.

### <a name="backup-policies-node"></a>백업 정책 노드
백업 정책은 로컬 및 클라우드 스냅숏의 작업 일정입니다. 사용 하 여 hello **백업 정책** 노드 toospecify는 백업을 만드는 빈도 및 기간 백업 해야 유지 합니다. 

* tooexpand hello 노드를 다음 너무 hello 화살표 아이콘을 클릭**백업 정책**합니다.
* 사용할 수 있는 동작 메뉴 toosee hello를 마우스 오른쪽 단추로 클릭 **백업 정책** 노드나 마우스 오른쪽 단추로 클릭 hello에 나타나는 hello 노드의 보기를 확장 합니다.
* 백업 정책 목록을 toosee 클릭 **백업 정책** hello에 **범위** 창. hello에 hello 각 정책에 대 한 정보와 함께 백업 정책 목록이 표시 됩니다 **결과** 창.

> [!NOTE]
> 최대 64개의 백업을 유지할 수 있습니다.


### <a name="backup-catalog-node"></a>백업 카탈로그 노드
hello **백업 카탈로그** 노드 Azure StorSimple 볼륨의 온사이트 및 오프 사이트 백업의 목록을 포함 합니다. 이 노드는 볼륨 그룹별로 구성 하 고 각 볼륨 그룹 컨테이너 위치에 로컬 스냅숏에 대 한 별도 구조가 (hello **로컬 스냅숏**s 노드) 및 클라우드 스냅숏 (hello **클라우드 스냅숏** 노드 ). 확장 하면 각 볼륨 그룹 컨테이너에 대화형으로 또는 구성 된 정책에 의해 수행 된 모든 hello 성공적인 백업이 나열 됩니다.

* tooexpand hello 노드를 다음 너무 hello 화살표 아이콘을 클릭**백업 카탈로그**합니다.
* 사용할 수 있는 동작 메뉴 toosee hello를 마우스 오른쪽 단추로 클릭 **백업 카탈로그** 노드나 마우스 오른쪽 단추로 클릭 hello에 나타나는 hello 노드의 보기를 확장 합니다.
* 백업 스냅숏 목록을 toosee 클릭 **백업 카탈로그** hello에 **범위** 창. hello에 hello 각 스냅숏에 대 한 정보와 함께 스냅숏 목록이 표시 됩니다 **결과** 창.

### <a name="local-snapshots-node"></a>로컬 스냅숏 노드
hello **로컬 스냅숏** 노드는 특정 볼륨 그룹에 대 한 로컬 스냅숏을 나열 합니다. hello 노드 hello 아래에 있는 **백업 카탈로그** hello에 대 한 노드 **범위** 창. 로컬 스냅숏은 hello Azure StorSimple 장치에 저장 된 볼륨 데이터의 지정 시간 복사본입니다. 일반적으로 이러한 유형의 백업은 신속하게 만들고 복원할 수 있습니다. 로컬 스냅숏은 로컬 백업 사본처럼 사용할 수 있습니다.

* tooexpand hello 노드를 다음 너무 hello 화살표 아이콘을 클릭**로컬 스냅숏**합니다.
* 사용할 수 있는 동작 메뉴 toosee hello를 마우스 오른쪽 단추로 클릭 **로컬 스냅숏** 노드나 마우스 오른쪽 단추로 클릭 hello에 나타나는 hello 노드의 보기를 확장 합니다.
* 로컬 스냅숏 목록을 toosee 클릭 **로컬 스냅숏** hello에 **범위** 창. hello에 hello 각 스냅숏에 대 한 정보와 함께 스냅숏 목록이 표시 됩니다 **결과** 창.

### <a name="cloud-snapshots-node"></a>클라우드 스냅숏 노드
hello **클라우드 스냅숏** 노드는 특정 볼륨 그룹에 대 한 클라우드 스냅숏을 나열 합니다. hello 노드 hello 아래에 있는 **백업 카탈로그** hello에 대 한 노드 **범위** 창. 클라우드 스냅숏은 hello 클라우드에 저장 된 볼륨 데이터의 지정 시간 복사본입니다. 클라우드 스냅숏은 같습니다 tooa 스냅숏 다른 오프 사이트 저장소 시스템에 복제 합니다. 클라우드 스냅숏은 특히 재해 복구 상황에서 유용합니다.

* tooexpand hello 노드를 다음 너무 hello 화살표 아이콘을 클릭**클라우드 스냅숏**합니다.
* 사용할 수 있는 동작 메뉴 toosee hello를 마우스 오른쪽 단추로 클릭 **클라우드 스냅숏** 노드나 마우스 오른쪽 단추로 클릭 hello에 나타나는 hello 노드의 보기를 확장 합니다.
* 클라우드 스냅숏 목록을 toosee 클릭 **클라우드 스냅숏** hello에 **범위** 창. hello에 hello 각 스냅숏에 대 한 정보와 함께 스냅숏 목록이 표시 됩니다 **결과** 창.

### <a name="jobs-node"></a>작업 노드
hello **작업** 노드 예약, 실행 및 최근에 완료 된 백업 작업에 대 한 정보를 포함 합니다. 

* tooexpand hello 노드를 다음 너무 hello 화살표 아이콘을 클릭**작업**합니다.
* 사용할 수 있는 동작 메뉴 toosee hello를 마우스 오른쪽 단추로 클릭 **작업** 노드나 마우스 오른쪽 단추로 클릭 hello에 나타나는 hello 노드의 보기를 확장 합니다.
* 예약 된 작업의 목록을 toosee 확장 hello **작업** 노드를 차례로 클릭 한 다음 **예약 된**합니다. hello 목록이 이전에 구성 된 작업과 각 작업에 대 한 정보에에서 표시 hello **결과** 창. 
* toosee 최근에 완료 된 작업 목록이 확장 hello **작업** 노드를 차례로 클릭 한 다음 **마지막 24 시간**합니다. Hello에 지난 24 시간 동안 hello 내에 완료 된 작업 목록이 표시 됩니다. **결과** 창. hello **결과** 창도 완료 된 각 작업에 대 한 정보를 포함 합니다.
* 현재 실행 중인 작업 목록을 toosee 확장 hello **작업** 노드를 차례로 클릭 한 다음 **실행**합니다. hello에 hello 현재 실행 중인 작업 및 각 작업에 대 한 정보 목록이 표시 됩니다 **결과** 창.

## <a name="results-pane"></a>결과 창
hello **결과** 창이 hello StorSimple 스냅숏 관리자 UI에서에서 hello 가운데 창입니다. 목록 및 hello에서 선택한 hello 노드에 대 한 자세한 상태 정보 **범위** 창.

### <a name="example"></a>예제
다음 예제를 toosee hello 클릭 hello **볼륨 그룹** hello에 대 한 노드 **범위** 창. hello **결과** 창에 각 그룹에 대 한 세부 정보와 함께 볼륨 그룹 목록이 표시 됩니다.

![결과 창](./media/storsimple-use-snapshot-manager/HCS_SSM_Results_pane.png) 

Hello에 표시 된 hello 세부 정보를 구성할 수 있습니다 **결과** 창: hello에 노드를 마우스 오른쪽 단추로 클릭 **범위** 창에서 클릭 **보기**, 클릭 하 고 **추가/제거 열**합니다.

## <a name="actions-pane"></a>작업 창
hello **동작** 창이 hello hello StorSimple 스냅숏 관리자 UI에서에서 오른쪽 창입니다. Hello 노드, 뷰 또는 hello에서 선택 하는 데이터에서 수행할 수 있는 작업의 메뉴가 포함 **범위** 창 또는 **결과** 창. hello **작업** 창은 hello로 명령을 동일 hello **동작** hello 항목에 사용할 수 있는 메뉴 **범위** 창 및 **결과**창. 각 동작에 대 한 hello에 hello 표를 참조 **동작** 메뉴 섹션.

### <a name="examples"></a>예
다음 예에서는 hello에 toosee hello **범위** 창 hello 확장 **작업** 노드와 클릭 **예약 된**합니다. hello **동작** hello hello에 대 한 사용 가능한 작업 창에 표시 됩니다 **예약 된** 노드.

![작업 창 예약 작업 예제](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane.png) 

hello에 toosee에서 기타 옵션 **범위** 창 hello 확장 **작업** 노드를 클릭 하 여 **예약 된**, hello에 예약된 된 작업을 클릭 하 고 **결과**창. hello **동작** 창 hello 다음 예제와 같이 hello hello 예약 된 작업에 사용 가능한 작업에 표시 됩니다.

![작업 창 작업 동작 예제](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

## <a name="keyboard-navigation-and-shortcuts"></a>키보드 탐색 및 바로 가기
StorSimple 스냅숏 관리자 hello Windows 운영 체제 및 MMC Microsoft Management Console () hello hello 내게 필요한 옵션 기능을 사용할 수 있습니다. 도 몇 가지 키보드 탐색 기능 및 특정 toohello StorSimple 스냅숏 관리자 되는 바로 가기 hello 다음 섹션에에서 설명 된 대로.

* [키보드 탐색 키](#keyboard-navigation-keys) 
* [메뉴 모음 바로 가기 키](#menu-bar-shortcut-keys) 
* [범위 창 바로 가기 키](#scope-pane-shortcut-keys) 

### <a name="keyboard-navigation-keys"></a>키보드 탐색 키
hello 다음 표에 hello 키 toonavigate hello StorSimple 스냅숏 관리자 사용자 인터페이스를 사용할 수 있습니다. 

| 탐색 키 | 동작 |
|:--- |:--- |
| 아래쪽 화살표 키 |아래쪽 화살표 키 toomove hello를 사용 하 여 세로로 메뉴 또는 창에서 다음 항목 toohello 합니다. |
| Enter |Hello Enter 키 toocomplete 동작을 누르고 toohello 다음 단계를 진행 합니다. 예를 들어 누르면 Enter tooselect **다음**, **확인**, 또는 **만들기**, toohello는 마법사의 다음 단계를 이동 합니다. |
| Esc |Hello Esc 키 tooclose 메뉴 또는 toocancel 키를 누릅니다 하 고 페이지를 닫습니다. |
| F1 |Hello 현재 활성 창에 대 한 hello F1 키 tooview 도움말 항목을 키를 누릅니다. |
| F5 |Hello F5 키 toorefresh 노드에 키를 누릅니다. |
| F6 |Hello F6 키 toomove hello에서 키를 눌러 **범위** 창 toohello **결과** 창. |
| F10 |Hello F10 키 toogo toohello 메뉴 모음 키를 누릅니다. |
| 왼쪽 화살표 키 |메뉴 모음 옵션 toohello 이전 옵션에서 화살표 키 toomove를 가로 방향으로 왼쪽 hello를 사용 합니다. Toohello 이전 이동 하면 hello 이전 항목에 대 한 항목 hello 메뉴 모음, hello 작업 (또는 상황에 맞는) 메뉴가 나타납니다. |
| 오른쪽 화살표 키 |다음 하나의 메뉴 옵션 toohello 모음에서 가로로 오른쪽 화살표 키 toomove hello를 사용 합니다. 이동 하면 hello 새 항목에 대 한 다음 항목 hello 메뉴 모음, hello 작업 (또는 상황에 맞는) 메뉴 toohello 나타납니다. |
| Tab 키 |Hello 탭 키 toomove toohello 다음 창을 사용 하 여 hello 콘솔 또는 toohello 다음 선택 이나 텍스트 상자에 페이지에 있습니다. |
| 위쪽 화살표 키 |위쪽 화살표 키 toomove hello를 사용 하 여 세로로 toohello 메뉴나 창의 이전 항목입니다. |

### <a name="menu-bar-shortcut-keys"></a>메뉴 모음 바로 가기 키
hello 다음 표에서 설명 hello hello 메뉴 모음에 대 한 바로 가기 키 조합 합니다. Hello 바로 가기 키 누른 hello 메뉴가 열립니다 후 메뉴 바로 가기 키 (hello 메뉴에서 밑줄이 그어진된 키 hello)를 사용할 수 있습니다. 너무 hello 메뉴 모음에 대 한 자세한 내용을 보려면 이동[메뉴 모음](#menu-bar)합니다.

| 바로 가기 | 결과 | 메뉴 바로 가기 키 | 결과 |
|:--- |:--- |:--- |:--- |
| ALT + F |엽니다 hello **파일** 메뉴. |N |새 콘솔 인스턴스를 엽니다. |
|  |O |엽니다 hello **관리 도구** 페이지. | |
|  |S |Hello StorSimple 스냅숏 관리자 콘솔을 저장합니다. | |
|  |A |엽니다 hello **다른 이름으로 저장** 페이지. | |
|  |M |엽니다 hello **스냅인 추가/제거** 페이지. | |
|  |P |엽니다 hello **옵션** 페이지. | |
|  |H |온라인 도움말을 엽니다. | |
| ALT + A |엽니다 hello **동작** 메뉴. |I |Hello 가져오기 표시 옵션을 설정 및 해제 합니다. |
|  |W |새 StorSimple 스냅숏 관리자 콘솔을 엽니다. | |
|  |F |Hello StorSimple 스냅숏 관리자 콘솔을 업데이트합니다. | |
|  |L |엽니다 hello **목록 내보내기** 페이지. | |
|  |H |온라인 도움말을 엽니다. | |
| ALT + V |엽니다 hello **보기** 메뉴. |A |엽니다 hello **열 추가/제거** 페이지. |
|  |U |엽니다 hello **보기 사용자 지정** 페이지. | |
| ALT + O |엽니다 hello **즐겨찾기** 메뉴. |A |엽니다 hello **tooFavorites 추가** 페이지. |
|  |O |엽니다 hello **즐겨찾기 구성** 페이지. | |
| ALT + W |엽니다 hello **창** 메뉴. |N |다른 StorSimple 스냅숏 관리자 창이 열립니다. |
|  |C |모든 열려 있는 콘솔 창을 계단식으로 표시합니다. | |
|  |T |모든 열려 있는 콘솔 창을 그리드 모양으로 표시합니다. | |
|  |I |Hello 화면 아래쪽에 가로 행의 아이콘을 정렬합니다. | |
| ALT + H |엽니다 hello **도움말** 메뉴. |H |온라인 도움말을 엽니다. |
|  |T |Hello Microsoft TechNet Techcenter 웹 페이지를 엽니다. | |
|  |A |엽니다 hello **Microsoft Management Console 정보** 페이지. | |

### <a name="scope-pane-shortcut-keys"></a>범위 창 바로 가기 키
hello 다음 표에서 보여 hello 바로 가기 키 조합을 각 노드에 대 한 hello에 **범위** 창. 

* [장치 노드 바로 가기 키](#devices-node-shortcut-keys)
* [볼륨 노드 바로 가기 키](#volumes-node-shortcut-keys)
* [볼륨 그룹 노드 바로 가기 키](#volume-groups-node-shortcut-keys)
* [백업 정책 노드 바로 가기 키](#backup-policies-node-shortcut-keys)
* [백업 카탈로그 노드 바로 가기 키](#backup-catalog-node-shortcut-keys)
* [작업 노드 바로 가기 키](#jobs-node-shortcut-keys)

#### <a name="devices-node-shortcut-keys"></a>장치 노드 바로 가기 키
| 메뉴 바로 가기 | 결과 |
|:--- |:--- |
| C |엽니다 hello **장치 구성** 페이지. |
| D |장치 및 장치 세부 정보 hello 목록을 새로 고칩니다. |
| V |엽니다 hello **보기** 메뉴. |
| W |새 StorSimple 스냅숏 관리자 콘솔 hello에 초점을 맞춘 열립니다 **세부 정보** 노드. |
| F |Hello StorSimple 스냅숏 관리자 콘솔을 업데이트합니다. |
| L |엽니다 hello **목록 내보내기** 페이지. |
| H |온라인 도움말을 엽니다. |

#### <a name="volumes-node-shortcut-keys"></a>볼륨 노드 바로 가기 키
| 메뉴 바로 가기 | 결과 |
|:--- |:--- |
| V |볼륨 hello 목록을 업데이트 합니다. |
| V(두 번 누르기) |엽니다 hello **보기** 메뉴. |
| W |새 StorSimple 스냅숏 관리자 콘솔 hello에 초점을 맞춘 열립니다 **볼륨** 노드. |
| F |Hello StorSimple 스냅숏 관리자 콘솔을 업데이트합니다. |
| L |엽니다 hello **목록 내보내기** 페이지. |
| H |온라인 도움말을 엽니다. |

#### <a name="volume-groups-node-shortcut-keys"></a>볼륨 그룹 노드 바로 가기 키
| 메뉴 바로 가기 | 결과 |
|:--- |:--- |
| G |엽니다 hello **볼륨 그룹 만들기** 페이지. |
| V |엽니다 hello **보기** 메뉴. |
| W |새 StorSimple 스냅숏 관리자 콘솔 hello에 초점을 맞춘 열립니다 **볼륨 그룹** 노드. |
| F |Hello StorSimple 스냅숏 관리자 콘솔을 업데이트합니다. |
| L |엽니다 hello **목록 내보내기** 페이지. |
| H |온라인 도움말을 엽니다. |

#### <a name="backup-policies-node-shortcut-keys"></a>백업 정책 노드 바로 가기 키
| 메뉴 바로 가기 | 결과 |
|:--- |:--- |
| B |엽니다 hello **정책 만들기** 페이지. |
| V |엽니다 hello **보기** 메뉴. |
| W |새 StorSimple 스냅숏 관리자 콘솔 hello에 초점을 맞춘 열립니다 **볼륨 그룹** 노드. |
| F |Hello StorSimple 스냅숏 관리자 콘솔을 업데이트합니다. |
| L |엽니다 hello * * 목록 내보내기 * * 페이지. |
| H |온라인 도움말을 엽니다. |

#### <a name="backup-catalog-node-shortcut-keys"></a>백업 카탈로그 노드 바로 가기 키
| 메뉴 바로 가기 | 결과 |
|:--- |:--- |
| W |새 StorSimple 스냅숏 관리자 콘솔 hello에 초점을 맞춘 열립니다 **볼륨 그룹** 노드. |
| F |Hello StorSimple 스냅숏 관리자 콘솔을 업데이트합니다. |
| H |온라인 도움말을 엽니다. |

#### <a name="jobs-node-shortcut-keys"></a>작업 노드 바로 가기 키
| 메뉴 바로 가기 | 결과 |
|:--- |:--- |
| V |엽니다 hello **보기** 메뉴. |
| W |새 StorSimple 스냅숏 관리자 콘솔 hello에 초점을 맞춘 열립니다 **작업** 노드. |
| F |Hello StorSimple 스냅숏 관리자 콘솔을 업데이트합니다. |
| L |엽니다 hello **목록 내보내기** 페이지. |
| H |온라인 도움말을 엽니다. |

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[StorSimple 솔루션 tooadminister StorSimple 스냅숏 관리자를 사용 하 여](storsimple-snapshot-manager-admin.md)합니다.
* 너무 방법에 대해 알아봅니다[tooconnect StorSimple 스냅숏 관리자를 사용 하 고 장치를 관리](storsimple-snapshot-manager-manage-devices.md)합니다.


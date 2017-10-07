---
title: "aaaMicrosoft 위협 모델링 도구-Azure | Microsoft Docs"
description: "Hello 위협 모델링 도구에서에서 사용할 수 있는 모든 hello 기능에 알아보기"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a>위협 모델링 도구 기능 개요

우리는 위협 모델링 요구 사항에 대해 toouse hello 위협 모델링 도구를 선택한 주셔서 감사 드립니다! 그렇게 하지 않은 경우 방문  **[hello 위협 모델링 도구 시작](./azure-security-threat-modeling-tool-getting-started.md)**  toolearn hello 기본 사항입니다.

> 이 도구는 자주 업데이트 되므로이 확인 하세요 우리의 최신 기능 및 향상 된 종종 toosee를 안내 합니다.

Hello "새 모델 만들기" 단추 클릭 하면 빈 시작 페이지, 아래와 유사한 toohello 이미지 열립니다.

![빈 시작 페이지](./media/azure-security-threat-modeling-tool/tmtstart.png)

Hello에 팀에서 만든 hello 위협 모델을 사용 하 여  **[시작](./azure-security-threat-modeling-tool-getting-started.md)**  예제에서는 현재 hello 도구에서 사용할 수 있는 모든 hello 기능을 사용해 확인해 보겠습니다.

![기본 위협 모델](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a>탐색

Hello 기본 제공 기능을 알아보기 전에 검토해 hello 도구에 있는 hello 주 구성 요소

### <a name="menu-items"></a>메뉴 항목

hello 경험 유사한 tooother Microsoft 제품 이어야 합니다. Hello 최상위 메뉴 항목 간을 이동 하 여 시작 해 보겠습니다.

![메뉴 항목](./media/azure-security-threat-modeling-tool/menuitems.png)

| 레이블                               | 세부 정보      |
| --------------------------------------- | ------------ |
| **파일** | <ul><li>파일 열기, 저장 및 닫기</li><li>OneDrive 계정의 로그인/로그아웃</li><li>공유 링크(보기 + 편집)</li><li>파일 정보 보기</li><li>새 템플릿 tooExisting 모델을 적용</li></ul> |
| **편집** | 작업 실행 취소/다시 실행, 복사, 붙여넣기 및 삭제 |
| **보기** | <ul><li>**분석** 및 **디자인** 보기 간 전환</li><li>닫힌 창 열기(예 스텐실, 요소 속성 및 메시지)</li><li>레이아웃 toodefault 설정을 다시 설정</li></ul> |
| **다이어그램** | 다이어그램 추가/삭제 및 다이어그램의 "탭"을 통해 이동 |
| **보고서** | 다른 사용자를 사용 하 여 HTML 보고서 tooshare 만들기 |
| **도움말** | 안내선 toohelp hello 도구를 사용 하 여 |

hello 아이콘은 hello 최상위 메뉴에 대 한 바로 가기 키:

| 아이콘                               | 세부 정보      |
| --------------------------------------- | ------------ |
| **열기** | 새 파일 열기 |
| **저장** | 현재 파일 저장 |
| **디자인** | 모델을 만들 수 있는 디자인 보기로 이동 |
| **분석** | 생성된 위협 및 해당 속성 표시 |
| **다이어그램 추가** | 새 다이어그램 (Excel에서 유사한 toonew 탭)를 추가합니다. |
| **다이어그램 삭제** | 현재 다이어그램 삭제 |
| **복사/잘라내기/붙여넣기** | 요소 복사/잘라내기/붙여넣기 |
| **실행 취소/다시 실행** | 작업 실행 취소/다시 실행 |
| **확대/축소** | 아웃 보다 잘 표시에 대 한 hello 다이어그램을 확대합니다. |
| **사용자 의견** | MSDN 포럼 hello를 엽니다. |

### <a name="canvas"></a>캔버스

hello 공간을 끌어서 놓으면 요소입니다. 끌어서 놓기는 가장 빠른 hello와 가장 효율적인 방식으로 toobuild 모델. 또한 마우스 오른쪽 단추로 클릭 하 고 아래와 같이 hello 요소를 사용 하는 제네릭 버전을 추가 하는 hello 메뉴에서 선택 될 수 있습니다.

#### <a name="dropping-hello-stencil-on-hello-canvas"></a>Hello 캔버스에 hello 스텐실을 삭제 하는 중입니다.

![캔버스 삭제](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a>Hello 스텐실 클릭 하면

![요소 속성](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a>스텐실

찾을 수 있는 모든 스텐실이 선택한 hello 템플릿을 기반으로 사용할 수 있는 toouse를 열립니다. Hello 오른쪽 요소를 찾을 수 없으면 다른 서식 파일을 사용 하 여 시도 하거나 하나의 toofit 요구에 맞게 수정 합니다. 일반적으로 아래 hello 것과 같은 범주의 조합 수 toofind 수 있어야 합니다.

| 스텐실 이름                               | 세부 정보      |
| --------------------------------------- | ------------ |
| **프로세스** | 응용 프로그램, 브라우저 플러그 인, 스레드, 가상 컴퓨터 |
| **외부 인자** | 인증 공급자, 브라우저, 사용자, 웹 응용 프로그램 |
| **데이터 저장소** | 캐시, 저장소, 구성 파일, 데이터베이스, 레지스트리 |
| **데이터 흐름** | 이진, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, 명명된 파이프, RPC/DCOM, SMB, UDP |
| **신뢰 선/경계** | 회사 네트워크, 인터넷, 컴퓨터, 샌드박스, 사용자/커널 모드 |

### <a name="notesmessages"></a>참고 사항/메시지

| 구성 요소                               | 세부 정보      |
| --------------------------------------- | ------------ |
| **메시지** | 요소 간 데이터 흐름 없음과 같은 오류가 발생할 때마다 사용자에게 경고하는 내부 도구 논리 |
| **참고 사항** | 엔지니어링 팀에서 수동 메모 추가 toohello 파일 전반적 디자인 hello 및 검토 프로세스 |

### <a name="element-properties"></a>요소 속성

이러한 선택한 hello 요소에 따라 다릅니다. 신뢰 경계 외에도 다른 모든 요소에 일반적인 3가지 선택 항목이 포함되어 있습니다.

| 요소 속성                               | 세부 정보      |
| --------------------------------------- | ------------ |
| **Name** | 프로세스, 저장소, 인자 및 흐름 toobe 쉽게 인식 이름을 지정 하는 데 유용 |
| **범위 외** | Hello 요소 (권장 하지 않음) hello 위협 생성 매트릭스에서 제거 됩니다. 선택한 경우 |
| **범위 외에 대한 이유** | 양쪽 맞춤 필드 toolet 사용자가 알고 이유 때문에 선택 된 범위를 벗어납니다. |

속성은 각 요소 범주 아래에서 변경됩니다. Hello 템플릿 toolearn 더 많은 열 또는 각 요소 tooinspect hello 사용할 수 있는 옵션을 클릭 합니다. Hello 기능으로 살펴보겠습니다.

## <a name="welcome-screen"></a>시작 화면

시작 화면 hello는 hello 앱을 열 때 hello 첫 번째 항목입니다.

### <a name="open-a-model"></a>모델 열기

"모델 열기" 단추를 가리키면 두 개의 숨겨진 옵션 "이 컴퓨터에서 열기" 및 "OneDrive에서 열기"가 표시됩니다. 먼저 hello hello 두 번째 과정을 안내해 hello 로그인 프로세스 OneDrive에 대 한 인증을 거친 후 toopick 폴더와 파일 수 하는 동안 hello 파일 열기 화면을 엽니다.

![모델 열기](./media/azure-security-threat-modeling-tool/openmodel.png)

![컴퓨터 또는 OneDrive에서 열기](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a>피드백, 제안 및 문제

이 옵션을 선택 하면 이동 됩니다 toohello MSDN 포럼 SDL 도구에 대 한. 해결 방법 및 새로운 아이디어를 포함 하는 hello 도구에 대 한 다른 사용자는 말 아웃 위한 훌륭한 방법 toocheck 이며

![사용자 의견](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a>디자인 보기

열거나 새 모델을 만들 때마다 toohello 디자인 보기로 이동 합니다.

### <a name="adding-elements"></a>요소 추가

두 가지 방법이 있습니다 tooadd 요소 hello 그리드에서:

- **끌어서 놓기** – hello 원하는 요소 toohello 그리드를 끌어 온 다음 hello 요소 속성 tooprovide 추가 정보를 사용 합니다.
- **마우스 오른쪽 단추로 클릭** – 마우스 오른쪽 단추로 hello 그리드에서 아무 곳 이나 클릭 하 고 hello 드롭다운 메뉴에서 선택 합니다. 해당 요소에 대 한 일반 표현을 hello 화면에 표시 됩니다.

### <a name="connecting-elements"></a>요소 연결

두 가지 방법이 있습니다 tooconnect 요소 hello 도구에서:

- **끌어서 놓기** – hello 원하는 데이터 흐름 toohello 눈금 끌어서 두 ends toohello 적절 한 요소를 연결 합니다.
- **Shift + 클릭** – hello 첫 번째 요소 (데이터 전송)를 클릭, 키를 누른 hello Shift 키를 그 선택 hello 두 번째 요소 (데이터 수신) 합니다. 마우스 오른쪽 단추로 클릭하고 "연결"을 선택합니다. 양방향 데이터 흐름을 사용 하는 hello 순서가 중요 하지 않습니다.

### <a name="properties"></a>properties

Hello 다이어그램에 배치 하는 hello 스텐실에 수정할 수 있는 모든 hello 속성을 보여 줍니다. hello 스텐실 toosee hello 속성을 클릭 하 고 hello 정보를 그에 따라 정보가 입력 됩니다. 다음 예제에서는 hello 스텐실 hello 다이어그램으로 끌 "Database" 전후 보여 줍니다.

#### <a name="before"></a>이전

![이전](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a>이후

![이후](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a>메시지

위협 모델을 만들고 tooconnect 데이터 흐름 tooelements 잊은 경우 hello 메시지 창 tooact을 알립니다. 또는 다음 tooignore를 선택할 수 있습니다 hello 지침 toofix hello 문제입니다. 

![메시지](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a>참고 사항

메시지 tooNotes에서 탭 간을 전환할 수 있습니다 있습니다 tooadd 노트 tooyour 다이어그램 toocapture 모든 의견을

## <a name="analysis-view"></a>분석 보기

완료 하 고 나면 toohello 상단 메뉴 선택 항목을 이동 하 고 hello 돋보기 다음 toohello 페인트 색상표를 선택 하 여 tooanalysis 보기 전환 다이어그램을 작성 합니다.

![분석 보기](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a>생성된 위협 선택

위협을 클릭하면 세 가지 고유한 기능을 활용할 수 있습니다.

| 기능                               | 정보      |
| --------------------------------------- | ------------ |
| **읽기 표시기** | <p>위협은 hello 항목 이미 진행을 추적할 수를 쉽게 얻을 수 있는 읽은 상태로 표시 됩니다.</p><p>![읽기/읽지 않음 표시기](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| **상호 작용 포커스** | <p>상호 작용 toothat 위협 속하는 hello 다이어그램에 강조 표시</p><p>![상호 작용 포커스](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| **위협 속성** | <p>Hello 위협에 대 한 자세한 내용은 hello 위협 속성 창에 채워집니다.</p><p>![위협 속성](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a>우선 순위 변경

생성 된 각 위협의 hello 우선 순위 수준 변경의 색 toomake 설치 경로도 변경 하기 쉬운 tooidentify 높음, 중간 및 낮음 우선 순위 위협입니다.

![우선 순위 변경](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a>위협 속성 편집 가능한 필드

위의 hello 이미지와 같이 사용자 hello 도구에 의해 생성 된 hello 정보를 변경할 수 있습니다를 근거 등의 정보 toocertain 필드를 추가할 수도 있습니다. 이러한 필드는 hello 템플릿에 의해 생성 되는 것이 좋습니다 toomake 수정 하는 각 위협에 대 한 자세한 정보를 필요 하므로.

![위협 속성](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a>보고서

우선 순위 변경 완료 되 고 각 업데이트 hello 상태 위협 생성 되 면에 hello 파일을 저장 하거나 이동 하 여 너무 "보고서" 다음 "전체 보고서 만들기." 보고서를 출력할 수 있습니다. 만들라는 메시지가 tooname hello 보고서 및 이렇게 할 경우, 다음과 유사한 toohello 이미지 아래 표시 됩니다.

![보고서](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a>다음 단계

toocontribute hello 커뮤니티에 대 한 템플릿을 참조 하십시오. tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  페이지. **[다운로드](https://aka.ms/tmtpreview)**  hello 도구 tooget 오늘 시작 합니다.

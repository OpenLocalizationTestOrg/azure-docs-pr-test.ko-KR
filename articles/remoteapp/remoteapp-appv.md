---
title: "Azure RemoteApp을 사용 하 여 App-v aaaUsing 앱 | Microsoft Docs"
description: "자세한 내용은 방법 Azure RemoteApp에서 toouse App-v 응용 프로그램입니다."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a>Azure RemoteApp에서 App-V 앱 사용
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

Azure RemoteApp 하이브리드 컬렉션에서 App-V 응용 프로그램을 사용할 수 있으며, 이때 도메인에 가입해야 합니다.

시작 하기 전에 hello 최신 업데이트를 사용 하 여 있는지 tooinstall hello App-v 5.1 클라이언트를 확인 합니다. Toocreate 해야는 [사용자 지정 이미지](remoteapp-create-custom-image.md) hello App-v 클라이언트를 포함 하는 합니다.  

쉽게 toouse는 Azure RemoteApp과 함께 기존 App-v 인프라입니다. 하이브리드 컬렉션 액세스 tooyour 도메인 컨트롤러가 있는 Azure VNET에 배포 되 고 hello Vm이 도메인에 가입를 기존 app-v 인프라와 배포 메서드 tooeasyily 호스트 App-v 응용 프로그램에서 Azure RemoteApp을 활용할 수 있습니다. 다음은 수의 현재 App-v 배포의 hello 형식을 기반으로 하는 몇 가지 고려 사항입니다.

| 구성 옵션 |  | Positive | Negative |
| --- | --- | --- | --- |
| 배달 방법 |스트리밍(주문형) |응용 프로그램은 항상 최신 버전과 새 hello |첫 번째 대기 시간 |
| 탑재됨 |가장 빠른; 앱은 이미 hello VM에 |Bloat - 이미지 공간을 차지함(127 GB 한계) | |
| 앱 위치 저장소 |공유 콘텐츠 |앱이 Azure RemoteApp 인스턴스의 메모리에서 실행됨 |Hello 앱이 있는 메모리와 좋은 연결 toostreaming (파일) 서버 무시 |
| 디스크(캐시됨) |고속 실행. 앱이 콘텐츠 원본의 가용성에 의존하지 않음 |Bloat - 이미지 공간을 차지함(127 GB 한계) | |
| 대상 지정 |사용자 |전체 독립 실행형 App-V 인프라가 필요함 | |
| 글로벌(컴퓨터) |게시 서버를 사용하여 미리 게시 또는 대상 지정 |원하는 tooupdate hello 앱 (거 대 한) 경우 tooupdate Azure 이미지를 필요 합니다. 이미지의 일부 공간을 차지합니다. | |

 사용자 지정 이미지 및 하이브리드 컬렉션을 만든 후 응용 프로그램을 게시, 사용자 지정 및 tooany 장치 아무 곳 이나 배달 하는 Azure RemoteApp에서 호스트 하 여 기존 App-v 응용 프로그램을 이용 하세요.


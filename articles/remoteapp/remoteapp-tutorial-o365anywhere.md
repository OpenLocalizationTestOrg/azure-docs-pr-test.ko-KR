---
title: "aaaGet hello Azure RemoteApp과 함께 모든 장치에서 동일한 Office 365 환경 | Microsoft Docs"
description: "자세한 내용은 방법 tooshare Azure RemoteApp을 사용 하 여 사용자와 Office 365 앱."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a>동일한 get hello Azure RemoteApp과 함께 모든 장치에서 제공 되는 Office 365
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

이 문서에서는 설명 하는 방법을 회사의 모든 장치에서 Office 365 toodeploy 합니다. 사용자가 hello 동일한 기능을 가져올 수 있습니다 및 Android, 사과 및 Windows에서 UI 경험 합니다.

이를 위해 사용자가 연결할 수 있는 Azure의 확장 가능한 가상 컴퓨터에서 Office 365를 호스트하여 Azure RemoteApp을 사용하겠습니다. 이 가상 컴퓨터 집합을 "클라우드 컬렉션"이라고 합니다.

## <a name="create-a-cloud-collection"></a>클라우드 컬렉션 만들기
처음 Azure 계정을 만든 후 이동 너무**RemoteApp** hello 왼쪽의 hello 링크를 클릭 하 여 합니다.
![Hello Azure 포털에서 Azure RemoteApp 표시](./media/remoteapp-tutorial-o365anywhere/1-menu.png)

다음을 클릭 하 여 계속 **새** hello 아래쪽과 "빠른 만들기"에 컬렉션입니다. 이름, hello 지역, hello 구독, hello 계획 및 제공 하는 hello 이미지 "Office Proffesional 2013"를 제공 합니다.
![만들기 대화 상자](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)

완료 되 면 hello 양식 hello 컬렉션 생성 프로세스를 시작 해야 합니다. tooan 시간 정도 걸릴 수 있습니다.

![대기](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

Hello 프로세스를 완료 한 후 다음과 같이 표시 됩니다. **게시** 를 클릭하면 대부분의 Office 응용 프로그램이 이미 게시되어 있음을 볼 수 있습니다.
![만들어진 컬렉션](./media/remoteapp-tutorial-o365anywhere/4-done.png)

![게시된 앱](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

이 시점에서 추가할 수도 있습니다를 클릭 하 여 액세스 toothis 컬렉션에 있는 더 많은 사용자가 **사용자 액세스**합니다.
![사용자 액세스 구성](./media/remoteapp-tutorial-o365anywhere/6-user.png)

이제 tooOffice 365 연결 시험해 보겠습니다!

## <a name="connect-toooffice-365"></a>TooOffice 365 연결
통해 너무 head 합니다 म[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), 아래로 스크롤하여 클릭 **클라이언트를 다운로드할** 하 고 hello 장치의 tooinstall hello Azure RemoteApp 클라이언트입니다. Windows hello 스크린 샷을 아래 됩니다.

Hello 응용 프로그램 시작 되 면 만들라는 메시지가 toosign Microsoft 계정 (이전의 "Live ID")으로, 사용 하 여 hello 지금은 동일한 Azure 계정. 로그인하면 새 초대에 대한 알림이 표시됩니다. 알림을 클릭하면 아래와 같은 목록이 표시됩니다. Azure 계정 소유자 전자 메일을 일치 하는 hello 초대를 수락 합니다.

![새 초대](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

새 초대가 있는 경우의 모양

![응용 프로그램 수락](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

Hello 초대를 수락 되 면 모든 hello Office 앱 hello Azure RemoteApp 클라이언트에 표시 되어야 합니다.

![앱 목록](./media/remoteapp-tutorial-o365anywhere/9-work.png)

이러한 hello 응용 프로그램 중 하나를 클릭 해야 hello에 Azure 가상 컴퓨터를 시작 하 고 모두 설정 해야 합니다.! 마음껏 즐기세요!

![시작 중](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)


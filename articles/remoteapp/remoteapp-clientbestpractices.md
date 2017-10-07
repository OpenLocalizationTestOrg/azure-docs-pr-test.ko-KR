---
title: "Azure RemoteApp 클라이언트에 대 한 aaaBest 사례 | Microsoft Docs"
description: "Hello RemoteApp 클라이언트를 사용 하기 위한 모범 사례에 알아보기"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 8c2e6068-8733-42f6-a05c-a2088634991b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: aa0ccb2f51d381462b78d60e966b87a67d8c247e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-remoteapp-clients"></a>Azure RemoteApp 클라이언트 모범 사례
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

다음 정보는 hello Azure RemoteApp 클라이언트를 사용할 수 있습니다.

* 항상 최신 클라이언트 hello를 사용 합니다. 이렇게 하면 해당 hello를 사용 중인 클라이언트 버전에는 hello 최신 버그 수정, 개선 사항 및 기능입니다. 해야 tooautomatically toosign hello 적절 한 저장소에 클라이언트 hello에 대 한 업데이트를 수신 합니다.
* 일정 기간 동안 비활성 상태이면 RemoteApp에서 자동으로 로그오프됩니다. 순서 tooprevent 데이터 손실, hello 서비스 사용을 마칠 때 응용 프로그램을 닫는 것이 좋습니다.


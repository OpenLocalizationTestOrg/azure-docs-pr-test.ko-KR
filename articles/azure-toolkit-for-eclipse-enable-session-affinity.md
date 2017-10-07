---
title: "Eclipse 용 Azure 도구 키트 hello aaaEnable 세션 선호도 사용 하 여"
description: "어떻게 Eclipse 용 Azure 도구 키트를 사용 하 여 tooenable 세션 선호도 hello에 대해 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a>세션 선호도 사용
Hello Azure Toolkit for Eclipse 내에서 "고정 세션", 역할 또는 HTTP 세션 선호도 설정할 수 있습니다. hello 다음 그림에 나와 hello **부하 분산** 속성 대화 상자 사용 tooenable hello 세션 선호도 기능:

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a>사용자의 역할에 대 한 tooenable 세션 선호도
1. Eclipse의 프로젝트 탐색기에서 hello 역할을 마우스 오른쪽 단추로 클릭 합니다. **Azure**, 클릭 하 고 **부하 분산**합니다.

2. Hello에 **WorkerRole1 부하 분산에 대 한 속성** 대화 상자:

   a. **Enable HTTP session affinity (sticky sessions) for this role**

   b. 에 대 한 **입력 끝점 toouse**, 예를 들어 한 입력된 끝점 toouse 선택 **http (공용: 80, 개인: 8080)**합니다. 응용 프로그램은 이 끝점을 해당 HTTP 끝점으로 사용해야 합니다. 사용자의 역할에 대 한 여러 끝점을 설정할 수 있지만 둘 중 하나만 toosupport를 선택할 수 있습니다 고정 세션입니다.

   c. 응용 프로그램을 다시 빌드합니다.

특정 클라이언트에서 발생 하는 HTTP 요청에서 처리 하 고 hello 동일 계속 사용할 수 있는 경우 역할 인스턴스가 둘 이상 있는 경우, 역할 인스턴스.

hello Eclipse 도구 키트에 각 역할 인스턴스에 요청 라우팅 ARR (응용 프로그램)를 호출 하는 특수 한 IIS 모듈을 설치 하 여 사용 하도록 설정 합니다. ARR에 HTTP 요청 toohello 적절 한 역할 인스턴스로 다시 라우팅합니다. hello 도구 키트는 hello 들어오는 HTTP 트래픽이 않도록 첫 번째 라우트된 toohello ARR 소프트웨어로 hello 선택한 끝점을 자동으로 재구성 합니다. 또한 hello toolkit Java 서버를 구성 된 toolisten 되는 새 내부 끝점을 만듭니다. ARR tooreroute hello HTTP 트래픽 toohello 적절 한 역할 인스턴스에 사용 되는 hello 끝점입니다. 이 방법으로 다중 인스턴스 배포의 각 역할 인스턴스는 모두에 대 한 역방향 프록시 hello 다른 경우 고정 세션을 사용 하도록 설정 됩니다.

## <a name="notes-about-session-affinity"></a>세션 선호도 관련 참고 사항
* 세션 선호도 hello 계산 에뮬레이터에서 작동 하지 않습니다. hello 설정을 hello 계산 에뮬레이터에서 빌드 프로세스를 방해 하지 않고 적용 하거나 계산 에뮬레이터 실행 하지만 자체 hello 기능은 hello 계산 에뮬레이터 내에서 작동 하지 않습니다.

* 세션 선호도 사용 하도록 설정 hello 추가 소프트웨어 다운로드 되 고 hello Azure 클라우드 서비스를 시작할 때 사용할 역할 인스턴스에 설치 하는 대로 azure에서 배포에서 사용할 디스크 공간에에서 증가 됩니다.

* hello 시간 tooinitialize 각 역할 더 오래 걸립니다.

* 내부 끝점으로, 위에서 설명한 것 처럼 트래픽 rerouter toofunction 추가 됩니다.


## <a name="see-also"></a>참고 항목
[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]

[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]

[Hello Eclipse 용 Azure 도구 키트 설치][Installing hello Azure Toolkit for Eclipse] 

Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터][Azure Java Developer Center]합니다.

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->

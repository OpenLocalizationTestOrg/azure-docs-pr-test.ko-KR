---
title: "Eclipse용 Azure 도구 키트를 사용하여 세션 선호도 사용"
description: "Eclipse용 Azure 도구 키트를 사용하여 세션 선호도를 사용 설정하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: ab8623d6f9751ed6d71d9a5b1c0d5e939c442862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-session-affinity"></a>세션 선호도 사용
Eclipse용 Azure 도구 키트 내에서 역할에 대해 HTTP 세션 선호도 또는 "고정 세션"을 사용하도록 설정할 수 있습니다. 다음 이미지는 세션 선호도 기능을 사용하도록 설정하는 데 사용되는 **부하 분산** 속성 대화 상자를 보여 줍니다.

![][ic719492]

## <a name="to-enable-session-affinity-for-your-role"></a>역할에 대한 세션 선호도를 사용하도록 설정하려면
1. Eclipse의 프로젝트 탐색기에서 역할을 마우스 오른쪽 단추로 클릭하고 **Azure**를 클릭한 다음 **부하 분산**을 클릭합니다.

2. **WorkerRole1 속성 부하 분산** 대화 상자에서:

   a. **Enable HTTP session affinity (sticky sessions) for this role**

   b. **사용할 입력 끝점**의 경우 **http (public:80, private:8080)**와 같이 사용할 입력 끝점을 선택합니다. 응용 프로그램은 이 끝점을 해당 HTTP 끝점으로 사용해야 합니다. 사용자의 역할에 대해 여러 끝점을 사용하도록 설정할 수 있지만 그중 하나만 선택하여 고정 세션을 지원할 수 있습니다.

   c. 응용 프로그램을 다시 빌드합니다.

사용하도록 설정하면 역할 인스턴스가 둘 이상 있는 경우 특정 클라이언트에서 발생하는 HTTP 요청이 동일한 역할 인스턴스에 의해 계속 처리됩니다.

Eclipse 도구 키트는 각 역할 인스턴스에 ARR(응용 프로그램 요청 라우팅)이라는 특별한 IIS 모듈을 설치하여 이를 사용하도록 설정합니다. ARR은 적절한 역할 인스턴스로 HTTP 요청의 경로를 전환합니다. 도구 키트는 들어오는 HTTP 트래픽이 먼저 ARR 소프트웨어로 경로 지정되도록 선택한 끝점을 자동으로 재구성합니다. 또한 도구 키트는 Java 서버가 수신 대기하도록 구성되는 새 내부 끝점을 만듭니다. 이는 적절한 역할 인스턴스로 HTTP 트래픽의 경로를 전환하도록 ARR에서 사용하는 끝점입니다. 이 방법으로 다중 인스턴스 배포의 각 역할 인스턴스는 다른 모든 인스턴스에 대한 역방향 프록시 역할을 수행하여 고정 세션을 사용하도록 합니다.

## <a name="notes-about-session-affinity"></a>세션 선호도 관련 참고 사항
* 세션 선호도는 계산 에뮬레이터에서 작동하지 않습니다. 빌드 프로세스 또는 계산 에뮬레이터 실행을 방해하지 않고 계산 에뮬레이터에서 설정을 적용할 수 있지만 기능 자체는 계산 에뮬레이터 내에서 작동하지 않습니다.

* 세션 선호도를 사용하도록 설정하면 Azure 클라우드에서 서비스를 시작할 때 추가 소프트웨어가 역할 인스턴스에 다운로드되어 설치되므로 Azure에서 배포에 사용되는 디스크 공간이 증가합니다.

* 각 역할을 초기화하는 시간이 오래 걸립니다.

* 위에서 언급한 트래픽 경로 전환기로 작동하는 내부 끝점이 추가됩니다.


## <a name="see-also"></a>참고 항목
[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]

[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]

[Eclipse용 Azure 도구 키트 설치][Installing the Azure Toolkit for Eclipse] 

Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터][Azure Java Developer Center]를 참조하세요.

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How to Maintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->

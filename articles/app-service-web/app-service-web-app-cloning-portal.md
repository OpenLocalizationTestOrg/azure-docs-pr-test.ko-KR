---
title: "Azure 포털을 사용 하 여 응용 프로그램 복제 aaaWeb"
description: "자세한 내용은 어떻게 tooclone 웹 응용 프로그램을 Azure 포털을 사용 하 여 웹 앱 toonew 합니다."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a>Azure 포털을 사용하여 Azure 앱 서비스 앱 복제
복제 기능에서 hello [Azure 앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714) 기존 웹 응용 프로그램 새로 만든 tooa 앱 또는 다른 지역에 쉽게 복제할 수 있습니다. 동일한 지역 hello 합니다. 이렇게 쉽고 신속 하 게 서로 다른 지역의 여러 고객 toodeploy 수의 앱 활성화 됩니다.

앱 복제는 현재 프리미엄 계층의 앱 서비스 계획에만 지원됩니다. 새 기능 사용 hello hello 동일한 웹 앱 백업 기능으로, 제한 사항 참조 [Azure 앱 서비스의 웹 앱 백업](web-sites-backup.md)합니다.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a>기존 앱 복제
hello에서 hello 웹 응용 프로그램을 실행 해야 **프리미엄** toocreate hello 웹 앱에 대 한 복제본을 위해에서 모드입니다.

1. Hello에 [Azure 포털](https://portal.azure.com/), 웹 앱 블레이드를 엽니다.
2. **도구**를 클릭합니다. 그런 다음, hello **도구** 블레이드에서 클릭 **복제 앱**합니다.
   
    ![][1]
   
   > [!NOTE]
   > Hello 웹 앱에에서 없는 경우 이미 hello **프리미엄** 모드를 나타내는 응용 프로그램 복제에 대 한 지원 hello 모드는 메시지가 표시 됩니다. 이 시점에서 hello 옵션 tooselect를 있는 **업그레이드**합니다.
   > 
   > 
3. Hello에 **복제 앱** 블레이드 hello 새 웹 앱, 리소스 그룹 및 앱 서비스 계획의 이름을 제공 합니다. 또한 hello 사용자 됩니다 수 toochoose 여부 tooclone 다양 한 소스 웹 응용 프로그램 설정 여부입니다.
   
    ![][2]
4. 클릭 한 후 **만들** hello 플랫폼 hello 소스 웹 응용 프로그램의 복제본을 만드는 방법에 대 한 작업을 시작 합니다.

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>기존 앱 tooan 앱 서비스 환경 복제
Hello에 **복제 앱** 블레이드 hello 고객 hello 옵션 toochoose 기존 앱 서비스 환경에 응용 프로그램 풀 있어야 합니다.

## <a name="current-restrictions"></a>현재 제한 사항
이 기능은 현재 미리 보기, 시간이 지남에 따라 tooadd 새로운 기능을 노력 하 고, hello 목록 다음에 Azure 포털에서 응용 프로그램 복제 hello 현재 지원에 대 한 알려진된 제한 hello 됩니다.

* Azure 트래픽 관리자 설정은 복제되지 않습니다.
* 자동 크기 설정은 복제되지 않습니다.
* 백업 일정 설정은 복제되지 않습니다.
* VNET 설정은 복제되지 않습니다.
* App Insights 설정 되지 않는 자동으로 hello 대상 웹 응용 프로그램
* 간편한 인증 설정은 복제되지 않습니다.
* Kudu 확장은 복제되지 않습니다.
* TiP 규칙은 복제되지 않습니다.
* 데이터베이스 내용이 복제되지 않습니다.

### <a name="references"></a>참조
* [PowerShell을 사용하여 웹앱 복제](app-service-web-app-cloning.md)
* [Azure 앱 서비스에서 웹앱 백업](web-sites-backup.md)
* [어떻게 tooCreate 앱 서비스 환경](app-service-web-how-to-create-an-app-service-environment.md)
* [App Service 환경에서 웹앱 만들기](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [소개 tooApp 서비스 환경](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png

---
title: "Visual Studio에서 연결 된 서비스를 사용 하 여 모바일 서비스 aaaAdding | Microsoft Docs"
description: "Hello Visual Studio 연결 된 서비스 추가 대화 상자를 사용 하 여 모바일 서비스 추가"
services: visual-studio-online
documentationcenter: na
author: mlhoop
manager: douge
editor: 
ms.assetid: 75c3cb93-88e1-476d-a416-f34caa3608e3
ms.service: visual-studio-online
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: mobile
ms.date: 12/16/2015
ms.author: mlearned
ms.openlocfilehash: c47b6fb63dc99fbc012e1c627c6c7e95249de7a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a>Visual Studio 연결된 서비스를 사용하여 모바일 서비스 추가
Visual Studio 2015와 함께 hello를 사용 하 여 tooAzure 모바일 서비스를 연결할 수 있습니다 **연결 된 서비스 추가** 대화 상자. 모든 C# 클라이언트 앱, JavaScript 앱 또는 크로스 플랫폼 Cordova 앱에서 연결할 수 있습니다. 연결되면 데이터를 만들고 액세스하고, 사용자 지정 API 및 예약된 작업을 만들거나 푸시 알림에 대한 지원을 추가합니다.  hello 연결 된 서비스 작업을 추가 하는 모든 적절 한 참조와 연결 코드입니다. Azure AD, Facebook, Twitter 및 Microsoft 계정과 같이 여러 인기 있는 ID 스키마로 인증용 기본 제공 지원을 활용할 수도 있습니다.

## <a name="supported-project-types"></a>지원되는 프로젝트 형식
> [!NOTE]
> Visual Studio 2015의 hello 연결 된 서비스 추가 대화 상자를 사용 하 여 Azure 모바일 서비스 tooa Windows 유니버설 (Windows 10) 프로젝트를 추가 지원 되지 않습니다. Hello NuGet 패키지 관리자를 사용 하 여 프로젝트에 대 한 hello 적절 한 패키지를 설치 하 여 Azure 모바일 서비스를 추가할 수 있습니다.
> 
> 

프로젝트 형식에 따라 hello에 hello 연결 된 서비스 대화 tooconnect tooAzure 모바일 서비스를 사용할 수 있습니다.

* .NET Windows 8.1 Store, Phone 및 Universal 앱 프로젝트
* JavaScript Windows 8.1 Store, Phone 및 Universal 앱 프로젝트
* Apache Cordova용 Visual Studio Tools를 사용하여 만든 프로젝트

## <a name="connect-tooazure-mobile-services-using-hello-add-connected-services-dialog"></a>Hello 연결 된 서비스 추가 대화 상자를 사용 하 여 tooAzure 모바일 서비스를 연결 합니다.
1. Azure 계정이 있어야 합니다. Azure 계정이 없으면 [무료 평가판](http://go.microsoft.com/fwlink/?LinkId=518146)에 등록할 수 있습니다.
2. 열기 hello **연결 된 서비스 추가** 대화 상자.
   
   * .NET 응용 프로그램에 대 한 hello에 대 한 상황에 맞는 메뉴를 열고 hello Visual Studio에서 프로젝트를 열고 **참조** 솔루션 탐색기에서 노드를 선택한 후 **연결 된 서비스 추가**
     
        ![TooAzure 모바일 서비스를 연결합니다.](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * Apache Cordova 앱 프로젝트에 대 한 Visual Studio 솔루션 탐색기에서 프로젝트 노드 hello open hello 상황에 맞는 메뉴에서에서 프로젝트를 열고 **연결 된 서비스 추가**합니다.
3. Hello에 **연결 된 서비스 추가** 대화 상자에서 선택 **Azure 모바일 서비스**, hello 선택 **구성** 단추입니다. 아직 수행 하지 않은 경우에 Azure에 증명된 toolog을 수 있습니다.
   
    ![Azure 모바일 서비스 추가](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. Hello에 **Azure 모바일 서비스** 대화 상자에서 있는 경우 기존 모바일 서비스를 선택 합니다. Toocreate 새 Azure 모바일 서비스를 필요 하므로 toodo 아래 hello 절차를 따릅니다. 그렇지 않은 경우 toohello 다음 단계를 건너뜁니다.
   
    새 모바일 서비스 계정 toocreate:
   
   1. hello 선택 * * 서비스 만들기 * * hello hello 대화 상자의 맨 아래에 링크 합니다.
       ![새 모바일 연결된 서비스 추가](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)
   2. Hello에 **모바일 서비스 만들기** 대화 상자에서에서 선택할 수 있습니다 JavaScript 백 엔드 모바일 서비스 또는.NET 백 엔드 모바일 서비스 hello **런타임** 드롭 다운 목록입니다. 
      
       ![모바일 서비스 만들기](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)
      
       JavaScript 백 엔드 서비스는 단순하면서도 강력합니다. JavaScript 백 엔드 모바일 서비스를 만들면 hello 서버 쪽 JavaScript 코드가 hello 클라우드에 저장 되지만 서버 탐색기 또는 hello Azure 관리 포털을 사용 하 여 서버 스크립트를 편집할 수 있습니다. 
      
       .NET 백 엔드 모바일 서비스는 hello 완전 하 고 Web API 및 Entity Framework의 유연성을 제공합니다. .NET 백 엔드 모바일 서비스를 만드는 경우 프로젝트를 자동으로 만들어집니다 및 tooyour 솔루션을 추가 합니다. 
   3. Hello 선택 **지역** hello 모바일 서비스와 서버 hello에 대 한 사용자 이름 및 암호를 입력 합니다.
   4. 모든 hello 필요한 정보를 입력 한 후 선택 hello **만들기** toocreate hello 모바일 서비스 단추입니다.
   5. hello 새 모바일 서비스는 hello에 hello 서비스 목록에 표시 되어야 **Azure 모바일 서비스** 대화 상자. 새 모바일 서비스 hello hello 목록에서 선택 하 고 hello 선택 **추가** 단추 tooadd hello 서비스 tooyour 프로젝트.
5. 검토 hello 시작 페이지를 표시 하 고 프로젝트를 수정 하는 방법을 알아봅니다. 연결된 서비스를 추가할 때마다 시작 페이지가 브라우저에 나타납니다. 검토할 수 있습니다 다음 제안 된 단계 및 코드 예제를 보려면 hello 또는 어떤 참조가 tooyour 프로젝트에 추가 되었습니다 및 코드 및 구성 파일이 수정 방법을 toohello 무슨 상황이 페이지 toosee를 전환 합니다.
6. Hello 코드 샘플을 사용 하 여 지침으로, 코드 tooaccess 모바일 서비스를 작성 하는 작업을 시작!

## <a name="how-your-project-is-modified"></a>프로젝트를 수정하는 방법
Visual Studio에서 프로젝트를 수정 하는 방법 hello 프로젝트 형식에 따라 달라 집니다. C# 클라이언트 앱의 경우 [변경된 내용 – C# 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=513119)를 참조하세요. JavaScript 클라이언트 앱의 경우 [변경된 내용 – JavaScript 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=513120)를 참조하세요. Cordova 앱의 경우 [변경된 내용 – Cordova 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=513116)를 참조하세요.

## <a name="next-steps"></a>다음 단계
질문하고 도움 받기: 

* [MSDN 포럼: Azure 모바일 서비스](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [Microsoft Azure 팀 블로그 hello에 azure 모바일 서비스](https://azure.microsoft.com/blog/topics/mobile/)
* [azure.microsoft.com의 Azure 모바일 서비스](https://azure.microsoft.com/services/mobile-services/)
* [azure.microsoft.com의 Azure 모바일 서비스 설명서](https://azure.microsoft.com/documentation/services/mobile-services/)


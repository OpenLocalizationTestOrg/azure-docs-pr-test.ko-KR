---
title: "SDK for.NET 2.5.1 aaaAzure 릴리스 정보"
description: "Azure SDK for .NET 2.5.1 릴리스 정보"
services: app-service
documentationcenter: .net,nodejs,java
author: Juliako
manager: erikre
editor: 
ms.assetid: 8d3d815f-bb58-447e-8ff0-f9b9603c7b00
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/10/2016
ms.author: juliako
ms.openlocfilehash: 5ee7688617c966baa409045881c172bbbc55ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-251-release-notes"></a>Azure SDK for .NET 2.5.1 릴리스 정보
이 문서는.NET 2.5.1 해제에 대 한 hello hello Azure SDK 릴리스 정보를 포함 합니다. 

## <a name="azure-sdk-for-net-251-release-notes"></a>Azure SDK for .NET 2.5.1 릴리스 정보
hello 다음 새로운 기능 및 hello Azure SDK for.NET 2.5.1에서에서 업데이트 됩니다.

* 새 기능 \ 시나리오 관련 너무**웹 도구 확장**합니다. 
  
  * Azure 웹 사이트에서 이름이 바뀐된 tooAzure 앱 서비스입니다. 자세한 내용은 [Azure 앱 서비스 및 기존 Azure 서비스](../app-service-web/app-service-changes-existing-services.md)를 참조하세요.
  * 고객 API 앱으로 ASP.NET 프로젝트를 게시 하 고 다음 추가 hello를 사용 하 여 수 있도록 azure API 앱 (미리 보기) 지원이 추가 되었습니다 > Azure API 앱 클라이언트 제스처의 hello hello 구조를 기반으로 C# 프로젝트 toogenerate 코드에서 API 앱을 배포 합니다. 
  * 서버 탐색기에서 웹 사이트 노드 hello 되지 않습니다 그룹 기반 그룹화 Azure API 앱, 모바일 앱 및 웹 응용 프로그램의 리소스에 대 한 지원을 포함 하는 hello Azure 앱 서비스 노드가 대신이 대화 상자.
  * 모바일 앱 컨트롤러를 추가할 고객 새 모바일 앱 프로젝트를 만들 수 있도록 azure 모바일 앱 (미리 보기) 지원이 추가 되었습니다, hello 프로젝트를 게시 및 응용 프로그램을 원격으로 디버깅 합니다.
  * 추가 > Azure API 앱 클라이언트 제스처에는 이제 로컬 JSON Swagger 파일 지원, Swashbuckle toogenerate와 같은 타사 NuGets Swagger 또는 수동으로 작성 개발자가 웹 API를 사용할 수 있도록 합니다. 이러한 방식으로 클라이언트 개발자가 사용할 수 hello 코드 생성 기능 tooconsume 모든 Swagger 끝점 C# 프로젝트에서. 
  * 웹 앱 및 API 앱 게시 대화 상자에 그룹화 하는 리소스의 향상 된 toosupport hello Azure 포털 개념 하 고 Azure 리소스 그룹 및 앱 서비스 계획의 선택/생성 된 hello 새 웹 앱 및 API 앱 프로 비전 대화 상자에 표시 됩니다. 
  * Azure API 앱 서버 탐색기 노드 링크 toohello 로그 스트리밍 및 원격 디버깅과 같은 다른 기능 뿐만 아니라 hello Azure 포털에서 API 앱 딥 링크를 제공 합니다.
    
    Azure SDK .NET 2.5.1의 알려진 문제와 현재 제한은 아래의 [이](app-service-release-notes.md#known_issues_2_5_1) 섹션을 참조하세요.
* 새 기능 \ 시나리오 관련 너무**HDInsight 도구** Visual Studio에서이 릴리스의 활성화 됩니다. 
  
  * 하이브 스크립트의 로컬 유효성 검사. 스크립트에 오류가 경우 hello 도구 모음 toosee hello 유효성 검사 스크립트 단추를 클릭 합니다. 
  * 향상된 하이브 작업 디버그. 이제 Visual Studio에서 Yarn 로그에 액세스하여 하이브 작업을 디버그할 수 있습니다. 응용 프로그램에 성능 문제가 있는 경우 YARN 로그를 조사하면 유용한 정보가 제공됩니다.
  * (공개 미리 보기) 하이브에 대한 키워드 자동 완성 및 IntelliSense 지원. Visual Studio 용 HDInsight 도구 하이브 스크립트를 작성 하는 toohelp 키워드 자동 완성 및 Hive에 대 한 IntelliSense 지원을 추가.
  * Storm 지원. 이제 Visual Studio toodevelop 스톰 토폴로지/Spouts/볼트 C#에 대 한 HDInsight 도구를 사용할 수 있습니다. 그런 다음 hello 토폴로지 tooa Storm 클러스터를 개발 하 고 hello 배출구 볼트/토폴로지/상태 참조를 제출할 수 있습니다. 시스템 로그를 사용할 수 있습니다 및 고객 프로그램 스톰 토폴로지/볼트/Spouts tootroubleshoot를 기록 합니다. 또한 HDInsight의 Storm에서 기존 JAVA 자산을 사용할 수 있습니다.
    
    자세한 내용은 [Visual Studio용 HDInsight Hadoop 도구 사용 시작](../hdinsight/hdinsight-hadoop-visual-studio-tools-get-started.md)을 참조하세요.

## <a id="known_issues_2_5_1"></a>Azure SDK for .NET 2.5.1 알려진 문제 및 제한
* Azure API 앱은 모바일 앱의 배포 대상으로 표시됩니다. 웹 앱 이후 릴리스까지 hello 모바일 앱에 대 한 유일한 대상 이어야 합니다. 
* Azure API 앱을 프로 비전 성공 하지만 hello Azure 앱 서비스 활동 창에서 실패 tooupdate hello 진행률 간헐적으로 발생할 수 있습니다. 해결 방법에는 hello Azure 포털에서에서 hello 새 Azure API 앱의 toocheck 상태입니다. 
* default/index.html이 없으므로 파일 > 새 프로젝트 > API 앱 > F5 키를 클릭하면 HTTP 오류가 발생합니다. 해결 방법 toomanually 찾아보기 toohello/api/값 URL입니다. 
* 서버 탐색기 아이콘이 평면으로 표시되는 경우가 가끔 있습니다. VS를 다시 시작하면 이 문제가 해결됩니다. 
* 웹 앱 또는 API 앱 (예: 할당량을 초과 했습니다 오류 또는 중복 Azure API 앱 게이트웨이 이름) 프로 비전 하는 동안 예외가 throw 되 면 hello 오류 일부 원시 JSON 텍스트를 표시 합니다. 
* 프로젝트를 만드는 과정에서 Application Insights를 확인할 때 프로젝트 생성 문제가 가끔 발생합니다.
* 경우에 따라 생성 된 hello Azure API 앱 클라이언트 코드가 없는 네임 스페이스, 사용자가 수동으로 포함 toobe (또는 Visual Studio 신호를 통해 자동으로 가져온) toocompile 코드에 대 한 합니다. 
* 모바일 앱 프로젝트 게시 tooweb 앱 수도 있지만 모바일 앱 프로젝트는 데이터베이스에 필요 하므로 사용자가 만든 hello Azure 포털에서에서 모바일 응용 프로그램으로 사이트를 선택 해야 합니다. 
* 모바일 앱에 대 한 hello 시작 페이지 "모바일 앱"이 아니라 "모바일 서비스" hello 라는 용어를 사용 하 여 
* 모바일 앱 프로젝트를 만드는 tooa 분 toocreate를 차지할 수 있습니다. 
* API 앱 중 오류 (경우에 따라) 프로 비전에서 돌아올 hello Azure API를 반영 하는 hello 사용 권한을 설정할 수 없습니다 제대로 hello API 앱 제대로 프로 비전 이며 사용 하기 위해 준비 하는 동안 합니다. 수동으로 hello Azure 포털을 사용 하 여 권한을 설정할 수 있습니다.
* API 앱 템플릿과 모바일 앱 템플릿에서 Application Insights가 지원되지 않습니다.
* API 앱 프로젝트를 클라우드 서비스 프로젝트와 함께 사용할 수 없습니다.
* API 앱 프로젝트 템플릿은 C#에서만 사용할 수 있습니다.
* API 앱 소비 hello "Azure API 앱 클라이언트 추가" 상황에 맞는 메뉴를 통해 C#만 지원 됩니다.


---
title: "명령줄 도구와 함께 Azure 응용 프로그램의 배포 aaaAutomate | Microsoft Docs"
description: "Hello 명령줄에서 Azure 응용 프로그램을 배포 하는 방법을 대 한 정보를 검색 합니다."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 8b65980c-eb75-44a2-8e0f-f9eb9e617d16
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: 3df66cc4bf4e6819ed0eee7278ac79dca2e5daa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-deployment-of-your-azure-app-with-command-line-tools"></a>명령줄 도구를 사용하여 Azure 앱 배포 자동화
명령줄 도구를 사용하여 Azure 앱 배포를 자동화할 수 있습니다. 이 문서에서는 사용할 수 있는 도구 및 방법을 보여 주는 유용한 링크를 hello 나열 toouse 배포 워크플로에서 해당 합니다. 

## <a name="msbuild"></a>MSBuild를 사용하여 배포 자동화
Hello를 사용 하는 경우 [Visual Studio IDE](#vs) 개발 작업에 사용할 수 있습니다 [MSBuild](http://msbuildbook.com/) tooautomate 아무 것도 IDE에서 수행할 수 있습니다. MSBuild toouse 하거나 구성할 수 있습니다 [웹 배포](#webdeploy) 또는 [FTP/FTPS](#ftp) toocopy 파일입니다. 웹 배포는 데이터베이스 배포와 같은 다른 많은 배포 관련 작업을 자동화할 수도 있습니다.

MSBuild를 사용 하 여 명령줄 배포에 대 한 자세한 내용은 hello 다음 리소스를 참조 하세요.

* [Visual Studio를 사용한 ASP.NET 웹 배포: 명령줄 배포](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment)MSBuild는 Visual Studio에서 사용되는 빌드 엔진입니다. 일련의 Visual Studio를 사용 하 여 배포 tooAzure에 대 한 자습서의 1/10입니다. Visual Studio에서 게시 프로필을 설정한 후 toouse 명령줄 toodeploy hello 하는 방법을 보여 줍니다.
* [내부 hello Microsoft Build Engine: MSBuild를 사용 하 여 및 Team Foundation Build](http://msbuildbook.com/)합니다. 하드 카피 책 장 방법에 포함 된 배포에 대 한 MSBuild toouse 합니다.

## <a name="powershell"></a>Windows PowerShell을 사용하여 배포 자동화
[Windows PowerShell](http://msdn.microsoft.com/library/dd835506.aspx)(영문)에서 MSBuild 또는 FTP 배포 기능을 수행할 수 있습니다. 이렇게 하면 컬렉션 hello Azure REST 관리 API 쉽게 toocall 수행 하는 Windows PowerShell cmdlet 사용할 수도 있습니다.

자세한 내용은 다음 리소스는 hello 참조:

* [웹 응용 프로그램 연결 tooa GitHub 리포지토리를 배포 합니다.](app-service-web-arm-from-github-provision.md)
* [SQL 데이터베이스를 사용하는 웹앱을 프로비전](app-service-web-arm-with-sql-database-provision.md)
* [Azure에서 마이크로 서비스를 예측 가능하게 프로비전 및 배포](app-service-deploy-complex-application-predictably.md)
* [Azure에서 실제 클라우드 앱 빌드 - 자동화](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything)(영문). Hello 전자책에 표시 된 hello 예제 응용 프로그램에서 Windows PowerShell 스크립트 toocreate Azure를 사용 하는 방법을 설명 하는 전자 문서 장 환경을 테스트 하 고 tooit를 배포 합니다. Hello 참조 [리소스](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything#resources) 링크 tooadditional Azure PowerShell 설명서에 대 한 섹션.
* [Windows PowerShell 스크립트 tooPublish tooDev 및 테스트 환경을 사용 하 여](../vs-azure-tools-publishing-using-powershell-scripts.md)합니다. Toouse Windows PowerShell 배포 스크립트에 Visual Studio 방법를 생성 합니다.

## <a name="api"></a>.NET 관리 API를 사용하여 배포 자동화
배포에 대 한 tooperform MSBuild 또는 FTP 함수는 C# 코드를 작성할 수 있습니다. 이렇게 하면 hello Azure 관리 REST API tooperform 사이트 관리 기능에 액세스할 수 있습니다.

자세한 내용은 다음 리소스는 hello 참조:

* [Hello Azure 관리 라이브러리 및.NET을 사용 하 여 모든 것 자동화](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)합니다. 소개 toohello.NET 관리 API 및 링크 toomore 설명서입니다.

## <a name="cli"></a>Azure CLI(Azure 명령줄 인터페이스)에서 배포
FTP를 사용 하 여 Windows, Mac 또는 Linux 컴퓨터 toodeploy의 hello 명령줄을 사용할 수 있습니다. 이렇게 하면 hello Azure CLI를 사용 하 여 hello Azure REST 관리 API에 액세스할 수도 있습니다.

자세한 내용은 다음 리소스는 hello 참조:

* [Azure 명령줄 도구](https://azure.microsoft.com/downloads/). Azure.com에서 명령줄 도구 정보를 제공하는 포털 페이지입니다.

## <a name="webdeploy"></a>웹 배포 명령줄에서 배포
[웹 배포](http://www.iis.net/downloads/microsoft/web-deploy) 배포 tooIIS 뿐만 아니라 지능형 파일을 제공 하는 기능을 동기화 하지만 또한 또는 수행할 수 많은 다른 배포 관련 작업 FTP를 사용 하는 경우에 자동화할 수 없는 조정에 대 한 Microsoft 소프트웨어 됩니다. 예를 들어 웹 배포는 웹 앱과 함께 새 데이터베이스나 데이터베이스 업데이트를 배포할 수 있습니다. 또한 웹 배포는 이후 변경 된 파일만 복사할 지능적으로 hello 필요한 시간 tooupdate 기존 사이트를 최소화할 수 있습니다. Microsoft Visual Studio와 Team Foundation Server에서는 기본 제공 웹 배포에 대 한 지원 하지만 hello 명령줄 tooautomate 배포에서 직접 웹 배포를 사용할 수도 있습니다. 웹 배포 명령은 매우 강력한 있지만 hello 배워야 할 필요성이 빠르게 습득할 수 있습니다.

## <a name="more-resources"></a>추가 리소스
다른 배포 옵션 toocommand 줄 자동화는 toouse 클라우드 기반 서비스와 같은 [여러 분기 배포](http://en.wikipedia.org/wiki/Octopus_Deploy)합니다. 자세한 내용은 참조 [웹 사이트를 배포 하는 ASP.NET 응용 프로그램 tooAzure](https://octopusdeploy.com/blog/deploy-aspnet-applications-to-azure-websites)합니다.

명령줄 도구에 대 한 자세한 내용은 다음 리소스는 hello 참조:

* [간단한 웹 앱: 배포](https://azure.microsoft.com/blog/2014/07/28/simple-azure-websites-deployment/). 도구에 대 한 David Ebbo 블로그에 올린 그 작성 toomake 것 보다 쉽게 toouse 웹 배포 합니다.
* [웹 배포 도구](http://technet.microsoft.com/library/dd568996)(영문). Hello Microsoft TechNet 사이트에서 공식 설명서입니다. 좋은 위치 toostart 여전히 하지만 발표 되었습니다.
* [웹 배포 사용](http://www.iis.net/learn/publish/using-web-deploy)(영문). Hello Microsoft IIS.NET 사이트에서 공식 설명서입니다. 또한 좋은 위치 toostart 하지만 발표 되었습니다.
* [Visual Studio를 사용한 ASP.NET 웹 배포: 명령줄 배포](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment)MSBuild는 Visual Studio에서 사용되는 빌드 엔진입니다. MSBuild는 hello 빌드 엔진 Visual Studio에서 사용 되며 또한 hello 명령줄 toodeploy 웹 응용 프로그램 tooWeb 앱에서에서 사용할 수 있습니다. 이 자습서는 주로 Visual Studio 배포에 대해 다루는 시리즈의 일부입니다.


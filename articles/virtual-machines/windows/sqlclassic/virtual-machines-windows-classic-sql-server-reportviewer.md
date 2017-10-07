---
title: "웹 사이트에서 ReportViewer aaaUse | Microsoft Docs"
description: "이 항목 저장 방법을 설명 toobuild 보고서를 표시 하는 hello Visual Studio ReportViewer 컨트롤과 함께 Microsoft Azure 웹 사이트는 Microsoft Azure 가상 컴퓨터에 있습니다."
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 78b76318-d9bf-48ef-9d9e-d1b7d8cf3042
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 8e0729d6657f96c32a9ac7dffdff7745ff92b48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-reportviewer-in-a-web-site-hosted-in-azure"></a>Azure에서 호스트되는 웹 사이트에서 ReportViewer 사용
> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

Microsoft Azure 가상 컴퓨터에 저장 된 보고서를 표시 하는 Visual Studio ReportViewer 컨트롤 hello로 Microsoft Azure 웹 사이트를 빌드할 수 있습니다. ReportViewer 컨트롤 hello hello ASP.NET 웹 응용 프로그램 템플릿을 사용 하 여 작성 하는 웹 응용 프로그램에는 합니다.

> [!IMPORTANT]
> hello ASP.NET MVC 웹 응용 프로그램 템플릿은 hello ReportViewer 컨트롤을 지원 하지 않습니다.

Microsoft Azure 웹 사이트에 ReportViewer를 tooincorporate, toocomplete hello 작업을 수행 해야 합니다.

* **추가** 어셈블리 toohello 배포 패키지
* **구성** 
* **게시** ASP.NET 웹 응용 프로그램 tooAzure hello

## <a name="prerequisites"></a>필수 조건
Hello "일반 권장 사항 및 모범 사례" 섹션 검토 [Azure 가상 컴퓨터의 SQL Server Business Intelligence](../classic/ps-sql-bi.md)합니다.

> [!NOTE]
> ReportViewer 컨트롤은 Visual Studio Standard Edition 이상 버전과 함께 제공됩니다. Hello Web Developer Express Edition을 사용 하는 경우 hello를 설치 해야 [MICROSOFT REPORT VIEWER 2012 런타임](https://www.microsoft.com/download/details.aspx?id=35747) toouse hello ReportViewer 런타임 기능입니다.
> 
> 로컬 처리 모드에서 구성된 ReportViewer는 Microsoft Azure에서 지원되지 않습니다.

## <a name="adding-assemblies-toohello-deployment-package"></a>어셈블리 toohello 배포 패키지를 추가합니다.
ASP.NET 응용 프로그램이 온-프레미스를 호스팅하는 경우 hello ReportViewer 어셈블리 일반적으로 Visual Studio를 설치 하는 동안 hello hello IIS 서버의 전역 어셈블리 캐시 (GAC)에 직접 설치는 및 hello 응용 프로그램에서 직접 액세스할 수 있습니다. 그러나 호스트 Microsoft Azure hello 클라우드에서 ASP.NET 응용 프로그램 toobe에 설치 하는 아무 것도 허용 하지 않는 hello GAC에 있는지 확인 해야 하므로 hello ReportViewer 어셈블리 응용 프로그램에 사용할 수 있습니다. 프로젝트에 대 한 참조 toothem를 추가 하 여이 작업을 수행 하 고 구성할 toobe 로컬로 복사 합니다.

원격 처리 모드 hello ReportViewer 컨트롤 어셈블리를 수행 하는 hello를 사용 합니다.

* **Microsoft.ReportViewer.WebForms.dll**: 포함 해야 하는 hello ReportViewer 코드 페이지에 ReportViewer toouse 합니다. 이 어셈블리에 대 한 참조는 프로젝트에서 ASP.NET 페이지에 ReportViewer 컨트롤을 놓을 때 tooyour 프로젝트를 추가 됩니다.
* **Microsoft.ReportViewer.Common.dll**: 런타임 시 hello ReportViewer 컨트롤에서 사용 하는 클래스를 포함 합니다. Tooyour 프로젝트 자동으로 추가 되지 않습니다.

### <a name="tooadd-a-reference-toomicrosoftreportviewercommon"></a>참조 tooMicrosoft.ReportViewer.Common tooadd
* 프로젝트를 마우스 오른쪽 단추로 클릭 **참조** 노드 선택한 **참조 추가**hello.NET 탭에서 hello 어셈블리를 선택 하 고 클릭 **확인**합니다.

### <a name="toomake-hello-assemblies-locally-accessible-by-your-aspnet-application"></a>ASP.NET 응용 프로그램에 액세스할 수 있는 로컬로 toomake hello 어셈블리
1. Hello에 **참조** 폴더를 해당 속성이 hello 속성 창에 표시 되도록 hello Microsoft.ReportViewer.Common 어셈블리를 클릭 합니다.
2. Hello 속성 창에서 설정 **로컬 복사** tooTrue 합니다.
3. Microsoft.ReportViewer.WebForms에 대해 1단계 및 2단계를 반복합니다.

### <a name="tooget-reportviewer-language-pack"></a>tooget ReportViewer 언어 팩
1. hello 제공 하는 Microsoft Report Viewer 2012 런타임 적절 한 재배포 가능 패키지 설치 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=317386)합니다.
2. Hello 드롭다운 목록 및 hello 페이지에서 선택 hello 언어 리디렉션된 toohello 해당 다운로드 센터 페이지를 가져옵니다.
3. 클릭 **다운로드** toostart hello ReportViewerLP.exe 다운로드 합니다.
4. ReportViewerLP.exe를 다운로드 한 후 클릭 **실행** tooinstall 즉시 키를 누르거나 **저장** toosave 것 tooyour 컴퓨터입니다. 클릭 하면 **저장**, hello 파일을 저장할 hello 폴더의 hello 이름 기억 합니다.
5. Hello 파일을 저장 하는 hello 폴더를 찾습니다. ReportViewerLP.exe를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭한 다음 **예**를 클릭합니다.
6. ReportViewerLP.exe를 실행 한 후 나타납니다 hello c:\windows\assembly에 리소스 파일 hello **Microsoft.ReportViewer.Webforms.Resources** 및 **Microsoft.ReportViewer.Common.Resources** .

### <a name="tooconfigure-for-localized-reportviewer-control"></a>지역화 된 ReportViewer 컨트롤에 대 한 tooconfigure
1. 다운로드 하 고 지정 된 명령이 위에 다음 hello 하 여 hello Microsoft Report Viewer 2012 런타임 재배포 가능 패키지를 설치 합니다.
2. 만들 <language> 폴더 hello 프로젝트 및 복사 hello에 리소스 어셈블리 파일에 연결 합니다. hello 리소스 어셈블리 파일 toobe 복사는: **Microsoft.ReportViewer.Webforms.Resources.dll** 및 **Microsoft.ReportViewer.Common.Resources.dll**합니다. Hello 리소스 어셈블리 파일을 선택 하 고 hello 속성 창에서 설정 **tooOutput 디렉터리 복사** 너무 "**항상 복사**"입니다.
3. 설정 hello 웹 프로젝트에 대 한 Culture 및 UICulture hello 합니다. Tooset hello Culture 및 UL Culture는 ASP.NET 웹 페이지에 대 한 참조 하는 방법에 대 한 자세한 내용은 [하는 방법: 집합 ASP.NET 웹 페이지 전역화를 위해 Culture 및 UL Culture hello](http://go.microsoft.com/fwlink/?LinkId=237461)합니다.

## <a name="configuring-authentication-and-authorization"></a>인증 및 권한 부여 구성
hello ReportViewer hello 보고서 서버와 적절 한 자격 증명 tooauthenticate toouse 되어야 하며 hello 보고서 서버 tooaccess hello 보고서를 원하는 hello 자격 증명에 권한을 부여 해야 합니다. 인증에 대 한 내용은 hello 백서를 참조 [Reporting Services 보고서 뷰어 컨트롤 및 Microsoft Azure 가상 컴퓨터 기반 보고서 서버](https://msdn.microsoft.com/library/azure/dn753698.aspx)합니다.

## <a name="publish-hello-aspnet-web-application-tooazure"></a>ASP.NET 웹 응용 프로그램 tooAzure hello 게시
ASP.NET 웹 응용 프로그램 tooAzure 게시에 대 한 지침을 참조 하십시오. [하는 방법: 마이그레이션하고 게시할 Visual Studio에서 웹 응용 프로그램 tooAzure](../../../vs-azure-tools-migrate-publish-web-app-to-cloud-service.md) 및 [웹 앱 및 ASP.NET 시작](../../../app-service-web/app-service-web-get-started-dotnet.md)합니다.

> [!IMPORTANT]
> 솔루션 탐색기에서 hello 바로 가기 메뉴에 표시 되지 않으면 hello Azure 배포 프로젝트 추가 또는 Azure 클라우드 서비스 프로젝트 추가 명령 하는 경우에 hello 프로젝트 too.NET Framework 4에 대 한 toochange hello에 대 한 대상 프레임 워크를 할 수 있습니다.
> 
> hello 두 명령은 기본적으로 제공 hello 동일한 기능입니다. 하나 또는 hello hello Microsoft Azure SDK의 버전에 따라 설치한 경우 다른 명령이 hello 바로 가기 메뉴에 표시 됩니다.
> 
> 

## <a name="resources"></a>리소스
[Microsoft 보고서](http://go.microsoft.com/fwlink/?LinkId=205399)

[Azure 가상 컴퓨터의 SQL Server Business Intelligence](../classic/ps-sql-bi.md)

[PowerShell tooCreate는 Azure VM으로는 기본 모드 보고서 서버를 사용 하 여](../classic/ps-sql-report.md)


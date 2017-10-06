---
title: "-Azure Cosmos DB 템플릿 사용 하 여 웹 응용 프로그램 aaaDeploy | Microsoft Docs"
description: "어떻게 toodeploy Azure Cosmos DB 계정, Azure 앱 서비스 웹 앱 및 샘플 웹 Azure 리소스 관리자 템플릿을 사용 하는 응용 프로그램에 알아봅니다."
services: cosmos-db, app-service\web
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 087d8786-1155-42c7-924b-0eaba5a8b3e0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: b2bdde9279aad570606d7bf06dfc710f564b4d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-cosmos-db-and-azure-app-service-web-apps-using-an-azure-resource-manager-template"></a>Azure Resource Manager 템플릿을 사용하여 Azure Cosmos DB 및 Azure App Service Web Apps 배포
이 자습서에서는 Azure 리소스 관리자 템플릿 toodeploy toouse 통합 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/), [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) web app 및 샘플 웹 응용 프로그램입니다.

Azure 리소스 관리자 템플릿을 사용 하 여 Azure 리소스의 hello 배포 및 구성을 쉽게 자동화할 수 있습니다.  이 자습서에서는 방법을 toodeploy 웹 응용 프로그램을 자동으로 Azure Cosmos DB 계정 연결 정보를 구성 합니다.

이 자습서를 완료 하면 다음 질문 수 tooanswer hello 수 있습니다.  

* Azure 리소스 관리자 템플릿 toodeploy 사용을 Azure Cosmos DB 계정 및 Azure 앱 서비스의 웹 응용 프로그램을 통합할 수 있습니다 어떻게 있습니까?
* Azure 리소스 관리자 템플릿 toodeploy를 사용 하 여을 Azure Cosmos DB 계정, 앱 서비스 웹 앱의 웹 앱 및 Webdeploy 응용 프로그램을 통합할 수 있습니다 어떻게 있습니까?

<a id="Prerequisites"></a>

## <a name="prerequisites"></a>필수 조건
> [!TIP]
> 이 자습서에서는 이전 Azure 리소스 관리자 템플릿을 또는 JSON 사용해 본 경험이 가정 하지, 해야 경우 할 toomodify hello 템플릿이나 배포 옵션을 참조 한 후 이러한 각 영역에 대 한 지식이 있으면 됩니다.
> 
> 

이 자습서에서는 hello 지침을 수행 하기 전에 hello 다음 있는지를 확인 합니다.

* Azure 구독. Azure는 구독 기반 플랫폼입니다.  구독을 얻는 방법에 대한 자세한 내용은 [구매 옵션](https://azure.microsoft.com/pricing/purchase-options/), [구성원 제공 항목](https://azure.microsoft.com/pricing/member-offers/) 또는 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.

## <a id="CreateDB"></a>1 단계: hello 템플릿 파일을 다운로드
이 자습서에 사용 될 hello 템플릿 파일을 다운로드 하 여 시작 하겠습니다.

1. Hello 다운로드 [Azure Cosmos DB 계정, 웹 응용 프로그램을 만들고 데모 응용 프로그램 샘플 배포](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json) 템플릿 tooa 로컬 폴더 (예: C:\Azure Cosmos DBTemplates). 이 템플릿은 Azure Cosmos DB 계정, App Service 웹앱 및 웹 응용 프로그램을 배포합니다.  Hello 웹 응용 프로그램 tooconnect toohello Azure Cosmos DB 계정을 자동으로 구성 됩니다.
2. Hello 다운로드 [Azure Cosmos DB 계정 및 웹 앱 샘플을 만드는](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json) 템플릿 tooa 로컬 폴더 (예: C:\Azure Cosmos DBTemplates). 이 템플릿은 Azure Cosmos DB 계정을 앱 서비스 웹 앱을 배포 합니다 및 hello 사이트의 응용 프로그램 설정 tooeasily 표면 Azure Cosmos DB 연결 정보를 수정 합니다 있지만 웹 응용 프로그램에 포함 되지 않습니다.  

<a id="Build"></a>

## <a name="step-2-deploy-hello-azure-cosmos-db-account-app-service-web-app-and-demo-application-sample"></a>2 단계: 배포 hello Azure Cosmos DB 계정으로 앱 서비스 웹 앱과 데모 응용 프로그램 샘플
이제 첫 번째 템플릿을 배포합니다.

> [!TIP]
> hello 템플릿 hello 웹 응용 프로그램 이름 및 Azure Cosmos DB 계정 이름 아래에 입력 되는) 유효 하 고 b) 사용 가능한 유효성이 확인 되지 않습니다.  Hello 가용성 hello의 이름을 확인 하는 것이 좋습니다 toosupply 이전 toosubmitting hello 배포를 계획 합니다.
> 
> 

1. 로그인 toohello [Azure 포털](https://portal.azure.com)"템플릿 배포"에 대 한 검색을 새로 만들기를 클릭 합니다.
    ![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment1.png)
2. Hello 템플릿 배포 항목을 선택 하 고 클릭 **만들기** ![hello 템플릿 배포 UI의 스크린 샷](./media/create-website/TemplateDeployment2.png)
3. 클릭 **템플릿 편집**hello DocDBWebsiteTodo.json 템플릿 파일의 hello 내용을 붙여넣고 클릭 **저장**합니다.
   ![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment3.png)
4. 클릭 **매개 변수 편집**각 매개 변수에 필수 hello에 대 한 값을 제공 하 고 클릭, **확인**합니다.  hello 매개 변수는 다음과 같습니다.
   
   1. SITENAME: hello 앱 서비스 웹 앱 이름 지정 및 tooaccess hello 웹 응용 프로그램 사용 하 여 사용 되는 tooconstruct hello URL입니다 (예: 경우 "mydemodocdbwebapp"를 지정 하 고 hello URL hello 웹 응용 프로그램을 액세스 합니다 기준이 됩니다. mydemodocdbwebapp.azurewebsites.net)입니다.
   2. HOSTINGPLANNAME: 앱 서비스 계획 toocreate 호스팅의 hello 이름을 지정 합니다.
   3. 위치: 지정 hello toocreate hello Azure Cosmos DB 및 웹 응용 프로그램 리소스에는 Azure 위치입니다.
   4. DATABASEACCOUNTNAME: hello Azure Cosmos DB 계정 toocreate의 hello 이름을 지정합니다.   
      
      ![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment4.png)
5. 기존 리소스 그룹을 선택 또는 새 리소스 그룹 이름을 toomake를 제공 하 고 hello 리소스 그룹에 대 한 위치를 선택 합니다.

    ![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment5.png)
6. 클릭 **약관을 검토**, **구매**, 클릭 하 고 **만들기** toobegin hello 배포 합니다.  선택 **Pin toodashboard** hello 결과 배포는 Azure 포털 홈 페이지에 쉽게 볼 수 있도록 합니다.
   ![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment6.png)
7. Hello 배포 완료 되 면 hello 리소스 그룹 블레이드가 열립니다.
   ![Hello 리소스 그룹 블레이드의 스크린샷](./media/create-website/TemplateDeployment7.png)  
8. toouse 단순히 toohello 웹 앱 URL을 이동 하 여 응용 프로그램 hello (hello 위의 예에서 hello URL 일 http://mydemodocdbwebapp.azurewebsites.net).  웹 응용 프로그램을 다음 hello에 표시 됩니다.
   
   ![샘플 Todo 응용 프로그램](./media/create-website/image2.png)
9. 계속 하 고 hello 웹 앱에서 몇 가지 작업을 만드는 hello Azure 포털에서에서 toohello 리소스 그룹 블레이드를 반환 합니다. Hello 리소스 목록에 hello Azure Cosmos DB 계정 리소스를 클릭 한 다음 클릭 **쿼리 탐색기**합니다.
    ![강조 표시 하는 hello 웹 앱과 요약 렌즈를 hello의 스크린샷](./media/create-website/TemplateDeployment8.png)  
10. Hello 기본 쿼리를 실행 "선택 * c에서" hello 결과 검사 하 고 있습니다.  Hello 쿼리 7 위의 단계에서 만든 hello 할 일 항목의 JSON 표현을 hello를 읽어들일 수를 확인 합니다.  쿼리로; 무료 tooexperiment을 생각 합니다. 예를 들어 SELECT를 실행 해 보십시오 * FROM c WHERE c.isComplete = true tooreturn 완료 상태로 표시 된 모든 할 일 항목입니다.
    
    ![Hello 쿼리 탐색기 및 결과 블레이드 hello 쿼리 결과 보여 주는 스크린샷](./media/create-website/image5.png)
11. 무료 tooexplore hello Azure Cosmos DB 포털 환경 느껴집니다 또는 hello 샘플 Todo 응용 프로그램을 수정 합니다.  준비가 되면 다른 템플릿을 배포합니다.

<a id="Build"></a> 

## <a name="step-3-deploy-hello-document-account-and-web-app-sample"></a>3 단계: 배포 hello 문서 계정 및 웹 앱 샘플
이제 두 번째 템플릿을 배포합니다.  이 서식 파일은 유용 tooshow 어떻게 주입할 수 계정 끝점 및 마스터 키와 같은 Azure Cosmos DB 연결 정보는 웹 앱에 응용 프로그램 설정 또는 사용자 지정 연결 문자열입니다. 예를 들어 경우가 있습니다 직접 웹 응용 프로그램을 Azure Cosmos DB 계정과 toodeploy 선택한 hello 연결 정보를 배포 하는 동안 자동으로 채워집니다.

> [!TIP]
> hello 템플릿 hello 웹 응용 프로그램 이름 및 Azure Cosmos DB 계정 이름 아래에 입력 되는) 유효 하 고 b) 사용 가능한 유효성이 확인 되지 않습니다.  Hello 가용성 hello의 이름을 확인 하는 것이 좋습니다 toosupply 이전 toosubmitting hello 배포를 계획 합니다.
> 
> 

1. Hello에 [Azure 포털](https://portal.azure.com)"템플릿 배포"에 대 한 검색을 새로 만들기를 클릭 합니다.
    ![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment1.png)
2. Hello 템플릿 배포 항목을 선택 하 고 클릭 **만들기** ![hello 템플릿 배포 UI의 스크린 샷](./media/create-website/TemplateDeployment2.png)
3. 클릭 **템플릿 편집**hello DocDBWebSite.json 템플릿 파일의 hello 내용을 붙여넣고 클릭 **저장**합니다.
   ![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment3.png)
4. 클릭 **매개 변수 편집**각 매개 변수에 필수 hello에 대 한 값을 제공 하 고 클릭, **확인**합니다.  hello 매개 변수는 다음과 같습니다.
   
   1. SITENAME: hello 앱 서비스 웹 앱 이름 지정 및 tooaccess hello 웹 응용 프로그램 사용 하 여 사용 되는 tooconstruct hello URL입니다 (예: 경우 "mydemodocdbwebapp"를 지정 하 고 hello URL hello 웹 응용 프로그램을 액세스 합니다 기준이 됩니다. mydemodocdbwebapp.azurewebsites.net)입니다.
   2. HOSTINGPLANNAME: 앱 서비스 계획 toocreate 호스팅의 hello 이름을 지정 합니다.
   3. 위치: 지정 hello toocreate hello Azure Cosmos DB 및 웹 응용 프로그램 리소스에는 Azure 위치입니다.
   4. DATABASEACCOUNTNAME: hello Azure Cosmos DB 계정 toocreate의 hello 이름을 지정합니다.   
      
      ![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment4.png)
5. 기존 리소스 그룹을 선택 또는 새 리소스 그룹 이름을 toomake를 제공 하 고 hello 리소스 그룹에 대 한 위치를 선택 합니다.

    ![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment5.png)
6. 클릭 **약관을 검토**, **구매**, 클릭 하 고 **만들기** toobegin hello 배포 합니다.  선택 **Pin toodashboard** hello 결과 배포는 Azure 포털 홈 페이지에 쉽게 볼 수 있도록 합니다.
   ![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment6.png)
7. Hello 배포 완료 되 면 hello 리소스 그룹 블레이드가 열립니다.
   ![Hello 리소스 그룹 블레이드의 스크린샷](./media/create-website/TemplateDeployment7.png)  
8. Hello 리소스 목록에 hello 웹 응용 프로그램 리소스를 클릭 한 다음 클릭 **응용 프로그램 설정** ![hello 리소스 그룹의 스크린 샷](./media/create-website/TemplateDeployment9.png)  
9. Note 있다는 hello Azure Cosmos DB 끝점 및 각 hello Azure Cosmos DB 마스터 키에 있는 응용 프로그램 설정 합니다.

    ![응용 프로그램 설정의 스크린샷](./media/create-website/TemplateDeployment10.png)  
10. Hello Azure 포털을 탐색 하는 무료 toocontinue 느껴집니다 또는 우리의 Azure Cosmos DB 중 하나를 수행 [샘플](http://go.microsoft.com/fwlink/?LinkID=402386) toocreate Azure Cosmos DB 응용 프로그램입니다.

<a name="NextSteps"></a>

## <a name="next-steps"></a>다음 단계
축하합니다. Azure Resource Manager 템플릿을 사용하여 Azure Cosmos DB, App Service 웹앱 및 샘플 웹 응용 프로그램을 배포했습니다.

* Azure Cosmos DB에 대해 자세히 toolearn 클릭 [여기](http://azure.com/docdb)합니다.
* Azure 앱 서비스 웹 앱에 대해 자세히 toolearn 클릭 [여기](http://go.microsoft.com/fwlink/?LinkId=325362)합니다.
* Azure 리소스 관리자 템플릿에 대해 자세히 toolearn 클릭 [여기](https://msdn.microsoft.com/library/azure/dn790549.aspx)합니다.

## <a name="whats-changed"></a>변경된 내용
* 웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)
* 가이드 toohello hello 이전 포털 toohello 새 포털의 변경 참조: [탐색에 대 한 참조 hello Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkId=529715)

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](http://go.microsoft.com/fwlink/?LinkId=523751)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 


---
title: "aaaWhat Azure Analysis Services는 | Microsoft Docs"
description: "Azure의 hello Analysis Services의 큰 그림을 가져옵니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 83d7a29c-57ae-4aa0-8327-72dd8f00247d
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: 48830a86f47a8ddc7770e6c44dd56c29927fe582
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-analysis-services"></a>Azure Analysis Services란?
![Azure Analysis Services](./media/analysis-services-overview/aas-overview-aas-icon.png)

Azure Analysis Services에서 엔터프라이즈급 데이터 hello 클라우드에서 모델링을 제공 합니다. Azure 데이터 플랫폼 서비스와 통합된 서비스로서 완벽하게 관리되는 플랫폼(PaaS)입니다. 

Analysis Services를 사용하면 여러 원본의 데이터를 매시업하고 결합하며 메트릭을 정의하며 단일한, 신뢰할 수 있는 유의적 데이터 모델에서 데이터를 보호할 수 있습니다. hello 데이터 모델은 쉽고 빠르게 하기 위한 방법을 제공 사용자 toobrowse Power BI, Excel, Reporting Services, 제 3 자 및 사용자 지정 응용 프로그램의 같은 클라이언트 응용 프로그램을 사용 하 여 데이터의 양이 합니다.

![데이터 원본](./media/analysis-services-overview/aas-overview-data-sources.png)

체크 아웃 [이 비디오](https://sec.ch9.ms/ch9/d6dd/a1cda46b-ef03-4cea-8f11-68da23c5d6dd/AzureASoverview_high.mp4) toolearn Azure Analysis Services Microsoft 연동 하는 방법의 전체 BI 기능 및 방법을 hello 클라우드로 데이터 모델을 얻을 수 있습니다.

## <a name="built-on-sql-server-analysis-services"></a>SQL Server Analysis Services에 구축
Azure Analysis Services는 이미 SQL Server Analysis Services Enterprise Edition에 있은 훌륭한 기능과 호환 가능하며, Azure Analysis Services 테이블 형식 모델 1200 및 1400 hello에는 지원 [호환성 수준](analysis-services-compat-level.md)합니다. 파티션, 행 수준 보안, 양방향 관계 및 변환을 모두 지원합니다. 메모리 내 및 DirectQuery 모드는 복잡한 대용량 데이터 집합에 대해 매우 빠른 쿼리를 제공합니다.

테이블 형식 모델은 신속한 개발을 제공하며 손쉽게 사용자 지정할 수 있습니다. 테이블 형식 모델 개발자를 위한 hello 테이블 형식 개체 모델 (TOM) toodescribe 모델 개체를 포함 합니다. TOM hello를 통해 JSON에 노출 된 [스크립팅 언어 TMSL (Tabular Model)](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference) 및 hello hello 통해 AMO 데이터 정의 언어 [Microsoft.AnalysisServices.Tabular](https://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx) 네임 스페이스입니다.

## <a name="better-with-azure"></a>Azure를 통해 더욱 향상된 환경
Azure Analysis Services toobuild 사용 하면 여러 Azure 서비스와 통합 되어 정교한 분석 솔루션입니다. 와 통합 [Azure Active Directory](../active-directory/active-directory-whatis.md) tooyour 중요 한 데이터에 안전 하 고, 역할 기반 액세스를 제공 합니다. 와 통합 [Azure Data Factory](../data-factory/data-factory-introduction.md) hello 모델에 데이터를 로드 하는 활동을 포함 하 여 파이프라인입니다. [Azure Automation](../automation/automation-intro.md) 및 [Azure Functions](../azure-functions/functions-overview.md)는 사용자 지정 코드를 사용하여 모델의 간단한 오케스트레이션을 수행하는 데 사용할 수 있습니다.

## <a name="get-up-and-running-quickly"></a>빠른 준비 및 실행
Azure Portal에서는 수분 내에 [서버를 만들 수 있습니다](analysis-services-create-server.md). 그리고 Azure Resource Manager [템플릿](../azure-resource-manager/resource-manager-create-first-template.md)과 PowerShell을 사용하면 선언적 템플릿을 통해 서버를 프로비전할 수 있습니다. 단일 템플릿을 사용하면 저장소 계정 및 Azure Functions과 같은 다른 Azure 구성 요소와 함께 여러 서비스를 배포할 수 있습니다. 

서버를 만들었으면 Azure Portal에서 테이블 형식 모델을 바로 만들 수 있습니다. 새 hello (미리 보기)로 [웹 디자이너 기능](analysis-services-create-model-portal.md), tooan Azure SQL 데이터베이스, Azure SQL 데이터 웨어하우스 데이터 원본에 연결 하거나 Power BI Desktop가.pbix 파일을 가져올 수 있습니다. 테이블 간의 관계는 자동으로 생성 하 고 브라우저에서 json 형식의 오른쪽 hello model.bim 파일을 편집 하거나 측정값을 만들 수 있습니다.

## <a name="scale-tooyour-needs"></a>배율 tooyour 요구 사항
Azure Analysis Services는 개발자, 기본 및 표준 계층에서 사용할 수 있습니다. 각 계층 내의 계획 비용 tooprocessing QPUs, 성능과 메모리 크기에 따라 다릅니다. 서버를 만들 때 계층 내에서 계획을 선택합니다. 계획 변경할 수 있습니다 또는 아래로 hello 내에서 동일한 계층을 지 또는 업그레이드 tooa 더 높은 계층이 있지만 더 높은 계층 tooa 하위 계층에서 다운 그레이드할 수 없습니다.

서버를 강화, 축소 또는 일시 중지합니다. 또는 PowerShell을 사용 하 여 즉시 전체 컨트롤을 포함할 hello Azure 포털을 사용 합니다. 사용한 양만큼만 요금을 지급합니다. hello 서로 다른 계획 및 계층의 경우, 및 사용 하 여 hello 가격 계산기 toodetermine hello 오른쪽 계획에 대해 자세히 toolearn 참조 [Azure Analysis Services 가격](https://azure.microsoft.com/pricing/details/analysis-services/)합니다.

## <a name="keep-your-data-close"></a>데이터를 닫은 상태로 유지
다음 예제 hello azure Analysis Services 서버를 만들 수 있습니다 [Azure 지역](https://azure.microsoft.com/regions/):

| 아메리카 | 유럽 | 아시아 태평양 |
|----------|--------|--------------|
|  브라질 남부<br> 캐나다 중부<br> 미국 동부 2<br> 미국 중북부<br> 미국 중남부<br> 미국 중서부<br> 미국 서부 | 북유럽<br> 영국 남부<br> 서유럽 |   오스트레일리아 남동부<br> 일본 동부<br> 동남아시아<br> 인도 서부  |

새 영역 되 고 추가 된 모든 hello 시간,이 목록은 불완전할 수 있습니다. Azure Portal 또는 Azure Resource Manager 템플릿을 사용하여 서버를 만들 때 위치를 선택합니다. tooget hello에서 최상의 성능이, 가장 큰 사용자 기반 가장 가까운 위치를 선택 합니다. 여러 지역의 중복 서버에 모델을 배포하여 [고가용성](analysis-services-bcdr.md)을 보장합니다.

## <a name="migrate-your-existing-tabular-models"></a>기존 테이블 형식 모델 마이그레이션
기존 온-프레미스 SQL Server Analysis Services 모델 솔루션을 이미 보유 하는 경우 tooAzure Analysis Services 중요 변경 없이 마이그레이션할 수 있습니다. toomigrate, SSDT toodeploy 사용할 수 있습니다 모델 tooyour 서버입니다. 또는 SSMS에서 백업 및 복원 또는 TMSL을 사용할 수 있습니다.

Tooinstall 필요 하 고 구성 온-프레미스 데이터 소스를 설정한 경우는 [온-프레미스 데이터 게이트웨이](analysis-services-gateway.md)합니다. 에서 역할 및 역할 멤버를 이미 구성 되어 있는 경우 역할을 마이그레이션할 하지만 SSMS 또는 PowerShell을 사용 하 여 tooreadd 역할 멤버를 포함 합니다.

## <a name="connect-toopopular-data-sources"></a>Toopopular 데이터 원본 연결
Azure Analysis Services는 지원 [toodata 소스 연결](analysis-services-datasource.md) 온-프레미스 조직에서 및 hello 클라우드에서 합니다. 하이브리드 솔루션을 위해 온-프레미스 및 클라우드 데이터 원본의 데이터를 모두 결합합니다. 

Ssdt에서 hello M 쿼리 수식 언어에 따라 hello 최신 데이터 가져오기 기능을 사용 하는 새 테이블 형식 1400 모델. 데이터 가져오기 더 많은 데이터 변환 매시업 기능 및 hello 기능 toocreate 수 있으며 사용자가 직접 고급 M 수식 언어 쿼리를 편집 합니다. 예를 들어 1400 테이블 형식 모델을 사용하면 Azure Blob Storage의 데이터 파일을 모델링할 수 있습니다.

## <a name="use-hello-tools-you-already-know"></a>이미 알고 있는 hello 도구를 사용 하 여

![BI 개발자 도구](./media/analysis-services-overview/aas-overview-dev-tools.png)

#### <a name="sql-server-data-tools-ssdt-for-visual-studio"></a>SSDT(SQL Server Data Tools) for Visual Studio
개발 하 고 무료 hello 사용 하 여 모델 배포 [SQL Server 데이터 도구 (SSDT) Visual Studio에 대 한](https://msdn.microsoft.com/library/mt204009.aspx)합니다. SSDT에는 빠르게 준비하고 실행할 수 있는 Analysis Services 프로젝트 템플릿이 포함되어 있습니다. SSDT 이제 기능이 있는 hello 최신 데이터 가져오기 데이터 원본 쿼리 및 매시업 1400의 테이블 형식 모델에 대 한 합니다. Power BI Desktop 및 Excel 2016에서 데이터 가져오기에 익숙한 경우 이미 알고 있는 얼마나 쉬운지 toocreate 고도로 사용자 지정 된 데이터 원본 쿼리.

#### <a name="sql-server-management-studio"></a>SQL Server Management Studio
[SSMS(SQL Server Management Studio)](https://msdn.microsoft.com/library/mt238290.aspx)를 사용하여 서버 및 모델 데이터베이스를 관리합니다. Tooyour hello 클라우드의 서버를 연결 합니다. Hello XMLA 쿼리 창에서 오른쪽 TMSL 스크립트를 실행 하 고 TMSL 스크립트를 사용 하 여 작업을 자동화 합니다. SSMS가 매월 업데이트되므로 새 특징과 기능이 빠르게 출시됩니다.

#### <a name="powershell"></a>PowerShell
서버 리소스 관리 작업과 서버를 만드는, 일시 중단 또는 서버 작업을 다시 시작 또는 변경 hello 서비스 수준 (계층)와 같은 Azure 리소스 관리자 (AzureRM) cmdlet을 사용 합니다. 역할 멤버 추가 또는 제거와 같은 데이터베이스를 관리 하기 위한 다른 작업을 처리 또는 TMSL 스크립트 실행에 cmdlet을 사용 hello SqlServer 모듈입니다. AzureRM와 SQLServer 모듈은 hello에서 사용할 수 있는 [PowerShell 갤러리](https://www.powershellgallery.com/)합니다.


## <a name="your-data-is-secure"></a>데이터가 안전함
![데이터 시각화](./media/analysis-services-overview/aas-overview-secure.png)

#### <a name="authentication"></a>인증
Azure Analysis Services에 대한 사용자 인증은 [AAD(Azure Active Directory)](../active-directory/active-directory-whatis.md)에서 처리됩니다. Toolog tooan Azure Analysis Services 데이터베이스를 사용 하 여 사용자의 조직 계정 id를 사용 하 여 toohello 데이터베이스 액세스를 시도할 때 tooaccess를 시도 하지 합니다. 이러한 사용자 id에 hello Azure Analysis Services 서버가 있는 hello 구독에 대 한 hello 기본 Azure Active Directory의 구성원 이어야 합니다. toolearn 더 참조 [인증 및 사용자 권한을](analysis-services-manage-users.md)합니다.

#### <a name="data-security"></a>데이터 보안
Azure Analysis Services에서 Azure Blob 저장소 toopersist 저장소 및 Analysis Services 데이터베이스에 대 한 메타 데이터를 사용합니다. Blob에 있는 데이터 파일은 Azure Blob SSE(Server Side Encryption)를 통해 암호화됩니다. 직접 쿼리 모드를 사용하는 경우 메타데이터만 저장됩니다. hello 실제 데이터 쿼리 시 hello 데이터 소스에서 액세스 됩니다.

#### <a name="on-premises-data-sources"></a>온-프레미스 데이터 원본
보안 액세스 toodata 상주 온-프레미스 조직에서 설치 및 구성에 의해 이루어집니다는 [온-프레미스 데이터 게이트웨이](analysis-services-gateway.md)합니다. 게이트웨이는 액세스 toodata 직접 쿼리 및 메모리 내 모드를 모두 제공합니다. Azure Analysis Services 모델 tooan 온-프레미스 데이터 원본에 연결 되 면 쿼리는 hello 온-프레미스 데이터 원본에 대 한 암호화 hello 자격 증명과 함께 생성 됩니다. hello 게이트웨이 클라우드 서비스 hello 쿼리를 분석 하 고 hello 요청 tooan Azure 서비스 버스를 푸시합니다. hello 온-프레미스 게이트웨이 보류 중인 요청 hello에 대 한 Azure 서비스 버스를 폴링합니다. hello 게이트웨이 다음 hello 쿼리, hello 자격 증명의 암호를 해독 가져오고 toohello 실행할 데이터 소스에 연결 합니다. hello 결과 다음 hello 데이터 원본에서 전송 toohello 게이트웨이 백업 하 고 데이터베이스 toohello Azure Analysis Services에 있습니다.

Azure Analysis Services는 hello에 준하여 [Microsoft 온라인 서비스 약관](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) 및 hello [Microsoft 온라인 서비스 개인정보취급방침](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx)합니다.
Azure 보안에 대해 자세히 toolearn 참조 hello [Microsoft 보안 센터](https://www.microsoft.com/trustcenter/Security/AzureSecurity)합니다.

## <a name="supports-hello-latest-client-tools"></a>Hello 최신 클라이언트 도구를 지원합니다.
![데이터 시각화](./media/analysis-services-overview/aas-overview-clients.png)

Power BI, Excel 및 타사 도구와 같은 최신 데이터 탐색 및 시각화 도구는 모델 데이터에 대해 시각적으로 풍부한 대화형 정보를 사용자에게 제공합니다.

MSOLAP, AMO 또는 ADOMD 클라이언트에 사용 하 여 [클라이언트 라이브러리](analysis-services-data-providers.md) tooconnect tooAnalysis 서비스 서버입니다. Power BI Desktop 및 Excel과 같은 Microsoft 클라이언트 응용 프로그램은 이러한 세 가지 클라이언트 라이브러리를 모두 설치합니다. 하지만 염두에서에 둬야, hello 버전 또는 업데이트 빈도 따라 클라이언트 라이브러리 Azure Analysis Services에 필요한 hello 최신 버전이 아닐 수도 있습니다. hello 마찬가지 toocustom 응용 프로그램이 나 AsCmd, TOM, ADOMD.NET 같은 다른 인터페이스입니다. 이러한 응용 프로그램 패키지의 일부로 hello 라이브러리를 수동으로 설치 합니다. 일반적으로 필요 합니다.


## <a name="get-help"></a>도움말 보기

#### <a name="documentation"></a>설명서
Azure Analysis Services는 간단한 tooset를 및 toomanage. Toocreate 필요 하 고 여기에 서버 서비스를 관리할 모든 hello 정보를 찾을 수 있습니다. 데이터 모델 toodeploy tooyour 서버를 만들 때 것이 훨씬 hello 동일 tooan 온-프레미스 서버를 배포 하는 데이터 모델을 만드는 그대로 합니다. 개념, 절차, 자습서 및 참조 문서에 대한 광범위한 자료는 [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services)에 있습니다.

#### <a name="videos"></a>비디오
[Channel 9의 Azure Analysis Services](https://channel9.msdn.com/series/Azure-Analysis-Services)에서 유용한 동영상을 확인하세요.

#### <a name="blogs"></a>블로그
상황이 빠르게 변화하고 있습니다. 항상 hello hello 대 대 한 최신 정보를 얻을 수 있습니다 [Analysis Services 팀 블로그](https://blogs.msdn.microsoft.com/analysisservices/) 및 [Azure 블로그](https://azure.microsoft.com/blog/)합니다.

#### <a name="community"></a>커뮤니티
Analysis Services에는 활발한 사용자 커뮤니티가 있습니다. Hello 대화에 참가 [Azure Analysis Services 포럼](https://aka.ms/azureanalysisservicesforum)합니다.

## <a name="feedback"></a>사용자 의견
제안할 사항이나 요청하려는 기능이 있습니까? 켜야 있는지 tooleave 설명을 [Azure Analysis Services 피드백](https://aka.ms/azureanalysisservicesfeedback)합니다.

Hello 설명서에 대 한 제안 사항 있습니까? 각 아티클에 hello 맨 아래에 Livefyre를 사용 하 여 주석을 추가할 수 있습니다.

## <a name="next-steps"></a>다음 단계
이제는 Azure Analysis Services에 대 한 자세한 정보를 알면이 시간 tooget 시작 합니다. 너무 방법에 대해 알아봅니다[서버 만들기](analysis-services-create-server.md) Azure에서. 서버를 준비 하는 경우 hello 단계별로 [Adventure Works 자습서](tutorials/aas-adventure-works-tutorial.md) toolearn 어떻게 toocreate 완벽 하 게 작동 하는 테이블 형식 모델 tooyour 서버를 배포 하 고 있습니다.

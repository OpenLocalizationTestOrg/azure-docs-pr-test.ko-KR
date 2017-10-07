---
title: "SDK for.NET 2.7 및.NET 2.7.1 aaaAzure 릴리스 정보"
description: "Azure SDK for .NET 2.7 및 .NET 2.7.1 릴리스 정보"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: 877d070a-9bd5-49b3-8fac-6bb5f65c3554
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 8ec72b0f18702e6d811f0cbe4790685be7881d96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-27-and-net-271-release-notes"></a>Azure SDK for .NET 2.7 및 .NET 2.7.1 릴리스 정보
## <a name="overview"></a>개요
이 문서는 hello.NET 2.7 릴리스에 대 한 hello Azure SDK 릴리스 정보를 포함합니다. 

hello 문서도.NET 2.7.1 해제에 대 한 hello hello Azure SDK 릴리스 정보를 포함 합니다.

Azure SDK 2.7은 Visual Studio 2015 및 Visual Studio 2013에서만 지원됩니다. [Azure SDK 2.6](https://azure.microsoft.com/downloads/) hello Visual Studio 2012 용 SDK를 마지막으로 지원 됩니다.

이 릴리스에 대한 자세한 내용은 [Azure SDK 2.7 발표 게시물](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/) 및 [Azure SDK 2.7.1 발표 게시물](http://go.microsoft.com/fwlink/?LinkId=623850)을 참조하세요.

## <a name="azure-sdk-for-net-27"></a>Azure SDK for .NET 2.7
### <a name="sign-in-improvements-for-visual-studio-2015"></a>Visual Studio 2015의 향상된 로그인 기능
Visual Studio 2015 용 azure SDK 2.7 Visual Studio 2015의 hello 새 id 관리 기능을 지원합니다.  역할 기반 액세스 제어, 클라우드 솔루션 공급자, DreamSpark, 기타 계정 및 구독 유형을 통해 Azure에 액세스하는 계정에 대한 지원이 포함되어 있습니다.

hello 로그인 개선 기능이 포함 된 Azure SDK 2.7은만 Visual Studio 2015에서 사용할 수 있습니다. Visual Studio 2013에 대한 지원은 Azure SDK 2.7.1에 포함되어 있습니다.

### <a name="mobile-sdk"></a>모바일 SDK
업데이트 **모바일 앱** 템플릿 tooreflect 최신 [NuGet 패키지](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) 하 여 프로세스를 설정 합니다.

### <a name="service-bus"></a>서비스 버스
일반 버그 수정 사항 및 향상된 기능입니다. 업데이트 및 기능에 대 한 정보를 얻기 위해 hello 최신 버전의 toohello 릴리스 정보를 참조 하십시오 [Service Bus NuGet](http://www.nuget.org/packages/WindowsAzure.ServiceBus/)합니다.

### <a name="hdinsight-tools"></a>HDInsight 도구
이 릴리스 hello에 다음과 같은 업데이트가 적용 되었습니다. 이러한 업데이트는 미리 보기 상태입니다. 자세한 내용은 [이 블로그](http://go.microsoft.com/fwlink/?LinkId=619108)를 참조하세요.

* Tez 기반 Hive 작업에 대한 Hive 그래프
* 완전한 Hive DML IntelliSense 지원
* Pig 템플릿 지원
* Azure 서비스용 Storm 템플릿

#### <a name="breaking-changes"></a>주요 변경 내용
* 이전 **스톰** 이 버전의 hello 도구를 사용 하는 경우 프로젝트를 업그레이드 해야 합니다. 자세한 내용은 [이 블로그](http://go.microsoft.com/fwlink/?LinkId=619108)를 참조하세요.
* Visual Studio Web Express는 더 이상 지원되지 않습니다. 자세한 내용은 [이 블로그](http://go.microsoft.com/fwlink/?LinkId=619108)를 참조하세요.

### <a name="azure-app-service-tools"></a>Azure 앱 서비스 도구
이 릴리스 hello에 다음과 같은 내용이 업데이트 tooWeb 도구 확장 합니다. 자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/)를 참조하세요. 

* DreamSpark 계정에 대한 지원 추가
* 전체 tooAzure 새로운 Azure 리소스 관리 Api hello toosupport 도구 변경
* Azure 앱 서비스에 대 한 지원 추가 너무[클라우드 탐색기](#cloud_explorer)

#### <a name="known-issues"></a>알려진 문제
서버 탐색기에서 hello 슬롯 노드 아래에서 웹 응용 프로그램 배포 슬롯 노드가 표시 되지 않습니다 및 웹 응용 프로그램 배포 슬롯 자식 노드 클라우드 탐색기에서 로드 되지 않습니다. 이 문제가 해결 되었으며 hello 다음 SDK 버전에 대 한 준비 합니다. 

### <a name="cloud_explorer"></a>Visual Studio 2015용 Cloud Explorer
Azure SDK 2.7 포함 되어 클라우드 탐색기 tooview 사용할 수 있는 Visual Studio 2015 용 Azure 리소스 사용, 해당 속성을 검사 하 고 Visual Studio 내에서 키 개발자 작업을 수행할 키를 누릅니다. 

클라우드 탐색기 hello 다음을 지원합니다.

* Azure 리소스에 대한 리소스 그룹 및 리소스 종류 뷰 
* 이름별 리소스 검색(리소스 종류 뷰에서 사용 가능)
* RBAC(역할 기반 액세스 제어)가 적용되는 구독 및 리소스에 대한 지원 
* 개발자 중심 작업 특정 tooselected 리소스를 보여 주는 통합된 작업 패널입니다. 예: 가상 컴퓨터를 사용 하 여 만든 리소스 관리자 스택의 등 가상 컴퓨터에 대 한 진단 데이터 보기 hello에 대 한 원격 디버거를 연결 합니다.
* 개발/테스트 중 일반적으로 필요한 개발자 중심 속성을 보여주는 통합 속성 패널 
* (도구 모음에서 설정 명령을 사용 하 여) 리소스 열거 hello 계정 toouse의 빠른 전환 
* (도구 모음에서 설정 명령을 사용 하 여) 리소스 열거 하는 경우 구독 toouse의 필터링 
* 리소스 및 리소스 그룹의 관리를 위한 딥 링크 toohello Azure 포털 

### <a name="azure-resource-manager-tools"></a>Azure 리소스 관리자 도구
hello Azure 리소스 관리자 도구에는 새 구독 유형 및 역할 기반 액세스 제어 (RBAC) 사용 하 여 업데이트 된 toowork 되었습니다.  Hello 기능 toouse 새 저장소 계정, 또한 tooclassic 저장소 배포 시 toostore 아티팩트는 이러한 변경 내용은 포함 되어 있습니다.  

Hello SDK의 이전 버전에서는 Azure 리소스 그룹 프로젝트를 사용 하 여 hello 2.7 SDK가 있는 경우 새 배포 스크립트는 새 저장소 계정을 클래식 저장소 대신 사용 하 여 필요한 toodeploy.  Tooyour 프로젝트 tooadd hello 새 스크립트 변경 하기 전에 라는 메시지가 표시 됩니다.  이전 스크립트 hello 바뀌고이 필요 합니다 toohello 새 스크립트 toomanually 사항을 수정 합니다.

### <a name="storage-explorer-tools"></a>저장소 탐색기 도구
* 추가 Blob 보기 지원입니다. 자세한 내용은 [이 블로그 게시물](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/04/13/introducing-azure-storage-append-blob.aspx)에 있습니다. 
* 서버 탐색기를 통한 프리미엄 저장소 계정 보기 지원입니다. 프리미엄 저장소 계정에만 지원 hello 형식으로 서버 탐색기 프리미엄 저장소 계정의 페이지 blob을 표시 됩니다.

### <a name="azure-data-factory-tools-for-visual-studio"></a>Visual Studio용 Azure Data Factory 도구
Visual Studio용 **Azure Data Factory 도구**를 소개합니다. 다음은 사용 하도록 설정 하는 hello 기능입니다. 자세한 내용은 [이 블로그](http://go.microsoft.com/fwlink/?LinkId=617530)를 참조하세요.

* **템플릿 기반 제작**: 기반된 템플릿을 사용 하 여 대/소문자를 사용, 데이터 이동 서식 파일 또는 데이터 처리 템플릿 toodeploy 종단 간 데이터 통합 솔루션을 선택 하 고 데이터 팩터리를 신속 하 게 시작 합니다. 
* **Data Factory 엔터티 작성 및 배포를 위해 솔루션 탐색기와 통합**: 파이프라인 및 관련 엔터티를 Visual Studio 프로젝트로 만들고 배포합니다. 
* **제작 하는 동안 시각적 상호 작용에 대 한 다이어그램 보기와의 통합**: 파이프라인 및 hello 다이어그램 보기에서에서 지 원하는 데이터 집합을 시각적으로 작성 합니다. 
* **탐색 및 상호 작용 이미 배포 된 엔터티가 포함 된 서버 탐색기와의 통합**: 활용 hello 서버 탐색기 toobrowse 이미 데이터 팩터리 및 해당 엔터티를 배포 합니다. 배포된 데이터 팩터리 또는 엔터티(파이프라인, 연결된 서비스, 데이터 집합)를 프로젝트로 가져옵니다. 
* **스키마 유효성 검사와 다양한 기능의 Intellisense를 사용하는 JSON 편집**: 다양한 기능의 Intellisense와 스키마 유효성 검사를 사용하여 Data Factory 엔터티의 JSON 문서를 효율적으로 구성하고 편집합니다. 
* **여러 환경 게시**: 제작 된 파이프라인 toodev, 테스트 또는 Prod 환경을 각 환경에 대 한 별도 구성 파일을 만들어 게시 합니다.
* **Pig, Hive 및 .Net 기반 데이터 처리 지원**: Data Factory 프로젝트의 Pig 및 Hive 스크립트에 대한 지원입니다. .NET 작업 관리에 필요한 C# 프로젝트 참조에 대한 지원입니다.

## <a name="azure-sdk-for-net-271"></a>Azure SDK for .NET 2.7.1
다음 단원을 hello 도입 된 것과 hello Azure SDK.NET 2.7.1 해제에 대 한 업데이트가 포함 되어 있습니다.

### <a name="hdinsight-tools"></a>HDInsight 도구
HDInsight 도구 업데이트에 대한 자세한 내용은 [이 블로그](http://go.microsoft.com/fwlink/?LinkId=623831)를 참조하세요.

* Hive 작업 운영자 뷰(새로운 기능)
  
    더 나은 하이브 쿼리, hello 하이브 연산자 보기 기능을 이해 하는 toohelp 추가 되었습니다. toosee hello 작업 그래프의 hello 꼭 짓 정점 내 모든 hello 연산자 두 번 클릭 합니다. tooview 해당 연산자 위에 마우스를 가져가고는 특정 연산자에 대 한 자세한 정보.
* Hive 오류 표식(새로운 기능)
  
    tooenable 있습니다 tooview hello 문법 오류 즉시 hello 오류 표식 하이브 기능이 추가 되었습니다. 또한 오류 메시지가 향상 되어 하 고 자세한 문법 오류 즉시 표시 됩니다 (이번이 릴리스까지 했던 toosubmit 하이브 스크립트 toohello 클러스터와 해당 오류 메시지에 대 한 세부 정보를 가져오기 전에 일정 시간 동안 대기).  
* Storm 토폴로지 그래프(새로운 기능)
  
    시각화는 토폴로지에 예상 대로 작동 하는 경우 toosee 하려는 경우에 매우 중요 합니다. 이 릴리스에서는 Storm 그래프에 대한 시각화가 추가되었습니다. 토폴로지에 대 한 hello 중요 한 메트릭을 시각화할 수 있습니다 (예를 들어 색에는 특정 이외의 날씨 인지 나타냅니다 "사용 중"). 클릭할 수도 있습니다 두 번 hello 볼트/배출구 tooview 자세한 세부 정보입니다.
* Hello Azure 포털 (버그 수정)에서 작성 된 HDInsight 클러스터에 대 한 지원
  
    이제 tooview Visual Studio를 사용 하 여 하 고 작업 tooall hello 클러스터 생성 된 관계 없이 HDInsight 클러스터를 제출할 수 있습니다.
* 추가 IntelliSense 지원 및 Hive 메타데이터 로드 속도 개선(향상)
  
    추가 사용자에 게 친숙 제안을 추가 하 여 hello IntelliSense를 개선 했습니다. 예를 들어 이제 테이블 별칭도 IntelliSense에서 제안되므로 쿼리를 보다 쉽게 작성할 수 있습니다. 또한 hello 하이브 메타 데이터를 개선 했습니다 모든 hello 데이터베이스, 테이블 및 열 하이브 metastore의 toolist 초 여러 걸립니다만 있도록 로드 합니다.

HDInsight 도구 업데이트에 대한 자세한 내용은 [이 블로그](http://go.microsoft.com/fwlink/?LinkId=623831)를 참조하세요.

### <a name="improvements-in-visual-studio-2013"></a>Visual Studio 2013의 향상된 기능
* Azure SDK 2.7.1 Visual Studio 2013 tooaccess Azure 계정 및 구독을 통해 역할 기반 액세스 제어, 클라우드 솔루션 공급자 및 Dreamspark를 사용 합니다.
* Azure sdk 2.7.1 hello 새 클라우드 탐색기 도구 창 이기도 이제 Visual Studio 2013에서 사용할 수 있습니다.

### <a name="known-issues"></a>알려진 문제
Azure SDK 2.6 hello 또는 2.7.1 용 설치 Visual Studio Community 2013에는 비-영어 버전 운영 체제에서 영어 hello 경고가 표시 됩니다 및 Visual Studio의 영어 이외의 리소스 일치 않을 수 있습니다. 이 경고는 해제해도 됩니다. Hello 컴퓨터는 이전 Visual Studio Community 2013 설치를 포함 하지 않고 한 hello SDK에는 비-영어 버전 운영 체제 설치 하려는 경우에 발생 합니다. 하지만 업데이트 4를 적용 하기 전에 hello 언어 팩 hello RTM 리소스 tooVisual Studio 적용 한 후 hello 경고가 표시 됩니다. Hello 경고를 해제 하면 hello 언어 팩 toocontinue 및 적용 하는 전체 업데이트 4 hello 버전 hello 언어 팩을 콘텐츠입니다.

LightSwitch 프로젝트는 이 릴리스와 호환되지 않습니다. 이 문제는 다음 SDK 릴리스 hello로 확인 됩니다.

## <a name="also-see"></a>참고 항목
[Azure SDK 2.7.1 발표 게시물](http://go.microsoft.com/fwlink/?LinkId=623850)

[Azure SDK 2.7 발표 게시물](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/)

[지원 및 hello Azure SDK for.NET 및 Api에 대 한 사용 중지 정보](https://msdn.microsoft.com/library/azure/dn479282.aspx/)


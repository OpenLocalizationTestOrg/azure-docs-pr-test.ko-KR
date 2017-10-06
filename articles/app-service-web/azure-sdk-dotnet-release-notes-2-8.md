---
title: "aaaAzure SDK for.NET 2.8 릴리스 정보"
description: "Azure SDK for .NET 2.8 릴리스 정보"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: de7207ff-ba4f-4008-9141-8742fcaa3254
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 2722dcdd27bf9ab65b48e91dcdb545536f987dd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-28-281-and-282"></a>Azure SDK for .NET 2.8, 2.8.1, 2.8.2
## <a name="overview"></a>개요
이 문서는 2.8.1 및 2.8.2.NET 2.8 릴리스를 hello Azure SDK에 대 한 hello 릴리스 정보 (즉 알려진된 문제 및 주요 변경 내용 포함)를 포함 합니다. 

새로운 기능 및 이번 릴리스에서 업데이트의 전체 목록은 참조 hello [Visual Studio 2013 및 Visual Studio 2015 용 Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/) 공지 합니다. 

## <a name="azure-sdk-for-net-28"></a>Azure SDK for .NET 2.8
### <a name="download-azure-sdk-for-net-28"></a>Azure SDK for .NET 2.8 다운로드
[Visual Studio 2015용 Azure SDK for .NET 2.8](http://go.microsoft.com/fwlink/?LinkId=699285) 

[Visual Studio 2013용 Azure SDK for .NET 2.8](http://go.microsoft.com/fwlink/?LinkId=699287)

### <a name="net-452-support"></a>.NET 4.5.2 지원
#### <a name="known-issues"></a>알려진 문제
Azure.NET SDK 2.8 있습니다 toocreate.NET 4.5.2 클라우드 서비스 패키지를 수 있습니다. 그러나.NET 4.5.2에 게스트 OS 이미지 될 때까지 2016 년 1 월 게스트 OS 릴리스 hello 기본 프레임 워크 설치 되지 것입니다. 그전에는 .NET 4.5.2 프레임워크를 별도 게스트 OS 릴리스 버전(2015년 11월-02)을 통해 사용할 수 있습니다. Hello 참조 [Azure 게스트 OS 릴리스 및 SDK 호환성 매트릭스](../cloud-services/cloud-services-guestos-update-matrix.md) 페이지 tootrack 때 hello 이미지를 출시 될 예정입니다.  Hello 년 11 월 2015-02 이미지 해제 되 면 선택할 수 있습니다 toouse 이미지 클라우드 서비스 구성 파일 (.cscfg) 파일을 업데이트 하 여. Hello 서비스 구성 파일 설정 hello ServiceConfiguration 요소 toohello 문자열의 hello osVersion 특성 "WA-게스트-OS-4.26_201511-02"입니다. 이 이미지에 toouse tooopt을 선택 하면 다음 더 이상 받아볼 수 게스트 OS 자동 업데이트 toohello 없습니다. tooget hello 자동 업데이트 hello osVersion 너무 설정 해야 합니다 "*"와.NET 4.5.2는 2016 년 1 월에서에서 자동 업데이트를 통해 사용할 수 있습니다.

### <a name="azure-data-factory"></a>Azure 데이터 팩터리
#### <a name="known-issues"></a>알려진 문제
중는 **데이터 팩터리 템플릿** 프로젝트 만들기와 관련 된 샘플 데이터를 azure 파워 셸 스크립트 hello 컴퓨터에 설치 된 azure power shell 버전 0.9.8 이후에 경우 실패할 수 있습니다.

설치 해야 합니다 toosuccessfully 순서 대로 이러한 유형의 프로젝트를 만들 [azure power shell 버전 0.9.8](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi)합니다.

### <a name="azure-resource-manager-tools"></a>Azure 리소스 관리자 도구
#### <a name="breaking-changes"></a>주요 변경 내용
hello hello Azure 리소스 그룹 프로젝트에서 제공 하는 PowerShell 스크립트에서이 릴리스 toowork hello 새 Azure PowerShell cmdlet 버전 1.0으로 업데이트 되었습니다.  이 새 스크립트에서 작동 하지 않습니다 Visual Studio와 함께 hello SDK 이전 too2.8의 버전을 사용 하는 경우.  

Hello SDK의 이전 버전에서 만든 프로젝트에서 스크립트 실행 되지 않습니다에서 Visual Studio 내에서 2.8 SDK hello를 사용 하는 경우.  모든 스크립트 hello 적절 한 버전의 Azure PowerShell cmdlet hello와 Visual Studio 외부에서 toowork를 계속 됩니다.  

hello 2.8 SDK 버전 1.0의 필요 hello Azure PowerShell cmdlet.  다른 모든 버전의 SDK hello 버전 0.9.8 hello Azure PowerShell cmdlet의가 필요 합니다.  자세한 내용은 [이 블로그](http://go.microsoft.com/fwlink/?LinkID=623011) 를 참조하세요.

### <a name="web-tools-extensions"></a>웹 도구 확장
#### <a name="known-issues"></a>알려진 문제
알려진된 문제에 따라 hello 출시 hello에서 해결 될 것입니다.

* 비프로덕션 환경(예: Azure China 또는 Azure 스택 고객)에서는 앱 서비스 관련 클라우드 및 서버 탐색기 제스처가 작동하지 않습니다. 고객에 게 이러한 영향을 받는 영역 hello 다운로드 게시에 대 한 hello Azure 포털에서에서 프로 파일 게시 기능을 활성화할 됩니다. 향후 릴리스에서 Azure China 및 스택 고객에 대한 "디버거 연결" 및 "스트리밍 로그 보기"와 같은 제스처가 복구됩니다. 
* 고객은 hello App Insights 인스턴스 toowhich 배포 하는 경우 작성 미국 동부 지역 하는 응용 프로그램 서비스 하는 동안 오류가 표시 될 수 있습니다. 이러한 시나리오에서는 hello 포털에서 응용 프로그램 서비스를 만드는 게시 다운로드 하 고 hello 프로필 게시 시나리오를 사용 하도록 설정 됩니다. 

### <a name="azure-hdinsight-tools"></a>Azure HDInsight 도구
#### <a name="new-updates"></a>새 업데이트
* 오버 헤드 없음 거의 HiveServer2 통해 hello 클러스터에서 하이브 쿼리를 실행 하 고 hello 작업 기록 실시간으로 확인할 수 있습니다.
* Hello를 사용 하 여 새 하이브 태스크 실행 보기 아래 인 작업을 살펴볼 수 있습니다 자세한 정보를 찾아 잠재적인 문제를 식별 합니다.

자세한 내용은 [Visual Studio 2013 및 Visual Studio 2015용 Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)을 참조하세요. 

## <a name="azure-sdk-for-net-281"></a>Azure SDK for .NET 2.8.1
### <a name="known-issues-for-visual-studio-2013-and-visual-studio-2015"></a>Visual Studio 2013 및 Visual Studio 2015에 대해 알려진 문제
1. 트리거된 WebJob 게시 tooslots가 표시 및 오류 않습니다 일정을 설정 하지만 푸시합니다 hello WebJob tooAzure 합니다. 고객은 예약 된 작업을 수행 해야 WebJob hello에 대 한 hello Azure 포털 tooset hello 일정을 유도할 수 있습니다. 
2. Python 고객에게 디버거 문제가 발생할 수 있습니다. 서비스 팀은이 대 한 수정 프로그램이 롤아웃하기 있지만 고객에 영향을 받는 경우 Microsoft hello 알림 블로그 또는 hello 포럼에서 모르거나 릴리스 노트 설명 섹션을 알려 주세요. 
3. 특정 지역(예: 인도 남부)의 고객에게 앱 서비스 프로비저닝 오류가 발생합니다. Hello 포털과 일치 이며이 문제가 발생 하는 고객 hello Azure 포털 toorequest 액세스 toopublish toothese 지리적 영역을 사용할 수 있습니다. 사용 하 여 액세스 toothese 영역 요청할 hello Azure 포털 프로 비전 작동 합니다. 

## <a name="azure-sdk-for-net-282"></a>Azure SDK for .NET 2.8.2
Hello 2.8.2 도구의 hello 설치 후 고객 hello 다음 문제가 발생할 수 있습니다.         

* Internet Explorer를 설치하지 않고 Windows 10을 사용하는 경우 "Internet Explorer를 찾을 수 없습니다"라는 오류가 발생할 수 있습니다.
  tooresolve hello 문제 추가 hello를 사용 하 여 Internet Explorer를 설치/Windows 구성 요소 대화 상자를 제거 합니다.

이 문제를 발견 될 경우 사용 하 여 hello 웃는 얼굴 보내기 a 기능 tooreport 것입니다.

자세한 내용은 [이 게시물](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-2-for-net/) 을 참조하세요.

## <a name="other-updates"></a>다른 업데이트
다른 업데이트는 [Azure SDK 2.8 발표 게시물](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)을 참조하세요.

## <a name="also-see"></a>참고 항목
[Azure SDK 2.8 발표 게시물](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)

[지원 및 hello Azure SDK for.NET 및 Api에 대 한 사용 중지 정보](https://msdn.microsoft.com/library/azure/dn479282.aspx)


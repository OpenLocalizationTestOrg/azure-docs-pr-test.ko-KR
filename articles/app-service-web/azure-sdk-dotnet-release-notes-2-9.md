---
title: "aaaAzure SDK for.NET 2.9 릴리스 정보"
description: "Azure SDK for .NET 2.9 릴리스 정보"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a>Azure SDK for .NET 2.9 릴리스 정보

이 항목에는 Azure SDK for .NET 버전 2.9 및 2.9.6에 대한 릴리스 정보가 포함되어 있습니다.

##<a name="azure-sdk-for-net-296-release-summary"></a>Azure SDK for .NET 2.9.6 릴리스 요약

릴리스 날짜: 11/16/2016
 
이 릴리스의 Azure SDK 2.9 없음 주요 변경 내용 toohello 도입 되었습니다. 기존 클라우드 서비스 프로젝트와 함께이 SDK 필요한 업그레이드 프로세스 tooleverage 하지도 않습니다.

### <a name="visual-studio-2017-release-candidate"></a>Visual Studio 2017 릴리스 후보

- Visual Studio 2017 RC에서 hello Azure 작업에서에서이 릴리스의 hello Azure SDK for.NET에 작성 됩니다. Toodo Azure 개발 해야 하는 모든 hello 도구에는 앞으로 Visual Studio 2017 RC의 일부가 됩니다. Visual Studio 2015 및 Visual Studio 2013에 대 한 hello SDK WebPI를 통해 사용할 수 있습니다. Visual Studio 2017이 최종 제품으로 출시될 때는 Visual Studio 2013용 Azure SDK for .NET 릴리스가 중단될 것입니다. 이 링크 toodownload Visual Studio 2017 RC에 따라: https://www.visualstudio.com/vs/visual-studio-2017-rc/

### <a name="azure-diagnostics"></a>Azure 진단

- 변경 된 hello 동작 tooonly 클라우드 서비스 진단 저장소 연결 문자열에 대 한 토큰으로 대체 하는 hello 키가 있는 부분 연결 문자열을 저장 합니다. 이제 hello 실제 저장소 키가 액세스 권한을 제어할 수 있도록 hello 사용자 프로필 폴더에 저장 됩니다. Visual Studio는 로컬 디버깅 및 게시 프로세스에 대 한 사용자 프로필 폴더에서 hello 저장소 키를 읽습니다. 
- 위에서 설명한 응답 toohello 변경에서 Visual Studio Online 팀 향상 된 hello Azure 클라우드 서비스 배포 작업 템플릿을 있으므로 사용자가 tooAzure 연속 통합에 게시할 때 진단 확장을 설정 하기 위한 hello 저장소 키를 지정할 수 있습니다. 및 배포 합니다.
- 만들었고 가능한 toostore 보안 연결 문자열 및 토큰화에 대 한 WAD (Azure 진단), toohelp environements에서 구성 사용 하 여 문제를 해결 합니다.
 
### <a name="windows-server-2016-virtual-machines"></a>Windows Server 2016 가상 컴퓨터

- 이제 visual Studio 배포 클라우드 서비스 tooOS 제품군 5 (Windows Server 2016) 가상 컴퓨터를 지원합니다. 기존 클라우드 서비스에 대 한 설정을 tootarget를 변경할 수 있습니다 hello 새 OS 제품군입니다. 새 클라우드 서비스를.net 4.6 이상이 사용 하 여 toocreate hello 서비스를 선택 하는 경우 만들 때 hello 서비스 toouse OS 제품군 5 기본값이 지정 됩니다.  자세한 내용은 hello를 검토할 수 있습니다 [게스트 OS 제품군 지원 테이블](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/)합니다.

#### <a name="known-issues"></a>알려진 문제

- Azure.NET SDK 2.9.6 지원 되지 않는.NET 프레임 워크 (예:.NET 4.6) tooany OS 제품군을 사용 하 여 프로젝트의 배포를 차단 하는 제한 도입 < 5입니다. 해결 방법이 [여기](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9)에 제공됩니다.

 
### <a name="azure-in-role-cache"></a>Azure In-Role Cache 

- Azure In-Role Cache에 대한 지원은 2016년 11월 30일에 종료됩니다. 자세한 내용을 보려면 [여기](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)를 클릭하세요.

### <a name="azure-resource-manager-templates-for-azure-stack"></a>Azure Stack용 Azure Resource Manager 템플릿

- Azure Resource Manager 템플릿에 대한 배포 대상으로 Azure Stack을 도입했습니다.


## <a name="azure-sdk-for-net-29-summary"></a>Azure SDK for .NET 2.9 요약

## <a name="overview"></a>개요
이 문서는 Azure SDK 2.9.NET 릴리스에 대 한 hello에 대 한 hello 릴리스 정보를 포함합니다. 

이 릴리스에서 업데이트에 대 한 자세한 내용은 참조 hello [Azure SDK 2.9 공지 게시물](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)합니다.

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a>Visual Studio 2015 업데이트 2 및 Visual Studio "15" Preview용 Azure SDK 2.9
이 업데이트는 버그 수정 다음 hello를 포함 합니다.

* 실행 관련된 tooREST API 클라이언트 생성에는 hello 문자열에 "알 수 없는 형식입니다" 나타났습니다 hello 코드 생성 폴더의 hello 이름 및/또는 hello 생성 된 코드를 삭제 하는 hello 네임 스페이스의 hello 이름으로 합니다.
* hello에 인증 정보 실패 한 toobe toohello 스케줄러 프로 비전 프로세스를 전달 하는 관련된 tooScheduled WebJobs를 실행 합니다.

이 업데이트는 새로운 기능을 수행 하는 hello를 포함 합니다.

* 앱 서비스 프로 비전 대화 상자 hello의 hello "서비스" 탭에서 보조 응용 프로그램 서비스에 대 한 지원. 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a>Visual Studio 2015 업데이트 2용 Azure Data Lake 도구
이 업데이트 hello 다음이 포함 됩니다.

* **Azure 데이터 레이크 도구** Visual Studio는 이제 Azure SDK.NET 릴리스 hello에 병합 됩니다. hello 도구는 Azure SDK를 설치할 때 자동으로 설치 됩니다. 
  
    hello 도구 자주 업데이트 되는, 이동 [여기](http://aka.ms/datalaketool) tooget hello 업데이트 합니다.
* **서버 탐색기** 이제 모든 tooview 있으며 일부 U-SQL 메타 데이터 엔터티를 만듭니다. 자세한 내용은 [이 블로그](https://azure.microsoft.com/documentation/services/data-lake-analytics/) 를 참조하세요.

## <a name="hdinsight-tools"></a>HDInsight 도구
**HDInsight 도구** 에서 Tez 그래프 표시 및 기타 언어 수정을 포함하여 HDInsight 버전 3.3을 지원합니다.

## <a name="azure-resource-manager"></a>Azure 리소스 관리자
이 릴리스는 Resource Manager 템플릿에 대한 [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) 지원을 추가했습니다.

## <a name="see-also"></a>참고 항목
[Azure SDK 2.9 발표 게시물](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)


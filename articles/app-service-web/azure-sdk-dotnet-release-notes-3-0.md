---
title: "aaaAzure SDK for.NET 3.0 릴리스 정보 | Microsoft Docs"
description: "Azure SDK for .NET 3.0 릴리스 정보"
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
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: 8970b4c9b64de40dc29a33d69006a00ae5e38a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a>Azure SDK for .NET 3.0 릴리스 정보

이 항목에 대 한.NET hello Azure SDK의 버전 3.0에 대 한 릴리스 정보를 포함합니다.

##<a name="azure-sdk-for-net-30-release-summary"></a>Azure SDK for .NET 3.0 릴리스 요약

릴리스 날짜: 03/07/2017
 
이 릴리스의 Azure SDK 3.0 없음 주요 변경 내용 toohello 도입 되었습니다. 기존 클라우드 서비스 프로젝트와 함께이 SDK 필요한 업그레이드 프로세스 tooleverage 하지도 않습니다. Azure SDK 3.0 업그레이드 프로세스를 요구 하지 않고 Azure SDK 3.0 hello tooallow 사용 설치 toohello 같은 Azure SDK 2.9 디렉터리입니다. 대부분의 hello 구성 요소 hello 주 버전 2.9에서 변경 되지 않은 하지만 대신 방금 hello 빌드 번호를 업데이트 합니다.

## <a name="visual-studio-2017-rtw"></a>Visual Studio 2017 RTW

- Visual Studio 2017이이 릴리스의 hello Azure SDK for.NET toohello Azure 작업 부하에에서 만들어집니다. Toodo Azure 개발 해야 하는 모든 hello 도구에는 앞으로 Visual Studio 2017의 일부가 됩니다. Visual Studio 2015 용 SDK hello WebPI를 통해 사용할 수 있습니다. 이제 Visual Studio 2017이 릴리스되었으므로 Visual Studio 2013용 Azure SDK for .NET 릴리스는 중단되었습니다.

### <a name="azure-diagnostics"></a>Azure 진단

- 변경 된 hello 동작 tooonly 클라우드 서비스 진단 저장소 연결 문자열에 대 한 토큰으로 대체 하는 hello 키가 있는 부분 연결 문자열을 저장 합니다. 이제 hello 실제 저장소 키가 액세스 권한을 제어할 수 있도록 hello 사용자 프로필 폴더에 저장 됩니다. Visual Studio는 로컬 디버깅 및 게시 프로세스에 대 한 사용자 프로필 폴더에서 hello 저장소 키를 읽습니다. 
- 위에서 설명한 응답 toohello 변경에서 Visual Studio Online 팀 향상 된 hello Azure 클라우드 서비스 배포 작업 템플릿을 있으므로 사용자가 tooAzure 연속 통합에 게시할 때 진단 확장을 설정 하기 위한 hello 저장소 키를 지정할 수 있습니다. 및 배포 합니다.
- 만들었고 가능한 toostore 보안 연결 문자열 및 토큰화에 대 한 WAD (Azure 진단), toohelp environements에서 구성 사용 하 여 문제를 해결 합니다.
 
### <a name="windows-server-2016-virtual-machines"></a>Windows Server 2016 가상 컴퓨터

- 이제 visual Studio 배포 클라우드 서비스 tooOS 제품군 5 (Windows Server 2016) 가상 컴퓨터를 지원합니다. 기존 클라우드 서비스에 대 한 설정을 tootarget를 변경할 수 있습니다 hello 새 OS 제품군입니다. 새 클라우드 서비스를.net 4.6 이상이 사용 하 여 toocreate hello 서비스를 선택 하는 경우 만들 때 hello 서비스 toouse OS 제품군 5 기본값이 지정 됩니다.  자세한 내용은 hello를 검토할 수 있습니다 [게스트 OS 제품군 지원 테이블](../cloud-services/cloud-services-guestos-update-matrix.md)합니다.

### <a name="known-issues"></a>알려진 문제

- Azure .NET SDK 3.0에는 Visual Studio 2015와의 병렬 구성에서 Visual Studio 2017을 제거할 경우 문제가 소개되었습니다.  Hello Azure SDK가 Visual Studio 2015 용 설치 되어 있는 경우 Microsoft Azure 저장소 에뮬레이터 hello 및 Microsoft Azure 계산 에뮬레이터를 제거할 Visual Studio 2017을 제거 하는 경우.  이로 인해 Visual Studio 2015에서 새 클라우드 서비스 프로젝트를 만들고 디버그할 때 오류가 발생합니다. 주문 toofix이이 문제에 hello 웹 플랫폼 설치 관리자에서에서 Azure SDK hello를 다시 설치 하십시오.  hello 문제가 해결 될 것에 이후 Visual Studio 2017 업데이트 합니다.  에서도 확인할 수 있습니다.

 
### <a name="azure-in-role-cache"></a>Azure In-Role Cache 

- Azure In-Role Cache에 대한 지원은 2016년 11월 30일에 종료되었습니다. 자세한 내용을 보려면 [여기](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)를 클릭하세요.





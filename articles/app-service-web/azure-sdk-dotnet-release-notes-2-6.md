---
title: "aaaAzure SDK for.NET 2.6 릴리스 정보"
description: "Azure SDK for .NET 2.6 릴리스 정보"
services: app-service/web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: b45853d5-a2b8-4962-a22d-579cb36ae14c
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: ac613cf20da4f731fab6f35ccbf6dbeaf18c0ec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-26-release-notes"></a>Azure SDK for .NET 2.6 릴리스 정보
이 문서는 Azure SDK 2.6.NET 릴리스에 대 한 hello에 대 한 hello 릴리스 정보를 포함합니다. 

Azure SDK 2.6으로 클라우드 서비스 응용 프로그램 (PaaS) hello 클라우드 서비스 역할에.NET Framework를 대상으로 hello를 수동으로 설치 된.NET 4.5.2 또는.NET 4.6을 대상으로 개발할 수 있습니다. [클라우드 서비스 역할에 .NET 설치](http://go.microsoft.com/fwlink/?LinkID=309796)를 참조하세요.

## <a name="service-bus-updates"></a>서비스 버스 업데이트
* 이벤트 허브: 
  
  * 이제 이벤트를 보낼 때 이벤트 허브에 대한 추가 게시자 끝점을 노출하여 대상별 액세스를 제어할 수 있습니다.
  * 추가 안정성 및 개선 tooEvent 허브 기능을 추가 합니다.
  * 메시징용 WebSocket 및 이벤트 허브를 통해 Amqp 프로토콜을 추가로 지원합니다.

## <a name="hdinsight-tools-for-visual-studio-updates"></a>Visual Studio용 HDInsight 도구 업데이트
* **IntelliSense 향상 기능**: 원격 메타데이터 제안
  
    이제 Visual Studio용 HDInsight 도구에서 하이브 스크립트를 편집할 때 원격 메타데이터 가져오기를 지원합니다. 예를 들어 입력할 수 있습니다 **선택 * FROM** 과 모든 hello 테이블 이름이 표시 됩니다. 또한 hello 열 이름은 테이블을 지정한 후 표시 됩니다.
* **HDInsight Emulator 지원**
  
    이제 HDInsight Tools for Visual Studio 지원 tooHDInsight 에뮬레이터를 연결 하는 비용을 일으키지 않고 로컬로 하이브 스크립트를 개발할 수 있습니다 다음 HDInsight 클러스터에 대해 이러한 스크립트를 실행 합니다. 
  
    자세한 내용은 참조 너무[이 수동](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409)합니다.
* **일반 Hadoop 클러스터에 대한 Visual Studio용 HDInsight 도구 지원** (미리 보기)
  
    이제 Visual Studio 용 HDInsight 도구는 Visual Studio toodo hello 다음에 대 한 HDInsight 도구를 사용할 수 있도록 제네릭 Hadoop 클러스터를 지원 합니다.
  
  * tooyour 클러스터에 연결 
  * 향상된 IntelliSense/자동 완성 지원으로 하이브 쿼리 작성 
  * 직관적인 UI로 클러스터의 모든 hello 작업을 봅니다. 
    
    자세한 내용은 참조 너무[이 수동](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409)합니다.

## <a name="in-role-cache-updates"></a>In-Role Cache 업데이트
* **역할 내 캐시** 가 업데이트 된 toouse **Microsoft Azure 저장소 SDK** 버전 4.3 합니다. 지금까지 hello **In-role Cache** 사용 하 여 Azure 저장소 SDK 버전 1.7 되었습니다.
  
    Azure SDK 2.5를 사용 하 여 또는 아래 해야 tooAzure SDK 2.6 업데이트 고객과 toohello 새로운 버전의 Azure 저장소 SDK를 이동 합니다. 
  
    이 시간 Azure 저장소 버전 2011-08-18는 2016 년 8 월 1 일을 제거 하는 예약 된 toobe 유지 됩니다. 이 시간까지 too2.6 아래 또는 Azure SDK 2.5에서 역할 내 캐시의 모든 마이그레이션을 완료 해야 합니다. Azure 저장소 2011-08-18 버전의 hello 사용 중지에 대 한 자세한 내용은 참조 하십시오. [Microsoft Azure 저장소 서비스 버전 제거 업데이트: 확장 too2016](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx)합니다.

> [!IMPORTANT]
> 발표 hello 2016 년 11 월 30 일 Azure 관리 캐시 서비스 및 Azure 역할 내 캐시에 대 한 사용 중지 합니다. 이 사용 중지에 대 한 준비 과정에서 Redis Cache tooAzure 마이그레이션하는 것이 좋습니다. 날짜 및 마이그레이션 지침에 대한 자세한 내용은 [내게 적합한 Azure 캐시 제품은 무엇인가요?](../redis-cache/cache-faq.md#which-azure-cache-offering-is-right-for-me)
> 
> 

## <a name="azure-app-service-tools"></a>Azure 앱 서비스 도구
다음 항목 hello hello Azure SDK 2.6 버전에서 업데이트 되었습니다.

* Azure 게시를 배포 대상으로 tooinclude Azure API 앱을 향상 합니다.
* API 앱 API 앱 작성 기능 tooenable 사용자를 프로 비전 및 기능을 제공 합니다.
* 서버 탐색기 변경 tooreflect 새 앱 서비스 노드를 리소스 그룹으로 그룹화 하는 웹, 모바일 및 API 앱.
* Azure API 앱 클라이언트 제스처 추가 하는 toomost C# 프로젝트 추가 Swagger 사용이 가능한 API는 사용자의 Azure 구독에서 실행 되는 앱의 자동 생성을 사용 하도록 설정 합니다.
* 서버 탐색기의 API 앱 도구 및 앱 서비스 노드는 Visual Studio 2013에서만 사용할 수 있습니다. 

## <a name="azure-resource-manager-tools-updates"></a>Azure 리소스 관리자 도구 업데이트
hello Azure 리소스 관리자 도구에는 가상 컴퓨터, 네트워킹 및 저장소에 대 한 업데이트 된 tooinclude 템플릿이 되었습니다. hello JSON 편집 환경을 업데이트 tooinclude 서식 파일 및 JSON 조각을 사용 하 여 hello 기능 tooedit hello 템플릿에 대 한 새 개요 보기 되었습니다. Visual Studio에서 배포 하는 템플릿은 않으므로 Visual Studio에서 사용 됩니다. 변경 내용을 toohello 스크립트 hello 프로젝트에서 제공 하는 PowerShell 스크립트를 사용 합니다.

## <a name="diagnostics-improvements-for-cloud-services"></a>클라우드 서비스에 대한 향상된 진단 기능
Azure SDK 2.6 저항력 hello Azure 계산 에뮬레이터에서 진단 로그를 수집 하 고 전송에 대 한 지원을 toodevelopment 저장소입니다. 응용 프로그램 추적 로그, 이벤트 로그 및 windows 이벤트 로그를 ETW (Windows) 로그, 성능 카운터, 인프라에 대 한 추적) (포함 진단 로그 생성 hello 응용 프로그램 hello 에뮬레이터에서 실행 중인 경우 수 전송된 toodevelopment 로컬 컴퓨터에서 진단 로깅이 작동 하는 저장소 tooverify 합니다. 

hello 진단 저장소 계정이 서로 다른 환경에 대 한 보다 쉽게 toouse 여러 진단 저장소 계정을 만드는 hello 서비스 구성 (.cscfg) 파일에 이제 지정할 수 있습니다. Hello 연결 문자열이 Azure SDK 2.4 및 Azure SDK 2.6에서 작동 하는 방법의 몇 가지 주목할 만한 차이점 있습니다. Toouse hello 진단 저장소 연결 문자열 및 프로젝트에 미치는 영향에 참조 하는 방법에 대 한 자세한 내용은 [Azure 클라우드 서비스에 대 한 진단 구성](http://go.microsoft.com/fwlink/?LinkID=532784)합니다.

## <a name="breaking-changes"></a>주요 변경 내용
### <a name="azure-resource-manager-tools"></a>Azure 리소스 관리자 도구
* hello **클라우드 배포 프로젝트** 프로젝트 hello Azure SDK 2.5 너무 바뀐에서 사용할 수 있는 형식을**Azure 리소스 그룹**합니다.
* **클라우드 배포 프로젝트** 2.6에서 hello Azure SDK 2.5에서에서 만든 프로젝트의 종류를 사용할 수 있지만 hello 템플릿을 Visual Studio에서 배포에 실패 합니다. 그러나 hello PowerShell 스크립트를 사용 하 여 배포가 이전 처럼 작동 계속 합니다.  방법에 대 한 내용은 toouse **클라우드 배포 프로젝트** 이 내용을 읽고 2.6 [게시](http://go.microsoft.com/fwlink/?LinkID=534086)합니다.

## <a name="known-issues"></a>알려진 문제
* 64 비트 운영 체제 필요 hello 에뮬레이터에서 진단 로그를 수집 합니다. 32비트 운영 체제에서 실행할 때는 진단 로그가 수집되지 않습니다. 다른 에뮬레이터 기능은 영향을 받지 않습니다. 
* 2015/04/29에 릴리스된 Azure SDK 2.6의 두 가지 문제: 
  
  * Azure SDK 2.6 hello 컴퓨터에 설치 될 때 Visual Studio 2015에서 유니버설 앱을 로드할 수 없습니다.
  * 클라우드 서비스 프로젝트를 디버깅 하는 Visual Studio 2013과 Visual Studio 2015 Visual Studio 응답 하지 않거나 하 고 "에뮬레이터에 대 한 진단 구성" hello 메시지와 함께 대화 상자를 표시 하는 동안 충돌 하는 위치에 실패 합니다.
    
    업데이트 tooAzure SDK 2.6 2015 년 5 월 18 일에 출시 되었습니다. hello 업데이트 버전은 2.6.30508.1601; 위에서 설명한 두 가지 문제에 대 한 수정 포함 됩니다. Hello의 hello 빌드를 식별할 수 있습니다. Control Panel에서 SDK-> 프로그램 및 기능에 Microsoft Visual Studio 2013-v 2.6에 대 한 Microsoft Azure 도구->. hello 버전 열 hello 빌드 번호를 표시 됩니다.
    
    설치 hello 최신 버전의 hello에 대 한 Azure 2.6 SDK 문제 위에 hello, 직면 여전히 하는 경우 [VS 2012](http://go.microsoft.com/fwlink/p/?linkid=323511&clcid=0x409), [VS 2013](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) 또는 [VS 2015](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)합니다.

## <a name="see-also"></a>참고 항목
[지원 및 hello Azure SDK for.NET 및 Api에 대 한 사용 중지 정보](https://msdn.microsoft.com/library/azure/dn479282.aspx/)


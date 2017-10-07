---
title: "Azure 앱 서비스에서 aaaOperating 시스템 기능"
description: "Hello OS 기능 사용 가능한 tooweb 앱, 모바일 앱 백 및 Azure 앱 서비스 API 앱에 대 한 자세한 내용은"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 39d5514f-0139-453a-b52e-4a1c06d8d914
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 695188c48102b10ece326fba8d50a5f55b03b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="operating-system-functionality-on-azure-app-service"></a>Azure 앱 서비스의 운영 체제 기능
이 문서에서는 hello 공용 기준 운영 체제 기능을 사용할 수 있는 tooall 앱에서 실행 되는 설명 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)합니다. 이 기능에는 파일, 네트워크, 레지스트리 액세스, 진단 로그 및 이벤트가 포함됩니다. 

<a id="tiers"></a>

## <a name="app-service-plan-tiers"></a>앱 서비스 계획 계층
앱 서비스는 다중 테넌트 호스팅 환경에서 고객 앱을 실행합니다. Hello에 배포 된 앱 **무료** 및 **Shared** 앱 hello에 배포 하는 동안 공유 가상 컴퓨터에서 작업자 프로세스에서 실행 하는 계층 **표준** 및  **프리미엄** 특히 단일 고객과 관련 된 hello 앱에 대 한 전용 가상 컴퓨터에서 계층을 실행 합니다.

앱 서비스에서 다른 계층 간에 원활 하 게 확장 경험을 지원 하므로 hello 보안 구성에는 적용 앱 서비스 앱은 유지 hello에 대 한 동일 합니다. 이렇게 하면 있는지 앱 하지 갑자기 다르게 동작할 때 실패 하는 예기치 않은 방법으로 하나의 계층 tooanother에서 전환 되는 앱 서비스 계획 합니다.

<a id="developmentframeworks"></a>

## <a name="development-frameworks"></a>개발 프레임워크
앱 서비스 가격 계산 리소스 (CPU, 디스크 저장소, 메모리 및 네트워크 송신) 양을 제어 hello 계층 tooapps 사용할 수 있습니다. 그러나 hello 다양 한 프레임 워크 기능 사용 가능한 tooapps 남아 hello 계층 크기 조정 hello와 관계 없이 동일 합니다.

앱 서비스는 ASP.NET, 클래식 ASP, node.js, PHP, Python을 포함하여 다양한 개발 프레임워크를 지원합니다. 이 프레임워크는 모두 IIS 내에서 확장으로 실행됩니다. 순서 toosimplify에서 및 보안 구성 정규화, 앱 서비스 앱 일반적으로 hello 다양 한 개발 프레임 워크의 기본 설정으로 실행 합니다. 한 가지 방법은 tooconfiguring 앱 toocustomize hello API 노출 영역 및 각 개별 개발 프레임 워크에 대 한 기능 있었습니다. 대신 앱 서비스는 앱의 개발 프레임워크에 관계없이 일반적인 기준 운영 체제 기능을 사용하여 보다 일반적인 접근 방식을 취합니다.

hello 다음 섹션에 요약 되어 hello 일반적인 종류의 서비스 응용 프로그램을 사용할 수 있는 tooApp 운영 체제 기능입니다.

<a id="FileAccess"></a>

## <a name="file-access"></a>파일 액세스
앱 서비스에는 로컬 드라이브와 네트워크 드라이브를 포함한 다양한 드라이브가 있습니다.

<a id="LocalDrives"></a>

### <a name="local-drives"></a>로컬 드라이브
본질적으로 앱 서비스는 hello Azure PaaS (platform 서비스로) 인프라를 기반으로 실행 하는 서비스. 결과 있는 로컬 드라이브를 hello "연결" tooa 가상 컴퓨터는 hello 동일한 드라이브 형식을 사용할 수 있는 tooany 작업자 역할 Azure에서 실행 합니다. 여기에 운영 체제 드라이브 (D:\ 드라이브 hello), 응용 프로그램 서비스 (및 액세스할 수 없는 toocustomers) 단독으로 사용 되는 Azure 패키지 cspkg 파일을 포함 하는 응용 프로그램 드라이브 및 hello 크기에 따라 크기가 달라 지기 "user" 드라이브 (C:\ 드라이브 hello) VM hello 합니다.

<a id="NetworkDrives"></a>

### <a name="network-drives-aka-unc-shares"></a>네트워크 드라이브(일명 UNC 공유)
앱 서비스 앱 배포 및 유지 관리를 간소화 하는 경우의 hello 고유한 측면 중 하나는 모든 사용자 콘텐츠 집합이 UNC 공유에 저장 된입니다. 이 모델에 콘텐츠 저장소 온-프레미스 웹 호스팅 부하 분산 된 서버가 여러 개 있는 환경에서 사용 하는 일반적인 패턴을 toohello 매우 적절 하 게 매핑합니다. 

앱 서비스 내에는 각 데이터 센터에서 만들어진 다수의 UNC 공유가 있습니다. 각 데이터 센터에 있는 모든 고객에 대 한 hello 사용자 콘텐츠의 백분율로 UNC 공유 tooeach를 할당 됩니다. 또한 hello 같은 UNC 공유에 배치 항상 단일 고객의 구독에 대 한 hello 파일 내용을 모두. 

작동 하는 클라우드 서비스 toohow 인해 메모 hello 특정 가상 컴퓨터를 UNC 공유를 호스팅해야 시간이 지남에 따라 변경 됩니다. UNC 공유 하는 동안 클라우드 작업의 정상적인 hello 아래로 가져오는 다른 가상 컴퓨터에서 탑재 됩니다 보장 됩니다. 이러한 이유로 응용 프로그램은 UNC 파일 경로에 hello 컴퓨터 정보 안정적인 시간이 지남에 따라 유지 하도록 하드 코드 된 가정의 만들면 안 됩니다. 대신, hello 편리 하 게 사용 해야 *포* 절대 경로 **D:\home\site** 앱 서비스에서 제공 하 합니다. 이 가상 경로 통해 휴대용, 응용 프로그램 및 사용자 무관 tooone의 응용 프로그램 참조에 있습니다. 사용 하 여 **D:\home\site**, tooconfigure 새 절대 경로 각 전송에 대 한 필요 없이 응용 프로그램 tooapp에서 공유 파일을 전송할 수 있습니다 하나 있습니다.

<a id="TypesOfFileAccess"></a>

### <a name="types-of-file-access-granted-tooan-app"></a>파일 액세스의 유형 부여 tooan 응용 프로그램
각 고객의 구독에는 데이터 센터 내의 특정 UNC 공유에 예약된 디렉터리 구조가 있습니다. 고객이 특정 데이터 센터 내에서 만든 앱을 여러 개 있을 수 있습니다, 그리고 때문에 hello에 생성 된 모든 hello 디렉터리 tooa 단일 고객 구독에 속한 동일한 UNC 공유 합니다. hello 공유 콘텐츠, 오류 및 진단 로그 및 이전 버전의 소스 제어에서 만든 hello 앱에 대 한 같은 디렉터리에 포함 될 수 있습니다. 예상 대로 고객의 응용 프로그램 디렉터리에 읽기 및 쓰기 액세스 hello 응용 프로그램의 응용 프로그램 코드에서 런타임에 사용할 수 있는 합니다.

Hello 로컬 드라이브 연결 응용 프로그램을 실행 하는 toohello 가상 컴퓨터, 앱 서비스는 hello 응용 프로그램별 임시 로컬 저장소에 대 한 C:\ 드라이브에 공간이의 청크를 예약 합니다. 앱 tooits 임시 소유한 모든 읽기/쓰기 액세스할 수 있지만 로컬 저장소에 해당 저장소에 실제로 의도 한 toobe hello 응용 프로그램 코드에서 직접 사용 하지 않습니다. 대신, hello 의도 tooprovide 임시 파일 저장소 IIS 및 웹 응용 프로그램 프레임 워크입니다. 앱 서비스는 hello 양을 임시 로컬 저장소 사용 가능한 tooeach 앱 tooprevent 개별 응용 프로그램에서 과도 한 양의 로컬 파일 저장소를 사용도 제한 됩니다.

앱 서비스의 임시 로컬 저장소를 사용 하는 방법의 두 예제는 hello 임시 ASP.NET 파일 디렉터리 및 IIS에 대 한 hello 디렉터리가 압축 파일입니다. ASP.NET 컴파일 시스템 hello 임시 컴파일 캐시 위치도 hello "Temporary ASP.NET Files" 디렉터리를 사용합니다. IIS는 hello "IIS 임시 압축 된 파일" 디렉터리 압축 toostore 응답 출력을 사용 합니다. 앱 서비스 앱 tooper 임시 로컬 저장소에 파일 사용 (물론 다른)의 두이 형식 모두 다시 매핑됩니다. 이렇게 다시 매핑되면 해당 기능이 예상대로 지속됩니다.

앱 서비스에서 각 응용 프로그램 실행 이라고 하는 임의의 고유한 낮은 권한의 작업자 프로세스 id hello "응용 프로그램 풀 id", 여기에 설명 된 추가: [http://www.iis.net/learn/manage/configuring-security/application-pool-identities ](http://www.iis.net/learn/manage/configuring-security/application-pool-identities). 응용 프로그램 코드는 기본 읽기 전용 액세스 toohello 운영 체제 드라이브 (D:\ 드라이브 hello)에 대 한이 id를 사용합니다. 따라서 응용 프로그램 코드는 일반적인 디렉터리 구조를 나열하고 운영 체제 드라이브에 있는 일반 파일을 읽을 수 있습니다. 파일은 액세스할 수 있으며이 toobe는 다소 광범위 한 액세스 수준을 표시, 동일한 디렉터리 hello 수도 있습니다는 Azure에서 작업자 역할 프로 비전 할 호스 티 드 서비스 되며 hello 드라이브 내용을 읽습니다. 

<a name="multipleinstances"></a>

### <a name="file-access-across-multiple-instances"></a>여러 인스턴스의 파일 액세스
hello 홈 디렉터리는 응용 프로그램의 콘텐츠를 포함 하 고 응용 프로그램 코드 tooit를 작성할 수 있습니다. 모든 인스턴스 hello를 확인할 수 있도록 hello 홈 디렉터리 모든 인스턴스에서 공유는 앱이 여러 인스턴스에서 실행 하는 경우 동일한 디렉터리입니다. 따라서 예를 들어 앱 toohello 홈 디렉터리 업로드 된 파일을 저장 하는 경우 해당 파일은 즉시 사용할 수 있는 tooall 인스턴스입니다. 

<a id="NetworkAccess"></a>

## <a name="network-access"></a>네트워크 액세스
응용 프로그램 코드에서 TCP/IP를 사용할 수 있습니다 및 아웃 바운드 기반 UDP 프로토콜 toomake 네트워크 외부 서비스를 노출 하는 연결 tooInternet 액세스할 수 있는 끝점 있습니다. 앱에 이러한 동일한 프로토콜 tooconnect tooservices 내 Azure &#151; 예를 들어 HTTPS 연결 tooSQL 데이터베이스를 설정 하 여 사용할 수 있습니다.

또한 앱 tooestablish 하나의 로컬 루프백 연결에 대 한 제한 된 기능 및 앱을 해당 로컬 루프백 소켓에서 수신 대기 합니다. 이 기능은 주로 tooenable 응용 프로그램 기능별로의 일부로 로컬 루프백 소켓에서 수신 대기 하는 존재 합니다. 각 응용 프로그램에는 "private" 루프백 연결; 게 표시 하는 참고 응용 프로그램 "A"는 "B" 응용 프로그램에서 설정한 tooa 로컬 루프백 소켓을 수신할 수 없습니다.

전체적으로 앱을 실행하는 다양한 프로세스 사이의 IPC(프로세스 간 통신) 메커니즘으로 명명된 파이프도 지원됩니다. 예를 들어 hello IIS FastCGI 모듈 PHP 페이지를 실행 하는 toocoordinate hello 개별 프로세스 명명 된 파이프에 의존 합니다.

<a id="Code"></a>

## <a name="code-execution-processes-and-memory"></a>코드 실행, 프로세스 및 메모리
앞에서 설명했듯이, 앱은 임의의 응용 프로그램 풀 ID를 사용하여 권한이 낮은 작업자 프로세스 내부에서 실행됩니다. 응용 프로그램 코드에는 CGI 프로세스 또는 다른 응용 프로그램에서 생성 될 수 있는 모든 자식 프로세스와 hello 작업자 프로세스와 관련 된 액세스 toohello 메모리 공간을 있습니다. 그러나 하나의 앱 hello 메모리에 액세스할 수 없습니다 또는 데이터에 있는 경우에 다른 응용 프로그램의 hello 동일한 가상 컴퓨터.

앱은 지원되는 웹 개발 프레임워크에서 작성된 스크립트나 페이지를 실행할 수 있습니다. 앱 서비스는 웹 프레임 워크 설정 toomore 제한 모드 구성 예를 들어, 앱 서비스에서 실행 되는 ASP.NET 앱 것과 반대로 tooa 더 제한 된 권한 모드도 "전체" 신뢰에서 실행 합니다. 클래식 ASP 및 ASP.NET을 포함 하 여 웹 프레임 워크는 hello Windows 운영 체제에서 기본적으로 등록 된 ADO (ActiveX Data Objects)와 같은 프로세스에서 COM 구성 요소 (하지만 프로세스 COM 구성 요소 제한을 초과 하지) 호출할 수 있습니다.

앱은 임의의 코드를 생성하고 실행할 수 있습니다. 앱 toodo 항목에 대 한 허용 되는 명령 셸을 생성 하거나 PowerShell 스크립트를 실행 하는 것입니다. 그러나 않더라도 임의의 코드 및 프로세스는 응용 프로그램 실행 프로그램에서에서 생성 된 수 있으며 스크립트는 여전히 제한 toohello 권한 부여 toohello 부모 응용 프로그램 풀. 예를 들어 응용 프로그램을 생성할 수 아웃 바운드 HTTP 호출을 하는 실행 파일 이지만 해당 NIC에서 가상 컴퓨터의 toounbind hello IP 주소를 시도할 수 없습니다 같은 실행 파일 아웃 바운드 네트워크를 호출 toolow 권한이 필요한 코드를 사용할 수 있지만 가상 컴퓨터에서 네트워크 설정을 tooreconfigure 시도 하려면 관리자 권한이 필요.

<a id="Diagnostics"></a>

## <a name="diagnostics-logs-and-events"></a>진단 로그 및 이벤트
로그 정보는 다른 일련의 데이터 일부 앱 tooaccess 된 시도 합니다. 로그 정보 사용 가능한 toocode 앱 서비스에서 실행 중인 hello 유형은 진단 포함 이며 toohello 쉽게 액세스할 수 있는 앱도 사용 되는 앱에서 생성 되는 정보를 기록 합니다. 

예를 들면 활성 응용 프로그램에서 생성 된 W3C HTTP 로그는 hello 앱에 대해 생성 되는 위치를 공유 hello 네트워크의 로그 디렉터리에 사용할 수 있는 또는 고객이 blob 저장소에서 사용할 수 있는 설정한 W3C 로깅 toostorage 합니다. hello 후자 옵션을 사용 하면 대량의 로그 toobe 네트워크 공유와 연결 된 hello 파일 저장소 제한을 초과 hello 위험 없이 수집 합니다.

비슷한.NET 응용 프로그램의 정보를 기록할 수와 옵션 toowrite hello.NET 추적 및 진단 인프라를 사용 하 여 실시간으로 진단 hello 추적 정보 tooeither hello 응용 프로그램의 네트워크 공유 또는 또는 tooa blob 저장소 위치입니다.

사용할 수 있는 tooapps 없는 진단 로깅 및 추적의 영역은 Windows ETW 이벤트 및 일반 Windows 이벤트 로그 (예: 시스템, 응용 프로그램 및 보안 이벤트 로그의 경우)입니다. ETW 추적 정보 잠재적으로 볼 수 있는 될 수 있으므로 시스템 수준의 (hello 권한이 있는 Acl), 읽기 및 쓰기 액세스 tooETW 이벤트 차단 됩니다. 개발자가 눈에 띄지 해당 API 호출 tooread 및 쓰기 ETW 이벤트 및 일반 Windows 이벤트 로그, toowork 표시 되지만 하기 때문 서비스 응용 프로그램에서는 hello 호출을 "가장"은 toosucceed 표시 되도록 합니다. 실제로 hello 응용 프로그램 코드에 대 한 액세스 toothis 이벤트 데이터가 없습니다.

<a id="RegistryAccess"></a>

## <a name="registry-access"></a>레지스트리 액세스
앱 (전부는 아니지만) 읽기 전용 액세스 toomuch 한 hello 레지스트리 hello 가상 컴퓨터에서 실행 됩니다. 실제로 즉, 읽기 전용 액세스 toohello 로컬 사용자 그룹을 허용 하는 레지스트리 키는 응용 프로그램에서 액세스할 수 있습니다. 읽기 또는 쓰기 액세스에 대 한 현재 지원 되지 않는 hello 레지스트리의 한 영역은 hello HKEY\_현재\_사용자 하이브입니다.

쓰기 액세스 toohello 레지스트리 액세스 tooany 사용자별 레지스트리 키를 포함 하 여 차단 됩니다. Hello 응용 프로그램의 관점에서 toohello 레지스트리 쓰기 액세스 해야 하지 수에 의존 하 여 hello Azure 환경 앱 (보고 수행할 수) 이후 여러 가상 컴퓨터에서 마이그레이션된 합니다. hello 영구만 쓰기 가능 저장소 앱에 종속 될 수 있는 hello 응용 프로그램 서비스 UNC 공유에 저장 된 hello 앱 별 콘텐츠 디렉터리 구조입니다. 

## <a name="more-information"></a>자세한 정보

[Azure 웹 앱 샌드박스](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox) -앱 서비스의 실행 환경 hello에 대 한 최신 정보를 대부분 hello 합니다. 이 페이지는 hello 앱 서비스 개발 팀에서 직접 유지 됩니다.

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 



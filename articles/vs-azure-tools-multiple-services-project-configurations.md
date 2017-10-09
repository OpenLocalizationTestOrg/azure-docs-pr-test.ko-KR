---
title: "aaaConfiguring 여러 서비스 구성을 사용 하 여 Azure 프로젝트 | Microsoft Docs"
description: "Tooconfigure Azure hello ServiceDefinition.csdef와 ServiceConfiguration.cscfg 파일을 변경 하 여 서비스 프로젝트를 클라우드 하는 방법에 대해 알아봅니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a4fb79ed-384f-4183-9f74-5cac257206b9
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 14222266093eb876db0ac9ce8d3d17a04c65d1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-your-azure-project-using-multiple-service-configurations"></a>여러 서비스 구성을 사용하여 Azure 프로젝트 구성
Azure 클라우드 서비스 프로젝트에는 ServiceDefinition.csdef 및 ServiceConfiguration.cscfg의 두 가지 구성 파일이 포함됩니다. 이러한 파일은 Azure 클라우드 서비스 응용 프로그램과 함께 패키지 됩니다 및 tooAzure 배포 합니다.

* hello **ServiceDefinition.csdef** 파일 hello 포함 된 어떤 역할을 포함 하 여 클라우드 서비스 응용 프로그램의 hello 요구 사항에 대 한 Azure 환경에 필요한 hello 메타 데이터를 포함 합니다. 이 파일에는 tooall 인스턴스를 적용 하는 구성 설정이 포함 되어 있습니다. 이러한 구성 설정은 hello Azure 서비스 호스팅 런타임 API를 사용 하 여 런타임에 읽을 수 있습니다. 서비스가 Azure에서 실행되는 동안 이 파일을 업데이트할 수 없습니다.
* hello **ServiceConfiguration.cscfg** 파일 hello 서비스 정의 파일에 정의 된 hello 구성 설정에 대 한 값을 설정 하 고 각 역할에 대 한 인스턴스 toorun hello 수를 지정 합니다. 클라우드 서비스가 Azure에서 실행되는 동안 이 파일을 업데이트할 수 있습니다.

hello Azure Tools for Microsoft Visual Studio는 이러한 파일에 저장 된 tooset 구성 설정을 사용할 수 있는 속성 페이지를 제공 합니다. tooaccess hello 속성 페이지, 솔루션 탐색기에서 hello Azure 클라우드 서비스 프로젝트 아래에 hello 역할 참조를 두 번 클릭 하거나 hello 역할 참조를 마우스 오른쪽 단추로 클릭 및 선택 **속성**hello 다음 그림에에서 나온 것 처럼 합니다.

![VS_Solution_Explorer_Roles_Properties](./media/vs-azure-tools-multiple-services-project-configurations/IC784076.png)

Hello 서비스 정 및 서비스 구성 파일에 대 한 스키마 기본 hello에 대 한 정보를 참조 hello [스키마 참조](https://msdn.microsoft.com/library/azure/dd179398.aspx)합니다. 서비스 구성에 대 한 자세한 내용은 참조 [tooConfigure 클라우드 서비스 방법](cloud-services/cloud-services-how-to-configure.md)합니다.

## <a name="configuring-role-properties"></a>역할 속성 구성
웹 역할 및 작업자 역할에 대 한 hello 속성 페이지는 hello 다음 섹션에서에서 언급 하는 몇 가지 차이점이 있지만 유사 합니다.

Hello에서 **캐싱** 페이지를 구성할 수 있습니다 hello Azure caching 서비스입니다.

### <a name="configuration-page"></a>구성 페이지
Hello에 **구성** 페이지에서 이러한 속성을 설정할 수 있습니다.

**인스턴스**

집합 hello **인스턴스** 속성 toohello이이 역할에 대 한 hello 서비스를 실행 하는 인스턴스 수를 계산 합니다.

집합 hello **VM 크기** 속성 너무**매우 작음으로**, **작은**, **보통**, **Large**, 또는 **초대형**합니다.  자세한 내용은 [클라우드 서비스에 적합한 크기](cloud-services/cloud-services-sizes-specs.md)를 참조하세요.

**시작 작업** (웹 역할만)

Visual Studio 디버깅을 시작할 때 hello HTTP 끝점 hello HTTPS 끝점 중 하나 또는 둘 다에 대 한 웹 브라우저를 시작 해야 하는이 속성 toospecify를 설정 합니다.

hello HTTPS 끝점 옵션은 HTTPS 끝점 역할에 대해 이미 정의한 경우에 사용할 수 있습니다. Hello에 HTTPS 끝점을 정의할 수 있습니다 **끝점** 속성 페이지.

HTTPS 끝점을 이미 추가한 경우 hello HTTPS 끝점 옵션은 기본적으로 사용 하도록 설정 하 고 HTTP 끝점에 대 한 tooa 브라우저 뿐만 아니라 디버깅을 시작할 때 Visual Studio는이 끝점에 대 한 브라우저를 시작 합니다. 이는 두 시작 옵션이 설정되었다고 가정합니다.

**진단**

기본적으로 진단 hello 웹 역할에 대해 사용 됩니다. hello Azure 클라우드 서비스 프로젝트 및 저장소 계정 toouse hello 로컬 저장소 에뮬레이터에 설정 됩니다. 준비 toodeploy tooAzure 되 면 hello 작성기 단추를 선택할 수 있습니다 (**...** ) tooupdate hello 저장소 계정 toouse hello 클라우드에서 Azure 저장소입니다. Hello 진단 데이터 toohello 저장소 계정을 자동으로 예약 된 간격으로 또는 요청 시 전송할 수 있습니다. Azure 진단에 대한 자세한 내용은 [Azure Cloud Services 및 Virtual Machines에서 진단 사용](cloud-services/cloud-services-dotnet-diagnostics.md)을 참조하세요.

## <a name="settings-page"></a>설정 페이지
Hello에 **설정을** 페이지에서 서비스에 대 한 구성 설정을 추가할 수 있습니다. 구성 설정은 이름-값 쌍입니다. Hello 역할에서 실행 되는 코드 hello에서 제공 하는 클래스를 사용 하 여 런타임에 구성 설정의 hello 값을 읽을 수 [Azure Managed Library](http://go.microsoft.com/fwlink?LinkID=171026)합니다. 특히 hello [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx) 메서드 런타임에 명명 된 구성 설정의 hello 값을 반환 합니다.

### <a name="configuring-a-connection-string-tooa-storage-account"></a>연결 문자열 tooa 저장소 계정 구성
연결 문자열은 hello 저장소 에뮬레이터에 대 한 또는 Azure 저장소 계정에 대 한 연결 및 인증 정보를 제공 하는 구성 설정입니다. 역할에서 실행 되는 코드에서 Azure 저장소 서비스 데이터-즉, blob, 큐 또는 테이블 데이터에 액세스 해야, 때마다 해당 저장소 계정에 대 한 연결 문자열 toodefine 해야 합니다.

Tooan Azure 저장소 계정을 가리키는 연결 문자열은 정의 된 형식을 사용 해야 합니다. 방법에 대 한 내용은 toocreate 연결 문자열 참조 [Azure 저장소 연결 문자열 구성](storage/common/storage-configure-connection-string.md)합니다.

때 했으면 toodeploy 클라우드 서비스 tooAzure를 준비 하거나 준비 tootest hello Azure 저장소 서비스에 대해 서비스는, Azure 저장소 계정 연결 문자열 toopoint tooyour 모든의 hello 값을 변경할 수 있습니다. (**...**)를 선택하고 **저장소 계정 자격 증명 입력**을 선택합니다. 계정 이름 및 계정 키를 포함한 계정 정보를 입력합니다. Hello에 **저장소 계정 연결 문자열** 대화 상자에서 있습니다 수 또한 여부를 지정 toouse hello 기본 HTTPS 끝점 (hello 기본 옵션), hello 기본 HTTP 끝점 또는 사용자 지정 끝점입니다. 에 설명 된 대로 서비스에 대 한 사용자 지정 도메인 이름을 등록 한 경우 사용자 지정 끝점 toouse 결정할 수도 있습니다 [Azure 저장소 계정에서 blob 데이터에 대 한 사용자 지정 도메인 이름을 구성](storage/blobs/storage-custom-domain-name.md)합니다.

> [!IMPORTANT]
> 서비스를 배포 하기 전에 연결 문자열 toopoint tooan Azure 저장소 계정을 수정 해야 합니다. Toodo 실패 하지 toostart 역할 발생할 수 있습니다 또는 통해 toocycle hello 초기화, 사용 중 및 중지 중 상태입니다.
> 
> 

## <a name="endpoints-page"></a>끝점 페이지
작업자 역할에는 임의 개수의 HTTP, HTTPS 또는 TCP 끝점이 있을 수 있습니다. 끝점 사용 가능한 tooexternal 클라이언트는 입력된 끝점 또는 hello 서비스에서 실행 되는 사용 가능한 tooother 역할 있는 내부 끝점일 수 있습니다.

* toomake HTTP 끝점 사용 가능한 tooexternal 클라이언트와 웹 브라우저 hello 끝점 형식 tooinput를 변경 하 고 이름 및 공용 포트 번호를 지정 합니다.
* toomake HTTPS 끝점이 사용 가능한 tooexternal 클라이언트와 웹 브라우저 hello 끝점 유형을 변경 너무**입력**, 이름, 공용 포트 번호 및 관리 인증서 이름을 지정 합니다.
  
    관리 인증서를 지정할 수 있습니다, 전에 hello에 hello 인증서를 정의 해야 하는 참고 **인증서** 속성 페이지.
* 다른 역할이 hello 클라우드 서비스에 내부 액세스에 사용할 수 있는 끝점 toomake hello 끝점 형식 toointernal 바꾼 이름 및이 끝점에 대 한 가능한 개인 포트를 지정 하십시오.

## <a name="local-storage-page"></a>로컬 저장소 페이지
Hello를 사용할 수 있습니다 **로컬 저장소** 속성 페이지 tooreserve 하나 또는 역할에 로컬 저장소 리소스를 더 합니다. 로컬 저장소 리소스는 hello Azure 가상 컴퓨터의 hello 파일 시스템에 예약된 된 디렉터리는 역할 인스턴스가 실행 되는 합니다.

## <a name="certificates-page"></a>인증서 페이지
Hello에 **인증서** 페이지에서 인증서를 역할과 연결할 수 있습니다. 사용 되는 tooconfigure hello에 HTTPS 끝점 수를 추가 하는 hello 인증서 **끝점** 속성 페이지.

hello **인증서** 인증서 tooyour 서비스 구성에 대 한 정보를 추가 하는 속성 페이지. 인증서 서비스;와 함께 패키징되 지 않습니다 참고 개별적으로 인증서를 업로드 해야 hello 통해 tooAzure [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다.

역할을 통해 인증서 tooassociate hello 인증서에 대 한 이름을 제공 합니다. 이 이름은 toorefer toohello 인증서를 사용 하 여 hello에서 HTTPS 끝점을 구성할 때 **끝점** 속성 페이지. 다음으로 hello 인증서 저장소 인지를 지정 **로컬 컴퓨터** 또는 **현재 사용자** 및 hello 저장소의 hello 이름입니다. 마지막으로 hello 인증서의 지문을 입력 합니다. Hello 인증서 이면 hello 현재 사용자 \ 개인 (My) 저장소 hello 인증서 채워진된 목록에서 선택 하 여 hello 인증서의 지문을 입력할 수 있습니다. 다른 위치에 있으면 hello 지문 값을 직접 입력 합니다.

Hello 인증서 저장소에서 인증서를 추가 하면 모든 중간 인증서 toohello 구성 설정에 자동으로 추가 됩니다. 이러한 중간 인증서도 업로드 되어야 tooAzure 순서 toocorrectly에 SSL에 대 한 서비스를 구성 합니다.

서비스와 연결 하는 모든 관리 인증서는 hello 클라우드에서 실행 되는 경우에 tooyour 서비스를 적용 합니다. 서비스는 hello 로컬 개발 환경에서 실행 중일 때 hello 계산 에뮬레이터에서 관리 되는 표준 인증서를 사용 합니다.

## <a name="configuring-hello-azure-cloud-service-project"></a>Hello Azure 클라우드 서비스 프로젝트 구성
tooan 전체 Azure 클라우드 서비스 프로젝트를 적용 되는 tooconfigure 설정을 먼저 hello 바로 가기 메뉴에서 해당 프로젝트 노드를 열고 속성 tooopen를 선택한 다음 해당 속성 페이지. 다음 표에서 hello 해당 속성 페이지를 보여 줍니다.

| 속성 페이지 | 설명 |
| --- | --- |
| 응용 프로그램 |이 페이지에서는이 클라우드 서비스 프로젝트를 사용 하는 Azure Tools의 hello 버전에 대 한 정보를 표시할 수 있습니다 및 toohello hello 도구의 현재 버전을 업그레이드할 수 있습니다. |
| 빌드 이벤트 |이 페이지에서 빌드 전 및 빌드 후 이벤트를 설정할 수 있습니다. |
| 개발 |이 페이지에서는 빌드 구성 지침과 빌드 후 이벤트 실행 되는 hello 조건을 지정할 수 있습니다. |
| 웹 |이 페이지에서는 toohello 웹 서버와 관련 된 설정을 구성할 수 있습니다. |


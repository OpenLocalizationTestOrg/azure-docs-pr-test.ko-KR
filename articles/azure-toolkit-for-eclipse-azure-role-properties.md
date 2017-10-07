---
title: "aaaAzure 역할 속성"
description: "Toouse Eclipse tooconfigure Azure 역할 설정에 대 한 Azure 도구 키트를 hello 하는 방법에 대해 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5c0ec412-5702-465a-8f47-87a8ce99a267
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: d111b4b9e4f12e49f38755bf6c9acc1a1de17a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-properties"></a>Azure 역할 속성
Azure 역할에 대 한 다양 한 구성 설정은 hello Azure Toolkit for Eclipse 내에서 설정할 수 있습니다.

## <a name="configuring-azure-role-properties"></a>Azure 역할 속성 구성
Azure 역할 속성을 구성 하는 작업자 역할에 대 한 hello 속성 대화 상자를 통해 수행 됩니다. Eclipse의 프로젝트 탐색기 창 및 선택 hello hello 역할에 대 한 상황에 맞는 메뉴를 열고 hello **Azure** 하위 메뉴입니다. (Hello 역할 hello Eclipse 프로젝트 탐색기에에서 표시 되지 않으면, 확장 프로젝트 탐색기에서 Azure 프로젝트.)

![][ic789599]

hello에서 설정할 수 있는 다양 한 속성이 hello **속성** 대화 상자는이 항목에서 설명 합니다. 새 Azure 배포 프로젝트를 만들 때 많은 속성이 자동으로 채워집니다.

속성 페이지를 수행 하는 hello Azure 역할에 사용할 수 있는 합니다.

* [가상 컴퓨터 속성](#virtual_machine_properties)
* [캐싱 속성](#caching_properties)
* [인증서 속성](#certificates_properties)
* [구성 요소 속성](#components_properties)
<!-- * [Debugging properties](#debugging_properties) -->
* [끝점 속성](#endpoints_properties)
* [환경 변수 속성](#environment_variables_properties)
* [부하 분산/세션 선호도(또는 "고정 세션") 속성](#session_affinity_properties)
* [로컬 저장소 속성](#local_storage_properties)
* [서버 구성 속성](#server_configuration_properties)
* [SSL 오프로딩 속성](#ssl_offloading_properties)

<a name="virtual_machine_properties"></a>

### <a name="virtual-machine-properties"></a>가상 컴퓨터 속성
Eclipse의 프로젝트 탐색기 창에서 hello 역할에 대 한 hello 상황에 맞는 메뉴를 열고 **Azure**, 클릭 하 고 **속성**, hello 기능 toochange hello 가상 컴퓨터 크기를 변경할 수도 및 인스턴스의: hello 다음 이미지와 같이 hello 수입니다.

![][ic719499]

> [!NOTE]
> Windows에만 해당: 설정한 인스턴스 수가 hello tooa 값 1 보다 큰 경우 응용 프로그램 서버를 구성할 수도 hello 지정할 수 하나의 역할 인스턴스 toorun이이 설정과 관계 없이 hello 에뮬레이터에서 합니다. 이 hello 서로 다른 서버 인스턴스 (예를 들어 모든 동안 toobind tooport 8080) 간의 포트 바인딩 충돌을 tooavoid hello에 따라 실행 될 때 동일한 컴퓨터. 프로그램 원하는 인스턴스 개수 설정은 보존 되지만 발효 되 toohello 클라우드를 배포할 때만 합니다.
> 
> 

<a name="caching_properties"></a> 

### <a name="caching-properties"></a>캐싱 속성
Eclipse의 프로젝트 탐색기 창에서 hello 역할에 대 한 hello 상황에 맞는 메뉴를 열고 **Azure**, 클릭 하 고 **캐싱**합니다. 이 대화 상자에서 위치에 배치 하는 명명 된 memcache 호환 캐시 있으므로 toohelp 속도 웹 응용 프로그램을 사용할 수 있습니다.

![][ic719483]

Hello 내 **캐싱** 속성 페이지에서 다음 hello에 대 한 전역 설정을 지정할 수 있습니다.

* 배치된 캐싱의 사용 여부.
* 메모리의 백분율로 hello 캐시 크기입니다.
* toosave hello 캐시 상태를 원하지 않는 경우 응용 프로그램이 실행 되는 클라우드 서비스 또는 none으로 hello 캐시 상태를 저장 하기 위한 hello 저장소 계정 이름입니다. (hello 저장소 계정 이름이 사용 되지 않습니다 hello 계산 에뮬레이터에서 응용 프로그램을 실행 하는 경우.) 너무 hello 저장소 계정 이름을 설정 하는 경우**(자동)** (hello 기본값) 인 캐싱 구성에서 자동으로 사용 됩니다 hello hello에서 선택 하는 대로 동일한 저장소 계정을 hello **tooAzure게시**대화 상자.

> [!NOTE]
> hello **(자동)** 설정을 효과가 필요한 hello hello Eclipse 도구 키트의를 사용 하 여 배포를 게시 하는 경우에 게시 마법사. Hello 등의 외부 메커니즘을 사용 하 여 수동으로 hello.cspkg 파일을 게시 하면 [Azure 관리 포털][Azure Management Portal], hello 배포 제대로 작동 하지 것입니다.
> 
> 

대화를 수행 하는 hello 캐시에 대 한 hello 속성을 보여 줍니다.

![][ic719501]

* **이름:** hello의 hello 이름 같은 캐시 위치에 배치 합니다.
* **포트 번호:** hello 캐시에 대 한 포트 번호 toouse hello 합니다.
* **만료 정책:** hello hello 캐시에 키가 만료 되는 시기를 지정 하는 다음 값 중 하나입니다.
  * **절대:** hello 키로 지정 된 hello 시간 만료 **분 toolive** 에 도달 합니다.
  * **NeverExpires:** hello 키 만료 시간이 없습니다.
  * **SlidingWindow:** hello 키로 지정 된 시간 동안 hello에 액세스 하지 않은 경우 만료 **분 toolive**때마다 액세스 하는 것, hello 만료 시계가 다시 설정 됩니다.
* **분 toolive:** toolive, memcached 키에 대 한 시간 (분) 최대 toohello 만료 정책을 적용 합니다.
* **다른 역할 인스턴스에서 복제된 백업을 통한 고가용성:** 사용하도록 설정하면 다른 역할 인스턴스에서 복제된 백업을 사용하여 고가용성 제공하도록 합니다. Note 두 개 이상의 역할 인스턴스 기능 toowork이에 대 한 배포에 적용 되어 있어야 합니다.

새 캐시 tooadd 클릭 hello **추가** hello 단추 **캐싱** 속성 페이지 및 **명명 된 캐시 구성** 대화 상자가 열립니다. 위에서 설명한 hello 속성에 대 한 값을 제공 합니다.

명명된 된 캐시 toomodify hello 캐시를 선택 하 고 hello 클릭 **편집** hello 단추 **캐싱** 속성 페이지. 대화 상자는 가능 하면 toomodify hello 캐시 속성 열립니다. 키를 눌러 **확인** toosave hello 캐시 값입니다.

캐시를 toodelete hello 캐시를 선택 하 고 hello 클릭 **제거** hello에서 단추 **캐싱** 속성 페이지 및 클릭 한 다음 **예** tooconfirm hello 삭제 합니다.

방법에 대 한 자세한 내용은 캐싱 toouse 참조 [어떻게 tooUse 배치 캐싱][How tooUse Co-located Caching]합니다.

<a name="certificates_properties"></a> 

### <a name="certificates-properties"></a>인증서 속성
Eclipse의 프로젝트 탐색기 창에서 hello 역할에 대 한 hello 상황에 맞는 메뉴를 열고 **Azure**, 클릭 하 고 **인증서**합니다.

![][ic710964]

이 대화 상자에서는 Eclipse 프로젝트에서 참조하는 인증서를 추가하거나 제거할 수 있습니다. 여기에 나열 된 hello 인증서는 Java keystore 안에 자동으로 저장 되지 않습니다 및 따라서 자동으로 사용할 수 없는 Java 응용 프로그램 내에서 사용할 모든 note 합니다. 다른 Windows 소프트웨어에 의해 인증서 배포를 실행 하는 hello 가상 컴퓨터에 저장을 사용 하 여 Windows hello를 미리 로드할 수 있도록 종종 azure 등록만 합니다. 현재 hello 인증서를 사용 하는 hello 도구 키트의 기능 hello 이런 방식이으로 참조만 hello **인증서** 대화 상자는 [SSL 오프 로딩][SSL Offloading]인해 tooits 필요한 인터넷 정보 서비스 (IIS) 및 응용 프로그램 요청 라우팅 (ARR)에 대 한 의존도 hello 적절 한 인증서 toobe 이런이 방식으로 사용할 수 있습니다.

PFX 개인 정보 교환 () 해당 암호와 함께 toothese 인증서 파일 순서로 tooautomatically 업로드 toohello hello에 증명된 toopoint 됩니다 hello 게시 마법사를 사용 하 여 프로젝트 tooAzure를 배포 하면 업로드 되지 않은 없는 이전에 경우에만 azure 서비스입니다.

<a name="components_properties"></a> 

### <a name="components-properties"></a>구성 요소 속성
Eclipse의 프로젝트 탐색기 창에서 hello 역할에 대 한 hello 상황에 맞는 메뉴를 열고 **Azure**, 클릭 하 고 **구성 요소**합니다. 이 대화 상자에서 있습니다 hello 기능 tooadd 있는, 수정 또는 사용자 역할의 hello 구성 요소를 제거할으로 처리 되는 hello 순서를 변경 합니다.

![][ic719502]

hello 구성 요소 기능을 통해 Java 응용 프로그램 프로젝트, 특수 한 파일 및 프로그램 배포에 필요한 실행 가능한 명령줄 문 등 tooadd 종속성 tooyour Azure 배포 프로젝트 있습니다.

각 구성 요소에 다음을 지정할 수 있습니다.

* hello 단계 toobe 작성 될 때 Azure 배포 프로젝트를 hello 구성 요소를 가져올 때 수행 됩니다.
* hello 단계 toobe hello Azure 클라우드에서에서 구성 요소를 배포할 때 수행 됩니다.

> [!NOTE]
> 구성 요소 파일 또는 명령줄을 지정할 때 배포 되도록 게시 된 tooa Windows 가상 컴퓨터를 사용자 지정 단계는 Windows 기반 운영 체제에 대 한 유효 해야 하므로 염두에서에 둬야 합니다. 
> 
> 

구성 요소에는 다음과 같은 속성 hello:

* **가져오기:** 방법을 hello 구성 요소는 프로젝트로 가져올 수 hello hello 프로젝트를 빌드할 때를 나타내는 방법입니다. Hello 다음 값 중 하나일 수 있습니다이:
  * **복사:** hello로 지정 된 hello 로컬 경로에서 hello 구성 요소가 복사 되 **에서** hello 역할에 속성 **approot** 디렉터리입니다.
  * **귀:** hello 구성 요소는 hello로 지정 된 hello 로컬 경로에 엔터프라이즈 응용 프로그램 프로젝트에서 가져온 Java 엔터프라이즈 아카이브 (EAR) **에서** 속성입니다. (이 자동으로 검색 되는 위치에서 hello 프로젝트의 hello 특성에 따라 hello 도구 키트에서).
  * **JAR:** hello 구성 요소는 Java 보관 파일 (JAR)와 hello로 지정 된 hello 로컬 경로에 있는 Java 프로젝트에서 가져온 **에서** 속성입니다. (이 자동으로 검색 되는 위치에서 hello 프로젝트의 hello 특성에 따라 hello 도구 키트에서).
  * **none:** 아무 작업도 tooimport hello 구성 요소입니다. 이 hello 구성 요소를 사용 하는 것으로 간주 하는 경우 적용 가능한 tooalready hello 역할에 있을 **approot** 디렉터리 때 hello 구성 요소는에 지정 된 hello로 실행 가능한 명령줄 문 단순히 또는 **로**속성 때 hello **배포** 방법은 **exec**합니다.
  * **WAR:** hello 구성 요소가 Java 웹 응용 프로그램 보관 파일 (WAR) 이며 hello로 지정 된 hello 로컬 경로에 있는 동적 웹 프로젝트에서 가져온 **에서** 속성입니다. (이 자동으로 검색 되는 위치에서 hello 프로젝트의 hello 특성에 따라 hello 도구 키트에서).
  * **zip:** hello 구성 요소는 zip 파일을 이동식 hello 디렉터리나 hello로 지정 된 파일에서 가져온 **에서** 속성입니다.
* **원본:** 로컬 컴퓨터 toohello 폴더나 hello 항목 tooimport tooyour 배포를 나타내는 파일의 원본 경로입니다. 이 속성에 Windows 환경 변수를 사용할 수 있습니다. Hello 역할으로 가져올 수 있는 모든 구성 요소를 가져올 수 있습니다 **approot** hello 프로젝트를 빌드할 때 디렉터리입니다.
  
    Note는 hello 기능 toodeploy 다운로드에서 구성 요소 경우 toohello 클라우드 (hello 계산 에뮬레이터가 아니라)를 배포 합니다. 구성 요소를 추가에 대해 아래의 관련된 정보를 참조하세요.    
* **데이터 형식:** hello 역할으로 가져올은 구성 요소는 hello에서 파일 이름을 **approot** 디렉터리와 Azure 클라우드 hello에 최종적으로 배포 합니다. 이 속성이 빈 tookeep hello 이름 hello hello 로컬 컴퓨터에는 같은 방법으로 둡니다. (실행 가능한 구성 요소, 즉,에 대 한 이러한 갖는 **배포** 방법을 너무 설정**exec**, 임의의 Windows 명령줄 문일 수 있습니다.)
  
  > [!IMPORTANT]
  > 이 값에 대 한 공백 문자를 사용 하는 경우 이러한 다르게 처리 됩니다 hello에 따라 배포 방법입니다. Hello 방법을 배포 하는 경우는 **exec**, 공간 하 고 hello 파일 이름의 일부가 아니라 명령줄 인수 구분 기호로 해석 됩니다. 다른 모든 배포 방법의 경우 공간 hello 파일 이름의 일부로 해석 됩니다.
  > 
  > 
* **배포:** hello 배포를 시작할 때 hello 동작을 나타내는 메서드가 toohello 구성 요소를 적용 합니다. Hello 다음 값 중 하나일 수 있습니다이:
  
  * **복사:** hello 구성 요소는 복사 toohello 대상 경로 hello로 지정 된 **를** 속성입니다.
  * **exec:** hello 구성 요소는 실행 가능한 Windows 명령줄 문 hello로 지정 된 hello 경로의 hello 컨텍스트에서 실행 **를** hello 배포가 시작 되는 hello 시 속성입니다.
  * **none:** hello 배포가 시작 될 때 아무 작업도 적용 된 toohello 구성 요소입니다.
  * **zip:** hello 구성 요소는 hello에서 지정한 압축 푼된 toohello 대상 경로 **를** 속성입니다. 이 메서드는 경우에 제공 hello **가져오기** 속성은 **zip**합니다.
* **대상:** hello 구성 요소를 배포할 hello 가상 컴퓨터에서 대상 경로입니다. Windows 환경 변수에이 속성에 사용할 수 있으며 파일 경로 너무 상대**approot**합니다.

새 구성 요소를 tooadd 클릭 hello **추가** hello 단추 **구성 요소** 속성 페이지 및 **Azure 역할 구성 요소** 대화 상자가 열립니다. 위에서 설명한 hello 속성에 대 한 값을 제공 합니다. 

hello 다음에는 새로운 WAR 구성 요소를 추가 하기 위한 예가 나와 있습니다.

![][ic719503]

때는 toohello 클라우드 (hello 계산 에뮬레이터가 아니라), toodeploy hello 구성 요소를 다운로드 하는 경우 배포 확인 하는 **때 hello 패키지에 포함 하는 대신 클라우드 배포에서** 을 선택 합니다. Azure 저장소 계정에서 toodownload를 원하는 경우 hello에서 hello 저장소 계정을 선택 **저장소 계정** 드롭 다운 목록 (hello를 클릭할 수 있는 **계정** hello 목록에 포함 된 내용 toomodify 연결), hello에 부분적으로 채워지면 있는 **URL** 필드를 선택한 다음 hello hello URL의 일부를 나머지를 입력 합니다. Azure 저장소 toouse 하지 않으려면 선택 **(없음)** hello에서 **저장소 계정** 드롭 다운 목록으로 이동한 hello에 hello URL tooyour 구성 요소 입력 **URL** 필드입니다. Hello 메서드를 다음 중 하나를 지정 합니다.

* **복사:** hello 다운로드 구성 요소는 복사 toohello 대상 경로 hello로 지정 된 **tooDirectory** 경로입니다.
* **동일한:** 에 사용 된 동일한 방법을 hello **다운로드에서 배포** 에 대 한 **패키지에서 배포**합니다.
* **zip:** hello 다운로드 구성 요소는 hello에서 지정한 압축 푼된 toohello 대상 경로 **tooDirectory** 경로입니다.

구성 요소를 선택 하는 hello 구성 요소와 클릭 hello toomodify **편집** hello 단추 **구성 요소** 속성 페이지. 대화 상자는 가능 하면 toomodify hello 구성 요소 속성 열립니다. 키를 눌러 **확인** toosave hello 구성 요소 값입니다.

구성 요소를 선택 하는 hello 구성 요소와 클릭 hello toodelete **제거** hello 단추 **구성 요소** 속성 페이지 및 클릭 한 다음 **예** tooconfirm hello 삭제 합니다.

구성 요소는 나열 된 hello 순서 대로 처리 됩니다. 사용 하 여 hello **위로 이동** 및 **아래로 이동** tooarrange hello 순서 단추입니다.

> [!NOTE]
> hello 서버 구성 기능이 구성 요소에도 의존합니다. 이러한 구성 요소 제거 하거나 hello 해당 서버 구성을 제거 하지 않고 편집할 수 있습니다. 메시지가 표시 됩니다이 대해 toomake 변경 toosuch 구성 요소를 시도할 때.
> 
> 

<!-- <a name="debugging_properties"></a> -->

<!-- ### Debugging properties -->
<!-- Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Debugging**. Within this dialog, you have hello ability tooenable or disable remote debugging, as well as create debug configurations, as shown in hello following image. -->

<!-- ![][ic719504] -->

<!-- For related information about debugging, see [Debugging Azure Applications in Eclipse][Debugging Azure Applications in Eclipse]. -->

<a name="endpoints_properties"></a> 

### <a name="endpoints-properties"></a>끝점 속성
Eclipse의 프로젝트 탐색기 창에서 hello 역할에 대 한 hello 상황에 맞는 메뉴를 열고 **Azure**, 클릭 하 고 **끝점**합니다. 이 대화 상자에서 hello 기능 toocreate 끝점으로 편집 했거나 hello 다음 이미지와 같이 끝점을 제거 합니다.

![][ic719505]

끝점을 tooadd 클릭 hello **추가** hello 단추 **끝점** 속성 페이지 및 **끝점 추가** 대화 상자가 열립니다.

![][ic710897]

Hello 끝점에 대 한 이름을 입력 hello 유형을 선택 합니다 (두 **입력**, **내부**, 또는 **InstanceInput**), hello 공용 및 개인 포트를 지정 합니다. 키를 눌러 **확인** toosave hello 새 끝점 값입니다.

끝점의 hello 유형에 따라 다음과 같이 포트 범위를 사용할 수 있습니다.

* Hello 공용 포트는 입력된 인스턴스 끝점에 대 한 포트의 범위를 수 있습니다 (예를 들어 **2000-2010**) hello 개인 포트는 고정된 값입니다.
* 내부 끝점에 대 한 hello 공용 포트를 사용 하지 않으면 및 hello 개인 포트 범위 또는 공백 또는 집합 tooan 별표 tooindicate Azure에서 자동으로 설정 될 수 있습니다.
* 입력된 끝점에 대 한 hello 공용 포트는 고정된 값 수만 하 고 hello 개인 포트는 고정된 값 또는 공백 또는 집합 tooan 별표 tooindicate Azure에서 자동으로 설정 될 수 있습니다.

Toouse 범위 대신 단일 포트 번호를 원하는 경우에 hello 범위 끝 hello에 대 한 hello 텍스트 상자를 비워 둡니다.

포트는 집합 tooautomatic toodetermine 해야 할 경우 런타임에 실제로 사용 되는 포트에 대 한 응용 프로그램 hello hello에 설명 되어 있는 Azure 서비스 런타임 API צ ְ ײ [com.microsoft.windowsazure.serviceruntime 패키지 요약][com.microsoft.windowsazure.serviceruntime package summary]합니다.

<!-- toosee how instance input endpoints can be used toohelp with debugging a multi-instance deployment, see [Debugging a specific role instance in a multi-instance deployment][Debugging a specific role instance in a multi-instance deployment]. -->

끝점을 toomodify hello 끝점을 선택 하 고 hello 클릭 **편집** hello 단추 **끝점** 속성 페이지. Toomodify hello 끝점 이름, 유형 및 공용 및 개인 포트를 허용 하는 대화 상자가 열립니다. 키를 눌러 **확인** toosave hello 끝점 값을 수정 합니다.

끝점을 toodelete hello 끝점을 선택 하 고 hello 클릭 **제거** hello 단추 **끝점** 속성 페이지 및 클릭 **예** tooconfirm hello 삭제 합니다.

Hello toolkit 사용자 정의 끝점과 함께 나열 될 특수 끝점을 자동으로 구성할 수 있습니다, 그리고 순서 tooproperly hello 사용자 역할에 의해 사용 하도록 설정 (예: 캐싱, 세션 선호도 또는 SSL 오프 로딩) hello 기능 중 일부를 구성 합니다. hello toolkit hello 사용자 편집 하거나 못하도록 hello 관련 기능으로 자동으로 생성 된 이러한 끝점을 삭제를 사용할 수 있습니다.

<a name="environment_variables_properties"></a> 

### <a name="environment-variables-properties"></a>환경 변수 속성
Eclipse의 프로젝트 탐색기 창에서 hello 역할에 대 한 hello 상황에 맞는 메뉴를 열고 **Azure**, 클릭 하 고 **환경 변수**합니다. 이 대화 상자에서 hello 기능 toocreate 환경 변수 뿐만 아니라 수정 했거나 hello 다음 이미지와 같이 환경 변수를 제거 합니다.

![][ic719506]

환경 변수는 hello 역할이 시작 될 때 사용할 수 있는 tooyour 시작 스크립트는 합니다.

> [!NOTE]
> 환경 변수를 지정할 때는 배포 되도록 게시 된 tooa Windows 가상 컴퓨터를 환경 변수는 Windows 기반 운영 체제에 대 한 유효 해야 하므로 염두에서에 둬야 합니다.
> 
> 

Hello 역할이 시작 될 때 사용할 수 없게 환경 변수의 예를 들어 hello를 클릭 하 여 새 환경 변수를 만들 **추가** 단추입니다. hello 다음 테이블에 나와 라는 환경 변수 **MyRoleVersion** 만들고 hello 값이 할당 **1.0**합니다.

![][ic659268]

Jsp 코드 내에서 hello를 사용 하 여 hello 값을 표시할 수 있습니다 `System.getenv` 메서드:

    <body>
      <b> Hello World!</b>
      <p>Running role version: <%= System.getenv("MyRoleVersion") %></p>
    </body>

응용 프로그램을 실행할 때 이 출력의 결과는 다음과 같습니다.

![][ic552233]

환경 변수를 toomodify hello 환경 변수를 선택 하 고 hello를 클릭 **편집** hello 단추 **환경 변수** 속성 페이지. 대화 상자는 가능 하면 toomodify hello 환경 변수 속성 열립니다. 키를 눌러 **확인** toosave hello 환경 변수 값입니다.

환경 변수를 toodelete hello 환경 변수를 선택 하 고 hello를 클릭 **제거** hello 단추 **환경 변수** 속성 페이지 및 클릭 한 다음 **예**tooconfirm hello 삭제 합니다.

순서 tooproperly hello 역할에는 사용자가 활성화 일부 hello 기능 (예: 서버 구성, 원격 디버깅 또는 로컬 저장소)를 구성, hello toolkit와 함께 나열 될 특수 환경 변수를 자동으로 구성할 수 있습니다. 사용자 정의 환경 변수입니다. hello toolkit hello 사용자 편집 하거나 못하도록 hello 관련 기능으로 이러한 자동으로 생성 된 환경 변수 삭제를 사용할 수 있습니다.

<a name="session_affinity_properties"></a> 

### <a name="load-balancing--session-affinity-aka-sticky-sessions-properties"></a>부하 분산/세션 선호도(또는 "고정 세션") 속성
Eclipse의 프로젝트 탐색기 창에서 hello 역할에 대 한 hello 상황에 맞는 메뉴를 열고 **Azure**, 클릭 하 고 **부하 분산**합니다. 이 대화 상자에서 hello 기능 tooenable 했거나 hello 다음 이미지와 같이 세션 선호도 사용 하지 않도록 설정 합니다.

![][ic719492]

관련된 내용은 [세션 선호도][Session Affinity]를 참조하세요. 또한에 설명 된 대로 SSL 오프 로딩의 hello 컨텍스트에서이 기능의 동작을 확인 [SSL 오프 로딩][SSL Offloading]합니다.

<a name="local_storage_properties"></a> 

### <a name="local-storage-properties"></a>로컬 저장소 속성
Eclipse의 프로젝트 탐색기 창에서 hello 역할에 대 한 hello 상황에 맞는 메뉴를 열고 **Azure**, 클릭 하 고 **로컬 저장소**합니다. Hello 기능 toocreate 있는이 대화 상자에서 수정 하거나 응용 프로그램을 실행 하는 hello 가상 컴퓨터에 대 한 임시 로컬 저장소를 제거 합니다. 특정 값 뿐만 아니라 hello 다음 이미지와 같이 hello 역할이 재활용 될 때 hello 내용이 보존 되는지 여부 hello 로컬 저장소의 hello 크기에 대해 설정할 수 있습니다.

![][ic719508]

또한 필요에 따라 toohello 로컬 저장소에 해당 하는 환경 변수를 지정할 수 있습니다.

기본적으로 Azure에 배포 하는 모든 항목은 배치 (및 압축을 푼) hello에 **approot** hello 역할 인스턴스의 폴더입니다. 가장 간단한 배포도 압축을 푼 후, hello에 할당 된 hello 공간 들어가지만 됩니다 동안 **approot** 디렉터리 제한 되어 있으며 잘 정의 된 (보다 작은 1GB는 적절 한 경험). 따라서 hello에 들어가지 않을 수 있는 큰 배포에 충분 한 디스크 공간이 할당 되 tooensure Azure **approot** hello를 사용 하 여 로컬 저장소 리소스를 설정 해야 폴더 **로컬 저장소** 대화 상자입니다. 쉽게 toodo에 대 한이, 참조 [대규모 배포의 배포][Deploying Large Deployments]합니다.

시작 스크립트에서 hello 저장소 리소스를 쉽게 참조할 수 있습니다 (예를 들어 프로그램 **startup.cmd**) hello와같이hello리소스와helloEclipse도구키트에서자동으로연결된hello환경변수를사용하여 **로컬 저장소** 대화 상자. 이 환경 변수에 hello 시작 스크립트가 실행 될 hello 시 구성 하는 hello 로컬 리소스의 전체 경로 포함 됩니다. 

로컬 저장소 리소스 toomodify hello 로컬 저장소 리소스를 선택 하 고 hello 클릭 **편집** hello 단추 **로컬 저장소** 속성 페이지. 대화 상자는 가능 하면 toomodify hello 로컬 저장소 리소스 속성 열립니다. 키를 눌러 **확인** toosave hello 로컬 저장소 리소스 값입니다.

로컬 저장소 리소스 toodelete hello 로컬 저장소 리소스를 선택 하 고 hello 클릭 **제거** hello 단추 **로컬 저장소** 속성 페이지 및 클릭 **예** tooconfirm hello 삭제 합니다.

<a name="server_configuration_properties"></a> 

### <a name="server-configuration-properties"></a>서버 구성 속성
Eclipse의 프로젝트 탐색기 창에서 hello 역할에 대 한 hello 상황에 맞는 메뉴를 열고 **Azure**, 클릭 하 고 **서버 구성**합니다. 이 대화 상자에서 hello 기능 tooadd, 제거 및 hello JDK와 Java 응용 프로그램 서버 배포에 사용 되는 수정으로 추가 또는 hello 응용 프로그램 (예: WAR, JAR 또는 EAR 파일) 배포에서 사용 하는 제거 해야 합니다.

### <a name="jdk-configuration"></a>JDK 구성
이 대화 상자에서는 배포에 대 한 toospecify hello JDK 패키지 toouse가 있습니다. Windows에서 Eclipse를 사용 하는 경우에 hello JDK 패키지 로컬에서 실행 중일 때 hello Azure 에뮬레이터 toouse 있고 hello 옵션 toodeploy 해당 로컬 설치 tooAzure를 지정할 수 있습니다. 비 Windows 운영 체제에서 hello 에뮬레이터 JDK 설정이 적용 되지 않으며 배포할 수 없습니다 Windows와 호환 되지 않으므로 hello 로컬 JDK를 설치 합니다. 그러나 사용 중인 hello 운영 체제와 관계 없이 항상 또는 선택할 수 있습니다 간에 hello 3rd party JDK 패키지 toodeploy tooAzure, 대체 다운로드 위치에서 사용자 고유의 Windows 호환 JDK 패키지 요소를 가리키고 있습니다.

hello 다음은 Windows에서 JDK를 지정 하는 방법의 예입니다.

![][ic780647]

Windows에서 Eclipse를 사용 하는 경우 계산 에뮬레이터; hello로 JDK toouse 지정할 수 있습니다. toodo 따라서 확인 **로컬 테스트를 위해이 파일 경로의 JDK 사용 하 여 hello** 체크 인 hello **에뮬레이터 배포** 섹션. 그런 다음 JDK; hello 로컬 경로 tooyour 지정 hello 하나 원하는 toouse 자동으로 선택 하지 않은 경우 toodifferent JDK를 찾아볼 수 있습니다. 또한 있습니다 hello 옵션 toodeploy 프로그램 JDK tooyour Azure 클라우드 서비스입니다. toodo hello를 따라서 선택 **(toocloud 저장소 자동 업로드) 내 로컬 JDK 배포** hello에 대 한 옵션 **배포 클라우드** 섹션.

참고: Windows 이외의 운영 체제에서 hello **에뮬레이터 배포** 설정과 hello **내 로컬 JDK 배포** 옵션은 사용할 수 없습니다. hello 다음 예제에서는 JDK를 지정 하는 mac 또는 지원 되는 다른 Windows 이외의 운영 체제:

![][ic789643]

다음 두 개의 hello 있는 hello 운영 체제에 관계 없이 **배포 클라우드** hello 원본과 JDK 패키지의 형식에 대 한 옵션:

* **Azure에서 사용할 수 있는 타사 JDK 패키지 배포** 
* **사용자 지정 다운로드에서 배포** 

Hello를 사용 하는 경우 **는 타사 JDK 패키지 Azure에서 사용할 수 있는 배포** 옵션:

1. 명명 된 hello 확인란 **는 타사 JDK 패키지 Azure에서 사용할 수 있는 배포**합니다.
2. Hello 드롭 다운 목록에서 hello 타사 JDK 패키지 Azure에서 사용할 수 있는 선택 합니다.
3. 프로그램 **JDK** 탭을 Windows에서 비슷한 toohello 다음 보여: ![][ic780648] 및 Mac OS에서 비슷한 toohello 다음 표시될지 또는 지원 되는 다른 Windows 이외의 운영 체제:![][ic789643]
4. 클릭 **확인** toosave 변경 내용을 합니다.
5. 증명된 tooaccept hello hello 타사 JDK 패키지 공급자에서 사용권 계약, 경우에 hello 사용 조건을 검토 합니다. 클릭 하 여 hello 조건에 동의 하는 것으로 가정 **예** tooclose hello **사용권 계약에 동의** 대화 상자.
    참고 항목 hello에 대 한 hello 드롭 다운 목록에 표시 되는 논리를 기본 해당 hello **는 타사 JDK 패키지 Azure에서 사용할 수 있는 배포** 옵션을 사용자 지정할 수 있습니다. hello에 toocustomize hello 항목 **JDK** 대화 상자에서 hello 클릭 **사용자 지정** 링크 합니다. Hello 닫힙니다 **JDK** 속성 페이지가 닫히고 열기 hello **componentsets.xml** 파일에 Eclipse 필요에 따라 수정할 수 있습니다. 에 대 한 설명서 **componentsets.xml** hello에 포함 된 **componentsets.xml** 파일 자체입니다.

Hello를 사용 하는 경우 **사용자 지정 다운로드에서 JDK 배포** 옵션:

1. 해당 hello 디렉터리 노드 자체가 hello ZIP 구조 및 내용이 아니라 hello 자식 인지 확인 하 여 JDK 설치 디렉터리의 ZIP을 만듭니다. 나중 필요 하 고이 JDK 염두에서에 둬야 합니다 hello 디렉터리의 hello 이름을 기록해 설치 배포 tooa Windows 가상 컴퓨터를 수 있습니다.
2. Hello ZIP Azure 저장소 계정에 blob으로 업로드 합니다. TooAzure 저장소 blob을 업로드 하기 위한 외부에서 사용 가능한 도구를 사용 하 여 수행할 수 있습니다. 개인 blob toouse 것이 좋습니다. Hello ZIP 내용의 blob URL hello 기록해 둡니다.
3. 명명 된 hello 확인란 **사용자 지정 다운로드에서 JDK 배포**합니다.
    Azure 저장소 계정에서 toodownload를 원하는 경우 hello에서 hello 저장소 계정을 선택 **저장소 계정** 드롭 다운 목록 (hello를 클릭할 수 있는 **계정** hello 목록에 포함 된 내용 toomodify 연결), hello에 부분적으로 채워지면 있는 **URL** 필드를 선택한 다음 hello hello URL의 일부를 나머지를 입력 합니다. Azure 저장소 toouse 하지 않으려면 선택 **(없음)** hello에서 **저장소 계정** 드롭 다운 목록으로 이동한 hello에 JDK 다운로드 hello URL tooyour 입력 **URL** 필드입니다. Azure 저장소를 사용 하 여 hello URL의 blob 이름은 소문자 여야 합니다.
4. 해당 hello 확인 **JAVA_HOME** textbox toohello 올바른 디렉터리 이름을 참조 합니다. 기본적으로 참조 합니다. 로컬 사용을 위해 선택한 hello 값과 동일한 JDK 디렉터리 이름을 hello 합니다. Hello ZIP에에서 포함 된 hello 디렉터리 이름이 다른 경우 (예를 들어 due toousing 다른 버전), hello에 업데이트 hello 디렉터리 이름을 **JAVA_HOME** textbox 적절 하 게 hello에서이 설정을 사용 되므로 클라우드 드 ( hello에 없는 에뮬레이터를 계산) 합니다.
5. 클릭 **확인** toosave 변경 내용을 합니다.

이것으로 끝입니다. 이제 hello 클라우드에 대 한 빌드 hello 패키지 크기가 훨씬 더 작은 됩니다, hello 빌드 프로세스는 일반적으로 짧은 시간 취해야 및 hello 배포 toohello 클라우드를 게시할 때 자체 소요 되는 시간도 더 짧은 시간을 확인할 수 있습니다. 해당 hello 참고 **(toocloud 저장소 자동 업로드) 내 로컬 JDK 배포** 또는 **사용자 지정 다운로드에서 JDK 배포** 옵션은 응용 프로그램 hello 클라우드에서 배포 되는 경우에 유효 합니다. 계산 에뮬레이터 환경;에 대 한 영향을 주지 않습니다. hello 로컬 버전의 hello 구성 요소는 toohello 계산 에뮬레이터를 배포할 때에 사용 됩니다. 

### <a name="server-configuration"></a>서버 구성
hello 다음은 응용 프로그램 서버를 지정 하는 방법의 예입니다.

![][ic796926]

해당 hello 확인 **이 유형의 서버를 배포** 확인란을 선택한 다음 hello 형식을 선택 toouse 원하는 응용 프로그램 서버.

클라우드 배포에 대 한 서버 toouse를 지정 하기 위한 다음 옵션 hello 이용할 수 있습니다.

1. **Azure에서 사용할 수 있는 세 번째 타사 서버 배포** -배포 효율성 및 단순성이 매우 우선 순위를 하 고 hello 서버에서 사용자 지정 구성 하지 않아도 개발/테스트 시나리오에서 특히 적합 합니다. 또는 적절 한 서버 사용자 지정 배포의 시작 논리 단계를 시작 지점 hello로 toouse 해당 서버 중 하나를 원하는 하지만 포함 하는 경우.
2. **사용자 지정 다운로드에서 배포** -hello 클라우드에서 toouse 하려는 특별히 준비 되 고 구성 된 서버가 있는 경우이 프로덕션 시나리오에서 특히 적합 합니다.
3. **내 로컬 서버 설치 배포** - 이 로컬 서버 설치가 이미 사용할 사용자 지정으로 구성된 경우 특히 적합합니다. Hello에 로컬 서버 경로도 지정 해야이 옵션을 선택 하면 **로컬 서버 경로** 아래 텍스트 상자입니다.

Hello를 사용 하는 경우 **는 타사 서버 Azure에서 사용할 수 있는 배포** 옵션:

1. 명명 된 hello 확인란 **는 타사 서버 Azure에서 사용할 수 있는 배포**합니다.
2. Hello 드롭다운 메뉴에서 배포 된 hello 원하는 서버 소프트웨어 toouse hello 클라우드에서 선택 합니다. 참고 제한 toochoosing hello에 있는 클라우드 서버만 됩니다 서버 toouse 이전 버전의 형식에 이미 지정한 경우 해당 서버 종류와 같은 제품군입니다. 하지만 서버 유형을 선택 하지 않은 경우 Azure에서 현재 사용할 수 있는 hello 서버 중에서 선택할 수 있습니다에 대 한 hello 서버 유형을 자동으로 선택 됩니다.
3. 클릭 **확인** toosave 변경 내용을 합니다.

Hello를 사용 하는 경우 **사용자 지정 다운로드에서 배포** 옵션:

1. 서버 유형을 toohello 이전 단계에 따라 이미 선택 했는지 확인 합니다. Hello 플러그 인을 설정 하는 것으로 사용자 지정 다운로드에서 toodeploy hello 서버 hello에서 어떻게 해야이 그러면 선택한 서버 종류와 같은 제품군입니다.
2. 명명 된 hello 확인란 **사용자 지정 다운로드에서 배포**합니다.
    Azure 저장소 계정에서 toodownload를 원하는 경우 hello에서 hello 저장소 계정을 선택 **저장소 계정** 드롭 다운 목록 (hello를 클릭할 수 있는 **계정** hello 목록에 포함 된 내용 toomodify 연결), hello에 부분적으로 채워지면 있는 **URL** 필드 및 나머지 부분의 hello URL tooyour 서버 hello에 다음 채우기 ZIP (hello URL의 blob 이름은 Azure 저장소를 사용 하는 소문자 여야 함) 하는 경우 다운로드 합니다. Azure 저장소 toouse 하지 않으려면 선택 **(없음)** hello에서 **저장소 계정** 드롭 다운 목록으로 이동한 hello URL tooyour 서버 다운로드 ZIP hello에 입력 **URL** 필드입니다. hello ZIP이 응용 프로그램 서버 설치 디렉터리를 나타내는 자식 폴더가 포함 됩니다. 예를 들어 Apache Tomcat 7.0.35의 대 한 우편 번호를 사용 하는 경우 hello 내 zip 것 hello 자식 폴더 나타내는 hello 설치 디렉터리와 같은 **7.0.35의 apache-tomcat**합니다. 
3. Hello 홈 디렉터리 환경 변수의 hello 값을 지정 합니다. 있는 경우 로컬 응용 프로그램 서버에 사용 된 toohello 값은 기본적 이지만 클라우드 응용 프로그램 서버가 로컬 응용 프로그램 서버와에서 다른 경우 다른 값을 지정할 수 있습니다. 그러나 클라우드 응용 프로그램 서버 hello의 인지 toomake 해야 이전에 선택한 hello 서버 종류와 같은 제품군입니다.
    Hello 나중에 클라우드 응용 프로그램 서버 zip을 업데이트 하는 경우 홈 디렉터리 설정을 hello 또는 (로컬 응용 프로그램 서버를 너무 변경) 하는 경우 로컬 설정과 일치 다시 toohave 수동으로 변경할 수 있습니다.
4. 클릭 **확인** toosave 변경 내용을 합니다.

기본 논리를 항목이 hello에 표시 하는 hello **서버** hello 탭 **서버 구성** 속성 페이지를 사용자 지정할 수 있습니다. 이 hello 기본값 이상으로 확장 해야 하는 경우 또는 tooadd 다른 서버를 원하는 경우에 필요할 수 있는 고급 기능입니다. hello에서 toocustomize hello 논리 **서버** 대화 상자에서 hello 클릭 **사용자 지정** 링크 합니다. Hello 닫힙니다 **서버 구성** 속성 페이지가 닫히고 열기 hello **componentsets.xml** 파일에 Eclipse 필요한 tooextend hello 서버 구성 템플릿을으로 수정할 수 있습니다. 에 대 한 설명서 **componentsets.xml** hello에 포함 된 **componentsets.xml** 파일 자체입니다.

Hello를 사용 하는 경우 **내 로컬 서버 (toocloud 저장소 자동 업로드) 배포** 옵션:

1. 명명 된 hello 확인란 **내 로컬 서버 (toocloud 저장소 자동 업로드) 배포**합니다.
2. Hello를 사용 하 여 **저장소 계정** 드롭 다운 목록 **(자동)**합니다. 지정 하는 경우 **(자동)** 여기에서 hello Eclipse 도구 키트 ´ ֲ hello 서버 hello와 동일한 저장소 계정 하나 hello에서 배포를 위한 선택한 **tooAzure 게시** 대화 상자.
3. 클릭 **확인** toosave 변경 내용을 합니다.

Hello에서 컴퓨터에 서버 설치 경로 선택 **로컬 서버 경로** hello 다음 조건 중 하나가 충족 되는 경우 텍스트 상자:

* Tootest hello 에뮬레이터 (tooWindows만 적용 됨)에서 배포 하려는 경우
* 로컬로 설치 된 서버 toohello 클라우드 toodeploy 할 수 있습니다.
* Toouse 있으며이 경우에서에 자신의 hello 클라우드의 사용자 지정 서버 다운로드를 원하는, 또한 hello 확인 **내 로컬 서버 (toocloud 저장소 자동 업로드) 배포** 위의 옵션을 선택 합니다.

Tooyour 상황 적용 되는 옵션이 hello 옵션 앞에 오는 경우 hello 로컬 서버 설정은 선택 사항입니다.

### <a name="applications-configuration"></a>응용 프로그램 구성
hello 다음은 응용 프로그램을 지정 하는 방법의 예입니다.

![][ic719512]

클릭 **추가** tooadd 다른 응용 프로그램 또는 **제거** tooremove 응용 프로그램입니다. 효율성 향상을 위해 toouse 다운로드를 응용 프로그램의 소스 hello에 대 한 toohello 클라우드를 배포할 때, 사용 hello [구성 요소 속성](#components_properties) toospecify a URL, 저장소 계정, 등입니다. 

2014 년 4 월 릴리스 hello로 시작 하 고, 응용 프로그램을 자동으로 업로드 hello 동일한 저장소 계정 (hello 아래 **eclipsedeploy** 컨테이너)으로 hello 하나를 배포에 대 한 선택 합니다. 배포의 시작 논리 hello 해당 저장소 계정에서 해당 응용 프로그램을 먼저 다운로드 하는 단계를 포함 합니다. 즉, toorebuild 필요 없이 응용 프로그램 배포에 업그레이드 되 고 해당 저장소 계정 (예: hello Azure 포털 사용)에 직접 hello 응용 프로그램의 최신 버전을 수동으로 업로드 하 여 hello 전체 패키지를 다시 배포할 수 있습니다. hello 도구 키트에서 원래 업로드 hello WAR 파일을 바꿔야 합니다. 그런 다음 시작 또는 다시, 명령줄 유틸리티를 통해 Azure 관리 포털을 사용 하 여 이러한 모든 역할 인스턴스 재활용 hello 합니다. (Hello Eclipse 도구 키트 내에서 직접 역할 재활용을 트리거하는 현재 지원 되지 않음)

### <a name="notes-about-server-configuration"></a>서버 구성에 대한 참고 사항
Hello를 통해 변경 내용이 **서버 구성** 속성 페이지 hello에 반영 됩니다 `<component>` hello package.xml 파일의 요소입니다.

Hello를 사용 하는 경우 **자동으로 업로드 중...**  또는 **다운로드에서 배포 중...**  hello 클라우드 (hello 계산 에뮬레이터가 아니라)를 작성 하는 hello JDK 또는 응용 프로그램 서버 및 사용자에 대 한 옵션 및 연결 된 toohello 네트워크를 Ant hello 대로 빌드 hello hello 콘솔 출력에는 다음과 같은 메시지가 표시 될 수도 있습니다 작성기는 hello 다운로드의 가용성을 확인합니다.

`[windowsazurepackage] Verifying blob availability (https://example.blob.core.windows.net/temp/tomcat6.zip)...` 

Hello를 선택한 경우 **다운로드에서 배포 중...**  옵션을 hello 경고 뒤에 표시 될 수 있지만 hello 빌드가 계속 됩니다.

`[windowsazurepackage] warning: Failed tooconfirm blob availability! Make sure hello URL and/or hello access key is correct (https://example.blob.core.windows.net/temp/tomcat6.zip).` 

이 경고는 hello 유일한 표시는 hello 다운로드의 가용성이 확인 되지 않은 합니다. 따라서 어떤 이유로 hello 클라우드에서 실패 하면 배포 toosee 경우 확인이 경고가 발생 합니다.

(예를 들어 수 있다고 생각 되 면 hello 빌드 불필요 하 게 저하) toodisable hello 다운로드 확인 하려는 경우, 설정 hello `verifydownloads` 너무 특성`false` hello에 `<windowsazurepackage>` package.xml의 요소: 

`<windowsazurepackage verifydownloads="false" ...>` 

Hello를 선택한 경우 **자동으로 업로드 중...**  빌드 hello 업로드 업로드 필요한 경우 언제 든 지 5 초 마다 hello 진행률 보고 메시지가 표시 됩니다 hello 콘솔 창에 옵션입니다.

<a name="ssl_offloading_properties"></a> 

### <a name="ssl-offloading-properties"></a>SSL 오프로딩 속성
Eclipse의 프로젝트 탐색기 창에서 hello 역할에 대 한 hello 상황에 맞는 메뉴를 열고 **Azure**, 클릭 하 고 **SSL 오프 로딩**합니다. 

![][ic719481]

이 대화 상자에서 SSL 오프 로딩, Java 응용 프로그램 서버에서 SSL tooconfigure 필요 없이 Azure에서 Java 배포에서 프로토콜 보안 HTTPS (Hypertext Transfer)를 지원 tooeasily 사용 수 있도록 설정할 수 있습니다. 자세한 내용은 참조 [SSL 오프 로딩] [ SSL Offloading] 및 [어떻게 SSL 오프 로딩 tooUse][How tooUse SSL Offloading]합니다.

## <a name="see-also"></a>참고 항목
[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]

[Hello Eclipse 용 Azure 도구 키트 설치][Installing hello Azure Toolkit for Eclipse]

[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]

[Azure 프로젝트 속성][Azure Project Properties]

[Azure Storage 계정 목록][Azure Storage Account List]

Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터][Azure Java Developer Center]합니다.

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Project Properties]: http://go.microsoft.com/fwlink/?LinkID=699524
[Azure Storage Account List]: http://go.microsoft.com/fwlink/?LinkID=699528
[com.microsoft.windowsazure.serviceruntime package summary]: http://azure.github.io/azure-sdk-for-java/com/microsoft/windowsazure/serviceruntime/package-summary.html
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Debugging a specific role instance in a multi-instance deployment]: http://go.microsoft.com/fwlink/?LinkID=699535#debugging_specific_role_instance
[Debugging Azure Applications in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[Deploying Large Deployments]: http://go.microsoft.com/fwlink/?LinkID=699536
[How tooUse Co-located Caching]: http://go.microsoft.com/fwlink/?LinkID=699542
[How tooUse SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699548
[SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699549

<!-- IMG List -->

[ic789599]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789599.png
[ic719499]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719499.png
[ic719483]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719483.png
[ic719501]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719501.png
[ic710964]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710964.png
[ic719502]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719502.png
[ic719503]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719503.png
[ic719504]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719504.png
[ic719505]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719505.png
[ic710897]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710897.png
[ic719506]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719506.png
[ic659268]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic659268.png
[ic552233]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic552233.png
[ic719492]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719492.png
[ic719508]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719508.png
[ic780647]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780647.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic780648]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780648.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic796926]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic796926.png
[ic719512]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719512.png
[ic719481]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719481.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690945.aspx -->

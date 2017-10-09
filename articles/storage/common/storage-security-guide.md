---
title: "aaaAzure 저장소 보안 가이드 | Microsoft Docs"
description: "세부 정보 hello 많은 메서드가 포함 되지만 제한 되지 tooRBAC, 저장소 서비스 암호화, 클라이언트 쪽 암호화, SMB 3.0 및 Azure 디스크 암호화 하는 Azure 저장소에 보안을 적용 합니다."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 6f931d94-ef5a-44c6-b1d9-8a3c9c327fb2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 1f5a4e724e00ea6d16f5511b9120154f89441758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-guide"></a>Azure 저장소 보안 가이드
## <a name="overview"></a>개요
Azure 저장소는 다양 한 개발자를 함께 사용 하는 보안 기능 toobuild 보안 응용 프로그램을 제공 합니다. 역할 기반 액세스 제어 및 Azure Active Directory를 사용 하 여 hello 저장소 계정 자체를 보호할 수 있습니다. [클라이언트 쪽 암호화](../storage-client-side-encryption.md), HTTP 또는 SMB 3.0을 사용하여 응용 프로그램과 Azure 간에 전송 중인 데이터의 보안을 유지할 수 있습니다. 데이터 toobe 기록 될 때 자동으로 암호화를 설정할 수 있습니다 tooAzure 저장소를 사용 하 여 [저장소 서비스 암호화 (SSE)](storage-service-encryption.md)합니다. 가상 컴퓨터에서 사용 되는 OS 및 데이터 디스크 toobe 사용 하 여 암호화를 설정할 수 있습니다 [Azure 디스크 암호화](../../security/azure-security-disk-encryption.md)합니다. Azure 저장소에서 위임 된 액세스 toohello 데이터 개체를 사용 하 여 부여할 수 [공유 액세스 서명](../storage-dotnet-shared-access-signature-part-1.md)합니다.

이 문서에서는 Azure 저장소에서 사용할 수 있는 이러한 각 보안 기능에 대해 간략히 설명합니다. Tooarticles 쉽게 할 수 있도록 각 기능에 대 한 세부 정보를 제공 하는 한 링크가 제공 됩니다 추가 각 항목에 대 한 조사 합니다.

이 문서에서 다루는 hello 항목 toobe 다음과 같습니다.

* [관리 평면 보안](#management-plane-security) - 저장소 계정 보안 유지

  저장소 계정을 사용 하는 리소스 toomanage hello의 hello 관리 평면 구성 됩니다. 이 섹션에서는 hello Azure 리소스 관리자 배포 모델 및 역할 기반 액세스 제어 (RBAC) toocontrol toouse tooyour 저장소 계정 액세스 하는 방법에 대 한 알아보겠습니다. 저장소 계정 키를 관리 하는 방법에 대 한도 다룹니다 방법과 tooregenerate 해당 합니다.
* [데이터 평면 보안](#data-plane-security) -액세스 보안 tooYour 데이터

  이 섹션에서는 살펴보게 저장소 계정의 blob, 파일, 큐 및 테이블을 같은 toohello 실제 데이터 개체 액세스할 수 있도록 공유 액세스 서명 및 저장 된 액세스 정책을 사용 하 여 합니다. 서비스 수준 SAS 및 계정 수준 SAS에 대한 설명이 제공됩니다. 것도 확인할 toolimit 액세스 방법을 tooa 특정 IP 주소 (또는 IP 주소 범위) 하 고 toolimit hello 프로토콜 tooHTTPS를 사용 하는 방법에 대 한 대기 하지 않고 공유 액세스 서명을 a toorevoke tooexpire 합니다.
* [전송 중 암호화](#encryption-in-transit)

  이 섹션에서는 어떻게 toosecure 데이터 또는 Azure 저장소 외부로 전송 하는 경우. Azure 파일 공유에 대 한 SMB 3.0에서 사용 하는 HTTPS 및 hello 암호화 사용을 권장 하는 hello 방법에 대해 알아보겠습니다. 또한 사용할 수 있는 클라이언트 응용 프로그램에서 저장소에 전송 될 때까지 tooencrypt hello 데이터 및 toodecrypt hello 데이터 저장소에서 전송 된 후 클라이언트 쪽 암호화를 살펴보면 메뉴로 이동 합니다.
* [휴지 상태의 암호화](#encryption-at-rest)

  저장소 서비스 암호화 (SSE) 및 저장소 계정에 대해 활성화 페이지 blob는 블록 blob에 tooAzure 저장소를 기록할 때 자동으로 암호화 되 고 blob을 추가 하는 방법에 대 한 설명 하겠습니다. Azure 디스크 암호화를 사용 하 여 hello는 기본적인 차이점 및 클라이언트 쪽 암호화 및 SSE 및 디스크 암호화의 사례를 탐색 하는 방법에 살펴보겠습니다. 미국 정부 컴퓨터의 FIPS 준수에 대해서도 간단히 살펴봅니다.
* 사용 하 여 [Storage Analytics](#storage-analytics) tooaudit 액세스의 Azure 저장소

  이 섹션에서는 요청에 대 한 hello 저장소 분석에서 toofind 정보 기록 하는 방법을 설명 합니다. 살펴보세요 실제 저장소 분석 로그 데이터를 알아보고 어떻게 toodiscern 여부는 요청은 hello 저장소 참조 하겠습니다 계정 공유 액세스 서명 사용 하 여 키 또는 성공 또는 실패 여부 및 익명으로 합니다.
* [CORS를 사용하여 브라우저 기반 클라이언트를 사용하도록 설정](#Cross-Origin-Resource-Sharing-CORS)

  이 섹션 방법에 논의 tooallow 크로스-원본 자원 공유 (CORS). 도메인 간 액세스 및 어떻게 toohandle 사용 하 여 hello CORS 기능에 기본 제공 Azure 저장소에 대 한 알아보겠습니다.

## <a name="management-plane-security"></a>관리 평면 보안
hello 관리 평면 hello 저장소 계정 자체에 영향을 주는 작업으로 구성 됩니다. 예를 들어 수 또는 저장소 계정을 삭제, 구독에 저장소 계정의 목록을 보려면, hello 저장소 계정 키를 검색할 만들거나 hello 저장소 계정 키 다시 생성 합니다.

새 저장소 계정을 만들 때 기본 배포 모델 또는 리소스 관리자 배포 모델 중에서 선택합니다. Azure의 리소스를 만드는 hello 클래식 모델 전부 아니면 전무 액세스 toohello 구독을 허용 및 저장소 계정을 차례로 hello 합니다.

이 가이드는 저장소 계정 만들기를 위한 권장 hello hello 리소스 관리자 모델에 중점을 둡니다. 주어진 액세스 toohello 전체 구독 보다는 hello 리소스 관리자 저장소 계정, 역할 기반 액세스 제어 (RBAC)를 사용 하 여 더 유한 수준 toohello 관리 평면에 대 한 액세스를 제어할 수 있습니다.

### <a name="how-toosecure-your-storage-account-with-role-based-access-control-rbac"></a>어떻게 toosecure 저장소 계정을 역할 기반 액세스 제어 (RBAC)
RBAC의 기능과 사용 방법에 대해 살펴보겠습니다. 각 Azure 구독에는 Azure Active Directory가 있습니다. 사용자, 그룹 및 해당 디렉터리에서 응용 프로그램 hello 리소스 관리자 배포 모델을 사용 하는 hello Azure 구독에에서 대 한 액세스 toomanage 리소스를 부여할 수 있습니다. 참조 된 tooas 역할 기반 액세스 제어 (RBAC)입니다. toomanage 액세스이 hello를 사용할 수 있습니다 [Azure 포털](https://portal.azure.com/), hello [Azure CLI 도구](../../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), 또는 hello [Azure 저장소 리소스 공급자 REST Api ](https://msdn.microsoft.com/library/azure/mt163683.aspx).

Hello 리소스 관리자, 모델로 hello 저장소 계정 리소스 그룹 및 컨트롤 액세스 toohello 관리 평면에서 Azure Active Directory를 사용 하 여 해당 특정 저장소 계정의 넣을 있습니다. 예를 들어 사용자 제공할 수 있습니다 특정 hello 기능 tooaccess hello 저장소 계정 키를 다른 사용자가 hello 저장소 계정에 대 한 정보를 볼 수 있지만 hello 저장소 계정 키에 액세스할 수 없습니다.

#### <a name="granting-access"></a>액세스 권한 부여
적절 한 RBAC 역할 toousers hello, 그룹 및 응용 프로그램 hello 오른쪽 범위에서 할당 하 여 액세스가 허용 됩니다. toogrant 액세스 toohello 전체 구독을 hello 구독 수준에서 역할을 할당할 수 있습니다. 리소스 그룹의 hello 리소스 액세스 tooall 자체 사용 권한 toohello 리소스 그룹에 부여 하 여 부여할 수 있습니다. 저장소 계정 등의 toospecific 리소스 특정 역할에 할당할 수도 있습니다.

다음은 Azure 저장소 계정의 RBAC tooaccess hello 관리 작업을 사용 하는 방법에 대 한 tooknow 해야 하는 hello 주요 요점입니다.

* 액세스에 할당 하면 toohave 액세스 해야 하는 역할 toohello 계정을 기본적으로 할당 합니다. 해당 저장소 계정 액세스 toohello 사용 하는 작업 toomanage를 제어할 수 있지만 toohello 데이터가 아닌 hello 계정 개체. 예를 들어 tooretrieve hello 속성 hello 저장소 계정 (예: 중복) 있지만 하지 tooa 컨테이너 또는 Blob 저장소 내의 컨테이너 내에서 데이터의 사용 권한을 부여할 수 있습니다.
* 다른 사용자에 대 한 toohave 권한 tooaccess hello hello 저장소 계정에 데이터 개체, 권한 tooread hello 저장소 계정 키를 제공할 수 및 이러한 키 tooaccess hello blob, 큐, 테이블 및 파일 해당 사용자를 유도할 수 있습니다.
* Tooa 특정 사용자 계정, 사용자 또는 tooa 특정 응용 프로그램의 그룹 역할을 할당할 수 있습니다.
* 각 역할에는 작업 목록 및 작업 안 함 목록이 있습니다. 예를 들어 hello 참가자 가상 컴퓨터 역할에 "Listkey"의 작업 hello 저장소 계정 키 toobe 읽을 수 있도록 합니다. hello 참가자 hello Active Directory의에서 사용자에 대 한 hello 액세스를 업데이트 하는 등 "작업"에 있습니다.
* 여기 (않음 제한 되지 않습니다) 저장소에 대 한 역할 hello 다음:

  * 소유자 - 액세스를 제외한 모든 것을 관리할 수 있습니다.
  * 참가자-수행할 수 있는 아무 것도 할당 액세스 hello 소유자 외 수 있습니다. 이 역할을 가진 사람이 볼 수 있으며 hello 저장소 계정 키 다시 생성. Hello 저장소 계정 키를 가진 hello 데이터 개체를 액세스할 수 있습니다.
  * Reader-기밀 정보를 제외 하 고 hello 저장소 계정에 대 한 정보를 볼 수 있습니다. 예를 들어 hello 저장소 계정 toosomeone에 판독기 권한이 있는 역할을 할당 하는 경우 hello 저장소 계정의 hello 속성 볼 수 있지만 toohello 속성 변경을 수행 하거나 hello 저장소 계정 키를 볼 수는 없습니다.
  * 저장소 계정 참가자 – hello 저장소 계정을 관리할 수 있는 – 읽을 수 구독의 리소스 그룹 및 리소스를 hello와 만들고 구독 리소스 그룹 배포를 관리 합니다. Hello 데이터 평면 액세스할 수 있는 따라서 hello 저장소 계정 키를 액세스할 수 있습니다.
  * 사용자 액세스 관리자에 게 – 사용자 액세스 toohello 저장소 계정을 관리할 수 있습니다. 예를 들어, 판독기 액세스 tooa 특정 사용자를 부여할 수 있습니다.
  * 가상 컴퓨터 참가자 – 하지 hello 저장소 계정 toowhich 연결 되어 있지만 가상 컴퓨터를 관리할 수 있습니다. 이 역할에는이 역할을 할당 하는 사용자 toowhom hello을 의미 하는 hello 데이터 평면을 업데이트할 수 hello 저장소 계정 키를 나열할 수 있습니다.

    사용자 toocreate 가상 컴퓨터에 대 한 순서 대로 저장소 계정에서 toobe 수 toocreate hello 해당 VHD 파일을 갖게 됩니다. toobe 수 tooretrieve hello 저장소 필요 하다는, toodo 계정 키를 만드는 VM hello toohello API 전달. 따라서 이러한 권한이 있어야이 hello 저장소 계정 키를 나열할 수 있도록 합니다.
* hello 기능 toodefine 사용자 정의 역할은 Azure 리소스에서 수행할 수 있는 사용 가능한 작업 목록에서 동작 집합이 toocompose 수 있는 기능입니다.
* hello 사용자에 게 toobe 역할 toothem를 할당 하기 전에 Azure Active Directory에 설정 합니다.
* 가 부여/취소 를/보낸 및 PowerShell을 사용 하 여 어떤 범위에 대 한 액세스의 종류에 대 한 보고서를 만들거나 Azure CLI hello 수 있습니다.

#### <a name="resources"></a>리소스
* [Azure Active Directory 역할 기반 액세스 제어](../../active-directory/role-based-access-control-configure.md)

  이 문서에서는 hello 설명 Azure Active Directory 역할 기반 액세스 제어 및 청구 방식입니다.
* [RBAC: 기본 제공 역할](../../active-directory/role-based-access-built-in-roles.md)

  이 문서는 모든 RBAC에 사용할 수 있는 기본 제공 역할 hello 자세히 설명 합니다.
* [리소스 관리자 배포 및 클래식 배포 이해](../../azure-resource-manager/resource-manager-deployment-model.md)

  이 문서는 hello 리소스 관리자 배포 및 클래식 배포 모델에 설명 하 고 hello 리소스 관리자 및 리소스 그룹을 사용 하 여 hello 이점을 설명 합니다. Hello Azure 계산, 네트워크 및 저장소 공급자 hello 리소스 관리자 모델에서 작동 하는 방법을 설명 합니다.
* [Hello REST API로 역할 기반 액세스 제어 관리](../../active-directory/role-based-access-control-manage-access-rest.md)

  이 문서에서는 toouse REST API toomanage RBAC hello 하는 방법을 보여 줍니다.
* [Azure 저장소 리소스 공급자 REST API 참조](https://msdn.microsoft.com/library/azure/mt163683.aspx)

  Api 사용할 수 있습니다 toomanage 저장소 계정의 프로그래밍 방식으로 hello에 대 한 hello 참조입니다.
* [개발자 가이드 tooauth Azure 리소스 관리자 api](http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/)

  이 문서에서는 tooauthenticate를 사용 하 여 리소스 관리자 Api을 hello 하는 방법을 보여 줍니다.
* [Ignite를 사용한 Microsoft Azure에 대한 역할 기반 액세스 제어](https://channel9.msdn.com/events/Ignite/2015/BRK2707)

  이 hello 2015 MS Ignite 컨퍼런스에서 Channel 9 비디오 링크 tooa는입니다. 이 세션에 대 한 이야기 관리 및 Azure의 보고 기능에 액세스 하 고 Azure Active Directory를 사용 하 여 tooAzure 구독 액세스 보안에 대 한 모범 사례를 탐색 합니다.

### <a name="managing-your-storage-account-keys"></a>저장소 계정 키 관리
저장소 계정 키는 512 비트 문자열로 Azure에서 만들어진, 함께 hello 저장소 계정 이름 예: blob, 테이블, 큐 메시지 및 Azure 파일 공유에 파일 내에서 엔터티에 hello 저장소 계정에 저장 된 사용된 tooaccess hello 데이터 개체를 수 있습니다. 해당 저장소 계정에 대 한 데이터 평면 toohello 액세스 하는 저장소 계정 키 제어에 대 한 제어의 액세스 toohello 합니다.

각 저장소 계정에 참조 하는 두 개의 키 tooas "키 1"과 "2 키" hello [Azure 포털](http://portal.azure.com/) 및 hello PowerShell cmdlet. 이러한 다시 생성할 수 있습니다 수동으로 hello toousing 제한 되지 않음, 여러 가지 방법 중 하나를 사용 하 여 [Azure 포털](https://portal.azure.com/), PowerShell, hello Azure CLI 또는 프로그래밍 방식으로 사용 하 여 hello.NET 저장소 클라이언트 라이브러리 또는 Azure를 환영 저장소 서비스 REST API입니다.

저장소 계정 키 매우 이유 tooregenerate 다양 합니다.

* 보안상의 이유로 정기적으로 다시 생성할 수 있습니다.
* 누군가가 toohack 응용 프로그램으로 관리 하 고 tooyour 저장소 계정의 모든 권한을 부여 하드 코드 된 되었거나 구성 파일에 저장 된 hello 키를 검색할 경우에 저장소 계정 키를 다시 생성 됩니다.
* 키 다시 생성에 대 한 경우 팀 hello 저장소 계정 키를 유지 하는 저장소 탐색기 응용 프로그램을 사용 하 고 hello 팀 멤버 중 하나를 벗어날 경우에 합니다. hello 응용 프로그램 삭제 놓은 후 액세스 tooyour 저장소 계정을 제공 toowork를 계속 합니다. 이것은 실제로 hello 주된 이유 자신이 만든 계정 수준 공유 액세스 서명 – 구성 파일에 hello 선택 키를 저장 하는 대신 계정 수준 SAS를 사용할 수 있습니다.

#### <a name="key-regeneration-plan"></a>키 다시 생성 계획
몇 가지 계획 없이 사용 중인 toojust regenerate hello 키가 되기를 원하지 않습니다. 이렇게 하면 모든 액세스 toothat 저장소 계정으로 주요 중단을 일으킬 수 있는 잘릴 수 있습니다. 이 때문에 두 개의 키를 준비하는 것입니다. 한 번에 하나의 키를 다시 생성해야 합니다.

키를 다시 생성 하기 전에 Azure에서 사용 하는 다른 서비스 뿐 아니라 모든 hello 저장소 계정에 의존 하는 응용 프로그램의 목록이 있는 해야 합니다. 예를 들어 저장소 계정에 의존 하는 Azure 미디어 서비스를 사용 하는 경우 다시 동기화 해야 hello 선택 키 미디어 서비스와 함께 hello 키를 다시 생성 합니다. 저장소 탐색기와 같은 모든 응용 프로그램을 사용 하는 경우 tooprovide hello 새 키 toothose 응용 프로그램 에서도 할 수 있습니다. VHD 파일을 포함 hello 저장소 계정에 저장 된 Vm을 사용 하는 경우 이러한 영향을 않는지 수 hello 저장소 계정 키 다시 생성 하는 참고 합니다.

Hello Azure 포털에서에서 키를 다시 생성할 수 있습니다. 키 다시 생성 되 면 수 차지 too10 분 toobe 저장소 서비스에서 동기화 합니다.

준비 되 면 키를 변경 해야 하는 방법을 자세히 보여 주는 hello 일반 프로세스는 다음과 같습니다. 이 경우 hello 된다고 가정해 키 1 현재 사용 중인 및 보아야 toochange 모든 toouse 키 2를 대신 합니다.

1. 키 2 tooensure 안전 하다는 것을 다시 생성 합니다. Hello Azure 포털에서에서이 수행할 수 있습니다.
2. 모든 hello 저장소 키 저장 된 hello 응용 프로그램에서는 hello 저장소 키 toouse 키 2의 새 값을 변경 합니다. 테스트 하 고 hello 응용 프로그램을 게시 합니다.
3. 결국 hello의 응용 프로그램 및 서비스 실행 중이 고 다시 생성할 키 1 성공적으로 실행 합니다. 이렇게 하면 hello 새 키를 명시적으로 부여 받지 않은 toowhom가 더 이상 누구나 toohello 저장소 계정에 액세스 합니다.

현재 키 2를 사용 하는 경우에 hello 역방향 hello 키 이름 이지만 동일한 프로세스를 사용할 수 있습니다.

각 응용 프로그램 toouse hello 새 키를 변경 하 고 게시 일 전 부터는 며칠 동안 마이그레이션할 수 있습니다. 모두 완료 한 후 다음 돌아가서를 더 이상 작동 하도록 hello 이전 키를 다시 생성 합니다.

두 번째 방법은 tooput hello 저장소 계정 키에는 [Azure 키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/) 는 암호로 있고 프로그램 응용 프로그램 검색 hello 키를 여기에서. 그런 다음 hello 키 다시 생성 하 고 hello Azure 키 자격 증명 모음을 업데이트할 때 hello 응용 프로그램 toobe hello hello Azure 키 자격 증명 모음에서에서 새 키를 자동으로 선택 됩니다 때문에 다시 배포할 필요 하지 않습니다. Note 필요할 때마다 hello 키를 읽을 hello 응용 프로그램을 사용할 수 있습니다 또는 메모리에 캐시 하 고, 사용 하는 경우 실패할 경우 hello Azure 키 자격 증명 모음에서에서 hello 키를 다시 검색 합니다.

또한 Azure 키 자격 증명 모음을 사용하면 저장소 키에 대한 보안이 한 층 더 강화됩니다. 이 방법을 사용 하면 액세스 특정 사용 권한이 없는 toohello 키를 가져오는 다른 사람이 해당 수단을 제거 하는 구성 파일에서 hello 저장소 키 하드 코드 하지 해야 합니다.

Azure 키 자격 증명 모음을 사용 하 여의 또 다른 이점은입니다 액세스 tooyour 키를 Azure Active Directory를 사용 하 여 제어할 수 있습니다. 즉, toohello 약간의 Azure 키 자격 증명 모음에서 tooretrieve hello 키가 필요 하며 다른 응용 프로그램 수 없음을 권한을 부여 하지 않고 사용 권한을 구체적으로 수 tooaccess hello 키를 알고 있는 응용 프로그램 액세스 권한을 부여할 수 있습니다.

참고: 것이 좋습니다 toouse hello 중 하나에 키의 모든 hello에 대 한 응용 프로그램 같은 전용 시간입니다. 일부 상황에서는 키 1 및 있고 다른 키 2를 사용 하는 경우는 금지 됩니다 수 toorotate 일부 응용 프로그램 액세스 권한의 상실 없이 키 수입니다.

#### <a name="resources"></a>리소스
* [Azure 저장소 계정 정보](storage-create-storage-account.md#regenerate-storage-access-keys)

  이 문서에서는 저장소 계정에 대해 대략적으로 설명하고 저장소 액세스 키를 보고, 복사하고, 다시 생성하는 과정을 논의합니다.
* [Azure 저장소 리소스 공급자 REST API 참조](https://msdn.microsoft.com/library/mt163683.aspx)

  이 문서는 hello REST API를 사용 하 여 Azure 계정에 대 한 hello 저장소 계정 키를 검색 하 고 다시 생성 hello 저장소 계정 키에 대 한 링크 toospecific 문서를 포함 합니다. 참고: Resource Manager 저장소 계정에 대한 내용입니다.
* [저장소 계정에 대한 작업](https://msdn.microsoft.com/library/ee460790.aspx)

  Hello 저장소 서비스 관리자 REST API 참조의에서이 문서를 검색 및 재생성 hello REST API를 사용 하 여 hello 저장소 계정 키에 링크 toospecific 아티클을 포함 합니다. 참고: hello 클래식 저장소 계정에 대 한입니다.
* [Goodbye tookey 관리 말 – Azure AD를 사용 하 여 액세스 tooAzure 저장소 데이터를 관리 합니다.](http://www.dushyantgill.com/blog/2015/04/26/say-goodbye-to-key-management-manage-access-to-azure-storage-data-using-azure-ad/)

  이 문서 toouse Active Directory toocontrol Azure 키 자격 증명 모음의 tooyour Azure 저장소 키를 액세스 하는 방법을 보여 줍니다. 또한 toouse Azure 자동화는 시간 단위로 tooregenerate hello 키를 작업 하는 방법을 보여 줍니다.

## <a name="data-plane-security"></a>데이터 평면 보안
데이터 평면 보안 참조 toohello 메서드를 사용 하는 toosecure hello 데이터 개체는 Azure 저장소-hello blob, 큐, 테이블 및 파일에에서 저장 합니다. 방법 tooencrypt hello 데이터 및 보안 전송 hello 데이터 중 살펴본 하지만 toohello 개체 액세스를 허용 하는 방법에 대 한 여러분이?

자체 제어 액세스 toohello 데이터 개체를 위한 두 메서드는 기본적으로 합니다. hello 먼저 제어 액세스 toohello 저장소 계정 키를 여는 hello 두 번째는 개체 및 사용 공유 액세스 서명 toogrant 액세스 toospecific 데이터 특정 기간에 대 한 합니다.

하나의 예외 toonote는 hello blob을 적절 하 게 보관 하는 hello 컨테이너에 대 한 hello 액세스 수준을 설정 하 여 tooyour blob 공용 액세스를 허용할 수 있습니다. 컨테이너 tooBlob 또는 컨테이너에 대 한 액세스를 설정 하는 경우 해당 컨테이너에서 hello blob에 대 한 공용 읽기 액세스 권한을 허용 합니다. 이 hello 저장소 계정 키를 잃어버리거나 공유 액세스 서명을 사용 하지 않고 브라우저에서 열 수 해당 컨테이너에 tooa blob을 가리키는 URL에 있는 모든 사용자를 의미 합니다.

### <a name="storage-account-keys"></a>저장소 계정 키
저장소 계정 키는 hello 저장소 계정 이름과 함께 사용 되는 tooaccess hello 데이터 개체 hello 저장소 계정에 저장 될 수 있습니다 하는 Azure에서 만든 512 비트 문자열입니다.

예를 들어 있습니다 blob 읽고, tooqueues 작성, 테이블을 만들고 수정할 수 파일입니다. 이러한 작업 중 수행할 수 있으므로 Azure hello를 통해 포털 또는 많은 저장소 탐색기 응용 프로그램 중 하나를 사용 합니다. 작성할 수도 있습니다 코드 toouse hello REST API 또는 hello 저장소 클라이언트 라이브러리 tooperform 중 이러한 작업 합니다.

Hello에 hello 섹션에서 설명한 대로 [관리 평면 보안](#management-plane-security), 클래식 저장소 계정 전체 액세스 toohello Azure 구독을 제공 하 여 부여할 수 있습니다에 대 한 저장소 키 toohello 액세스 합니다. 역할 기반 액세스 제어 (RBAC)를 통해 hello Azure 리소스 관리자 모델을 사용 하 여 저장소 계정에 대 한 액세스 toohello 저장소 키를 제어할 수 있습니다.

### <a name="how-toodelegate-access-tooobjects-in-your-account-using-shared-access-signatures-and-stored-access-policies"></a>Toodelegate tooobjects 공유 액세스 서명 및 저장 된 액세스 정책을 사용 하 여 계정에 액세스 하는 방법
공유 액세스 서명 될 수 있는 보안 토큰을 포함 하는 문자열 연결 tooa toodelegate toostorage 개체 액세스를 허용 하는 URI 및 hello 사용 권한 및 액세스의 hello 날짜/시간 범위와 같은 제약 조건을 지정 합니다.

액세스 tooblobs, 컨테이너, 큐의 메시지, 파일 및 테이블을 부여할 수 있습니다. 사용 테이블을 부여할 수 있습니다 실제로 사용 권한을 tooaccess hello 테이블에서 엔터티 범위 hello 파티션 및 행 키 범위 toowhich hello 사용자 toohave 액세스를 지정 하 여 합니다. 예를 들어 지리적 상태의 파티션 키로 저장 된 데이터를 사용 하는 경우 지정할 수 있다 누군가가 toojust hello 데이터 액세스 캘리포니아에 대 한 합니다.

또 다른 예로, 웹 응용 프로그램 toowrite 항목 tooa 큐 수 있는 SAS 토큰을 제공할 수도 있으며 작업자 역할 응용 프로그램 큐에 대기 하 고 처리 하는 hello에서 SAS 토큰 tooget 메시지 제공 수 있습니다. 또는 한 명의 고객이 tooupload 그림 tooa 컨테이너를 사용 하 여 Blob 저장소에 수 있으며 웹 응용 프로그램 사용 권한 tooread 이러한 그림을 제공 하는 SAS 토큰을 부여할 수 있습니다. 두 경우 모두이 문제의 분리 – 각 응용 프로그램에 필요한 정당한 hello 액세스 권한을 부여할 수 tooperform 자신의 작업을 요청 합니다. 이것이 공유 액세스 서명의 hello 사용을 통해 가능 합니다.

#### <a name="why-you-want-toouse-shared-access-signatures"></a>공유 액세스 서명 toouse 이유
이유는 무엇 일까요 toouse 방금 아웃 훨씬 쉽습니다 사용자 저장소 계정 키를 지정 하는 대신 SAS? 저장소 계정 키를 제공할 공유 저장소 kingdom의 hello 키와 비슷합니다. 완전한 액세스 권한을 부여하게 됩니다. 사용자 수 키를 사용 하 여을 전체 음악 라이브러리 tooyour 저장소 계정으로 업로드 했습니다. 파일을 바이러스에 감염된 버전으로 바꿀 수도 있고 데이터를 훔칠 수도 있습니다. 무제한 액세스 tooyour 저장소 계정을 제공 lightly 수행 해야 하는 것입니다.

공유 액세스 서명에 hello 권한이 제한 된 기간에 대 한 클라이언트에 게 제공할 수 있습니다. 예를 들어 누군가가 blob tooyour 계정을 업로드 하는 경우 하면 부여할 수 (에 따라 hello blob의 hello 크기 물론) 되는 데 충분 한 시간 tooupload hello blob에 대 한 쓰기 액세스입니다. 또한 마음이 바뀌면 부여한 권한을 취소할 수 있습니다.

또한 SAS를 사용 하 여 요청이 특정 IP 주소 또는 IP 주소 범위 외부 tooAzure 제한 tooa 지 지정할 수 있습니다. 특정 프로토콜(HTTPS 또는 HTTP/HTTPS)을 사용하여 요청이 수행되도록 요구할 수도 있습니다. 즉, tooallow HTTPS 트래픽을 높은 사람만 hello 필요한 프로토콜 tooHTTPS만 설정할 수 있습니다 및 HTTP 트래픽을 차단 됩니다.

#### <a name="definition-of-a-shared-access-signature"></a>공유 액세스 서명의 정의
공유 액세스 서명을 쿼리 매개 변수 집합 추가 hello 리소스에서 가리키는 toohello URL입니다.

제공 하 hello 액세스에 대 한 정보 허용 되는 hello에 대 한 액세스가 허용 되는 시간의 길이 hello 됩니다. 다음은 예제입니다. 이 URI는 5 분 동안 tooa blob 읽기 액세스를 제공합니다. SAS 쿼리 매개 변수는 URL로 인코딩되어야 합니다(예: 콜론(:)의 경우 %3A, 공백의 경우 %20).

```
http://mystorage.blob.core.windows.net/mycontainer/myblob.txt (URL toohello blob)
?sv=2015-04-05 (storage service version)
&st=2015-12-10T22%3A18%3A26Z (start time, in UTC time and URL encoded)
&se=2015-12-10T22%3A23%3A26Z (end time, in UTC time and URL encoded)
&sr=b (resource is a blob)
&sp=r (read access)
&sip=168.1.5.60-168.1.5.70 (requests can only come from this range of IP addresses)
&spr=https (only allow HTTPS requests)
&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D (signature used for hello authentication of hello SAS)
```

#### <a name="how-hello-shared-access-signature-is-authenticated-by-hello-azure-storage-service"></a>어떻게 공유 액세스 서명을 의해 인증 됩니다 hello hello Azure 저장소 서비스
Hello 저장소 서비스는 hello 요청을 받으면 hello 입력된 쿼리 매개 변수를 사용 하 고 서명을 만듭니다 hello 호출 프로그램으로 동일한 방법을 hello를 사용 하 여 합니다. Hello 두 시그니처를 비교합니다. 동의 hello가 없으면 저장소 서비스 hello 저장소 서비스 버전 toomake 수 있는지를 확인, hello 현재 날짜 및 시간 내에 있는 지정 된 창 hello, toohello 요청 등을 해당 하는 요청 된 확인 되었는지 hello 액세스 확인 수 있습니다.

예를 들어 위의 URL이 있는 hello URL가 blob 대신 tooa 파일을 가리키는 경우이 요청 때문에 실패 해당 hello blob은 공유 액세스 서명을 지정 합니다. 나머지 명령은 호출 되 고 hello tooupdate blob 되었으면 hello 공유 액세스 서명을 지정 하므로 읽기 권한을 사용할 수 있는 실패 합니다.

#### <a name="types-of-shared-access-signatures"></a>공유 액세스 서명의 유형
* 서비스 수준 SAS 저장소 계정에 특정 리소스를 사용 하는 tooaccess 될 수 있습니다. 이 몇 가지 예는 컨테이너의 blob 목록을 검색 하는, 다운로드 blob, 테이블의 엔터티를 업데이트, tooa 큐 메시지 추가 또는 업로드 파일 tooa 파일 공유 합니다.
* 계정 수준 SAS 사용된 tooaccess 원하는 대로 입력할 수에 대 한 서비스 수준 SAS를 사용할 수 있는 합니다. 또한 것 hello 기능 toocreate 컨테이너, 테이블, 큐 및 파일 공유와 같은 서비스 수준 sa, 허용 되지 않는 옵션 tooresources를 제공할 수 있습니다. 또한 액세스 toomultiple 서비스를 한 번에 지정할 수 있습니다. 예를 들어 줄 수 있습니다 다른 사람이 tooboth blob 액세스 및 파일 저장소 계정에 있습니다.

#### <a name="creating-an-sas-uri"></a>SAS URI 만들기
1. 필요에 따라 될 때마다 모든 hello 쿼리 매개 변수 정의 임시 URI 만들 수 있습니다.

   이 방식은 정말 유연한 방법이지만 매번 비슷한 매개 변수의 논리적 집합을 사용한다면 저장된 액세스 정책을 사용하는 것이 더 좋습니다.
2. 전체 컨테이너, 파일 공유, 테이블 또는 큐에 대해 저장된 액세스 정책을 만들 수 있습니다. 그런 다음 hello 만들면 SAS Uri에 대 한 hello 기준으로 사용할 수 있습니다. 저장된 액세스 정책을 기준으로 하는 사용 권한은 쉽게 해지할 수 있습니다. 사용할 수 있습니다 각 컨테이너, 큐, 테이블 또는 파일 공유에서 정의 된 too5 정책을 합니다.

   예를 들어 toohave 바뀔 때 많은 사람들이 특정 컨테이너에서 hello blob을 읽고, "읽기 권한을 제공 합니다." 라고 표시 하는 저장 된 액세스 정책을 만들 수 있습니다 및 수 있는 다른 모든 설정을 hello 될 때마다 동일 합니다. 그런 다음 저장 된 액세스 정책 hello의 hello 설정을 사용 하 고 hello 만료 날짜/시간을 지정 하는 SAS URI를 만들 수 있습니다. hello이 이점이 toospecify 없는 모든 hello 될 때마다 쿼리 매개 변수입니다.

#### <a name="revocation"></a>해지
프로그램 SAS가 손상 된 또는 toochange를 원하는 경우를 가정해 볼 회사 보안 또는 규정 준수 요구 사항 때문에 해당 합니다. 해당 SAS를 사용 하 여 액세스 tooa 리소스를 어떻게 권한을 해지할 수 있습니다. Hello SAS URI를 생성 하는 방법에 따라 다릅니다.

임시 URI를 사용하는 경우 세 가지 옵션이 있습니다. 짧은 만료 정책을 사용 하 여 SAS 토큰을 발급할 수 있으며 단순히 hello SAS tooexpire 될 때까지 기다립니다. 이름을 변경 하거나 hello 리소스 (가정함 hello 토큰 tooa 범위가 지정 된 단일 개체)를 삭제할 수 있습니다. Hello 저장소 계정 키를 변경할 수 있습니다. 이 마지막 옵션 개수 서비스 해당 저장소 계정 사용에 따라 큰 영향을 줄 수 및 몇 가지 계획 없이 toodo 원하는 아닐 합니다.

저장 된 액세스 정책에서 파생 된 SAS를 사용 하는 저장 된 액세스 정책 hello를 취소 하 여 액세스를 제거할 수 있습니다 – 이미 만료 된 하거나 완전히 제거만 변경할 수 있습니다. 이러한 작업은 즉시 적용되며 해당 저장된 액세스 정책을 사용하여 만든 모든 SAS가 무효화됩니다. 업데이트 또는 제거 하는 hello 저장 된 액세스 정책에는 해당 특정 컨테이너, 파일 공유, 테이블 또는 큐 SAS 통해 액세스 하려는 사용자 영향을 줄 수 있지만 경우 hello 클라이언트는 기록 hello 기존 계획이 무효화 될 때 새 SAS 요청 되므로, 정상적으로 작동 합니다.

저장 된 액세스 정책에서 파생 된 SAS를 사용 하 여 제공 하기 때문에 SAS를 즉시 인지 hello 권장 모범 사례 tooalways hello 기능 toorevoke 가능 하면 저장 된 액세스 정책을 사용 합니다.

#### <a name="resources"></a>리소스
공유 액세스 서명 및 저장 된 액세스 정책에 예제가 포함 된 사용에 대 한 자세한 내용을 보려면 toohello 다음 문서를 참조 하십시오.

* 이들은 hello 참조 문서입니다.

  * [서비스 SAS(영문)](https://msdn.microsoft.com/library/dn140256.aspx)

    이 문서에서는 Blob, 큐 메시지, 테이블 범위 및 파일에서 서비스 수준 SAS를 사용하는 예제를 제공합니다.
  * [서비스 SAS 생성(영문)](https://msdn.microsoft.com/library/dn140255.aspx)
  * [계정 SAS 생성(영문)](https://msdn.microsoft.com/library/mt584140.aspx)
* 이들은 hello.NET 클라이언트 라이브러리 toocreate 공유 액세스 서명 및 저장 된 액세스 정책을 사용 하 여에 대 한 자습서입니다.

  * [SAS(공유 액세스 서명) 사용](../storage-dotnet-shared-access-signature-part-1.md)
  * [만들기 및 SAS를 사용 하 여 Blob 서비스 hello로 공유 액세스 서명, 2 부:](../blobs/storage-dotnet-shared-access-signature-part-2.md)

    Hello SAS 모델, 공유 액세스 서명의 예에 대 한 설명을 포함 하 고 sa hello 모범 사례에 대 한 권장 사항을 사용 합니다. Hello 해지 hello 사용 권한 부여는 대해서도 설명 합니다.
* IP 주소(IP ACL)를 통해 액세스 제한

  * [끝점 ACL(액세스 제어 목록)이란?](../../virtual-network/virtual-networks-acl.md)
  * [서비스 SAS 생성(영문)](https://msdn.microsoft.com/library/azure/dn140255.aspx)

    이 서비스 수준 SAS;에 대 한 hello 참조 문서 IP acling에 예제가 포함 됩니다.
  * [계정 SAS 생성(영문)](https://msdn.microsoft.com/library/azure/mt584140.aspx)

    계정 수준 SAS;에 대 한 hello 참조 문서입니다. IP acling에 예제가 포함 됩니다.
* 인증

  * [Hello Azure 저장소 서비스에 대 한 인증](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* 공유 액세스 서명 시작 자습서

  * [SAS 시작 자습서(영문)](https://github.com/Azure-Samples/storage-dotnet-sas-getting-started)

## <a name="encryption-in-transit"></a>전송 중 암호화
### <a name="transport-level-encryption--using-https"></a>전송 수준 암호화 - HTTPS 사용
Azure 저장소 데이터의 tooensure hello 보안을 수행 해야 하는 다른 단계는 클라이언트 hello와 Azure 저장소 간에 tooencrypt hello 데이터입니다. hello 제일 tooalways hello를 사용 하는 것 [HTTPS](https://en.wikipedia.org/wiki/HTTPS) 프로토콜을 통해 안전한 통신을 보장 하는 공용 인터넷 hello 합니다.

보안 통신 채널 toohave 해야 항상 HTTPS를 사용 하면 개체 저장소에 액세스 하거나 hello REST Api를 호출 하는 경우. 또한 **공유 액세스 서명**, tooAzure 저장소 개체에 액세스, 공유 액세스 서명, 모든 사용자가 확인을 사용 하는 경우 HTTPS 프로토콜을 사용할 수만 해당 hello 옵션 toospecify 포함 toodelegate 사용된 될 수 있습니다 링크와 SAS 토큰을 보내는 hello 적절 한 프로토콜을 사용 합니다.

저장소 계정에서 사용 하 여 hello REST Api tooaccess 개체를 호출할 때 HTTPS hello 사용을 적용할 수 있습니다 [보안 전송 필요](../storage-require-secure-transfer.md) hello 저장소 계정에 대 한 합니다. 설정된 경우 HTTP를 사용한 연결은 거부됩니다.

### <a name="using-encryption-during-transit-with-azure-file-shares"></a>전송 중에 Azure 파일 공유에 암호화 사용
Azure 파일 저장소 hello REST API를 사용 하는 경우 HTTPS를 지원 하지만 일반적으로 SMB 파일 공유 tooa VM 연결에 사용 합니다. SMB 2.1 암호화를 지원 하지 않으므로 연결이 허용 됩니다 hello 동일한 azure에서 지역입니다. 그러나 SMB 3.0 암호화를 지 원하는 및 Windows Server 2012 r 2에서 사용할 수, 액세스 및 hello 바탕 화면에 대 한 액세스를 포함 하 여 Windows 8, Windows 8.1 및 Windows 10에서 지역 간 수 있도록 합니다.

참고는 Unix와 Azure 파일 공유를 사용할 수 있지만 hello Linux SMB 클라이언트가 아직 지원 하지 않습니다 암호화, 액세스는 Azure 지역 내 에서만 허용 됩니다. Linux에 대 한 암호화 지원 SMB 기능을 수행 하는 Linux 개발자 로드맵 hello 켜져 있습니다. 나면 암호화를 추가 하는 경우 hello Windows의 경우와 마찬가지로 Linux의 경우 Azure 파일 공유에 액세스 하기 위한 동일한 기능이 있습니다.

사용 하도록 설정 하 여 hello를 사용 하 여 hello Azure 파일 서비스를 사용 하는 암호화를 적용할 수 있습니다 [보안 전송 필요](../storage-require-secure-transfer.md) hello 저장소 계정에 대 한 합니다. REST Api를 hello를 사용 하 여, HTTPs가 필요 합니다. SMB의 경우, 암호화를 지원하는 SMB 연결만 성공적으로 연결됩니다.

#### <a name="resources"></a>리소스
* [어떻게 toouse Linux로 Azure 파일 저장소](../storage-how-to-use-files-linux.md)

  이 문서에서는 Linux 시스템 및 업로드/다운로드 파일에 toomount Azure 파일을 공유 하는 방법을 설명 합니다.
* [Windows에서 Azure 파일 저장소 시작](../storage-dotnet-how-to-use-files.md)

  이 문서에서는 Azure 파일 공유에 대 한 개요와 방법을 toomount 사용할 PowerShell 및.NET을 사용 하 여 합니다.
* [Azure File Storage 내부 구조(영문)](https://azure.microsoft.com/blog/inside-azure-file-storage/)

  이 문서 hello Azure 파일 저장소의 일반적인 가용성을 알리는 hello SMB 3.0 암호화에 대 한 기술 정보를 제공 하며

### <a name="using-client-side-encryption-toosecure-data-that-you-send-toostorage"></a>Toostorage 보내는 클라이언트 쪽 암호화 toosecure 데이터를 사용 하 여
데이터가 클라이언트 응용 프로그램 및 저장소 간에 전송되는 동안 보안을 유지하는 데 도움이 되는 또 다른 옵션은 클라이언트 쪽 암호화입니다. hello 데이터는 Azure 저장소로 전송 하기 전에 암호화 됩니다. Azure 저장소에서 hello 데이터를 검색할 때 hello 클라이언트 쪽에서 받은 후 hello 데이터 암호가 해독 됩니다. Hello 네트워크를 통해 이동 hello 데이터가 암호화 되는 경우에 것이 좋습니다도 HTTPS를 사용 하는 hello 데이터의 hello 무결성에 영향을 주는 네트워크 오류를 완화할 수 있는 기본 제공 데이터 무결성 검사가 있습니다.

클라이언트 쪽 암호화 hello 데이터는 암호화 된 형식으로 저장 되어 있는 미사용 데이터를 암호화 하는 방법 이기도 합니다. 방법에 대해 알아보겠습니다이 hello 섹션에서 더 자세하게에서에 [휴지 암호화](#encryption-at-rest)합니다.

## <a name="encryption-at-rest"></a>휴지 상태의 암호화
휴지 상태의 암호화를 제공하는 세 가지 Azure 기능이 있습니다. Azure 디스크 암호화는 사용 되는 tooencrypt hello OS 및 데이터 디스크에서 IaaS 가상 컴퓨터는입니다. 두 개의 다른 hello-클라이언트 쪽 암호화 및 SSE-는 Azure 저장소에 사용 되는 tooencrypt 데이터 모두 합니다. 이러한 각 방법을 살펴보고 비교한 후 각 방법을 사용할 수 있는 경우를 확인해 보겠습니다.

Hello 전송 하는 동안 toosimply 사용 하 여 HTTPS를 선호 하 고 hello 데이터 toobe 되었을 때 자동으로 암호화에 대 한 몇 가지 방법이 될 수 있습니다 (저장소에서 암호화 된 형태로 저장도)이 표시 되는 전송 중에 클라이언트 쪽 암호화 tooencrypt hello 데이터를 사용할 수 있지만 저장 됩니다. 있는 경우 두 가지 방법으로 toodo이-SSE 및 Azure 디스크 암호화 사용 하는 toodirectly hello 데이터 Vm을 사용 하 여 OS 및 데이터 디스크를 암호화 되며 다른 hello tooAzure Blob 저장소를 쓴 tooencrypt 사용 되는 데이터입니다.

### <a name="storage-service-encryption-sse"></a>SSE(저장소 서비스 암호화)
SSE는 hello 저장소 서비스 tooAzure 저장소를 작성할 때 자동으로 hello 데이터를 암호화 하는 toorequest이 있습니다. Azure 저장소에서 hello 데이터를 읽을 때 반환 하기 전에 hello 저장소 서비스에서 해독할 수 됩니다. 그러면 toosecure toomodify 필요 없이 데이터는 코드 또는 코드 tooany 응용 프로그램을 추가할 수 있습니다.

이것이 toohello 전체 저장소 계정에 적용 되는 설정입니다. 사용 및 hello hello 설정 값을 변경 하 여이 기능을 비활성화할 수 있습니다. toodo이 hello Azure 포털, PowerShell hello Azure CLI를 사용 하 여 hello 저장소 리소스 공급자 REST API 또는.NET 저장소 클라이언트 라이브러리를 hello 수 있습니다. 기본적으로 SSE는 꺼져 있습니다.

이때 hello 키 hello 암호화에 사용 되는 Microsoft에서 관리 됩니다. 원래 hello 키를 생성 하 고 내부 Microsoft 정책에 의해 정의 된 대로으로 hello 키 hello 일반 회전 hello 안전한 저장소를 관리 합니다. Hello 이후에서 hello 기능 toomanage 직접 암호화 키를 얻을 쿼리하고 키 toocustomer 관리 되는 Microsoft에서 관리 하는 키에서의 마이그레이션 경로 제공 합니다.

이 기능은 hello 리소스 관리자 배포 모델을 사용 하 여 만든 표준 및 프리미엄 저장소 계정에 사용할 수 있습니다. SSE에는 추가 blob 및 tooblock blob만, 페이지 blob을 적용 합니다. hello 다른 유형의 데이터를 테이블, 큐 및 파일을 포함 하 여 암호화 되지 않습니다.

SSE 사용 하 고 hello 데이터가 저장소 tooBlob 기록에 데이터가 암호화 됩니다. SSE를 사용하거나 사용하지 않도록 설정해도 기존 데이터에는 영향을 주지 않습니다. 즉,이 암호화를 사용 하도록 설정 하면 하지 이전 단계로 이동 하 고 이미 있습니다; 데이터 암호화 도 SSE를 사용 하지 않도록 설정 하는 경우 이미 존재 하는 hello 데이터를 해독 합니다.

클래식 저장소 계정 사용 하 여이 기능 toouse을 원하는 경우 새 리소스 관리자 저장소 계정을 만들고 AzCopy toocopy hello 데이터 toohello 새 계정을 사용 합니다.

### <a name="client-side-encryption"></a>클라이언트 쪽 암호화
설명한 대로 클라이언트 쪽 암호화 hello 전송 되는 데이터의 hello 암호화에 논의 하는 경우. 이 기능은 있습니다 tooprogrammatically hello 와이어 toobe tooAzure 저장소 작성을 통해 보낼 클라이언트 응용 프로그램에서 데이터를 암호화 하 고 tooprogrammatically Azure 저장소에서 검색 한 후 데이터를 암호 해독할 수 있습니다.

이에서는 전송 중에 암호화를 제공 하지만 또한 미사용 데이터 암호화의 hello 기능을 제공 합니다. 참고는 hello 데이터 전송 중에 암호화 되어 있지만 여전히 사용할 수 있는 권장 HTTPS tootake 활용 hello 기본 제공 데이터 무결성 hello 데이터의 hello 무결성에 영향을 주는 네트워크 오류를 완화할 수 있는 것을 확인 합니다.

이 사용할 수 있는의 예에는 blob을 저장 하 고 blob을 검색 하는 웹 응용 프로그램 있고 원하는 hello 응용 프로그램 및 데이터 toobe 최대한 안전 하 게 됩니다. 이 경우 클라이언트 쪽 암호화를 사용할 수 있습니다. 암호화 hello 리소스를 포함 하는 클라이언트 hello와 hello Azure Blob 서비스 간에 트래픽을 hello 및 아무도 hello 전송 되는 데이터를 해석 하 고 개인 blob에 다시 구성할 수 있습니다.

클라이언트 쪽 암호화 변환은 hello Java 및 hello 있습니다 tooimplement 상당히 쉽게 Azure 키 자격 증명 모음 Api를 사용 하는 hello.NET 저장소 클라이언트 라이브러리를에 있습니다. hello 데이터 암호화 및 해독 hello 과정 hello 봉투 (envelope) 기술을 사용 하 고 각 저장소 개체에 hello 암호화에서 사용 하는 메타 데이터를 저장 합니다. 예를 들어 blob의 경우 저장 hello blob 메타 데이터에서 대기열에 있는 동안 해당 tooeach 큐 메시지 추가 합니다.

자체 hello 암호화를 위해 생성 하 고 직접 암호화 키를 관리할 수 있습니다. Hello Azure 저장소 클라이언트 라이브러리에서 생성 한 키를 사용할 수도 있습니다. 또는 Azure 키 자격 증명 모음 hello hello 키를 생성 합니다. 온-프레미스 키 저장소에 암호화 키를 저장하거나 Azure 키 자격 증명 모음에 저장할 수 있습니다. Azure 키 자격 증명 모음에 Azure Active Directory를 사용 하 여 Azure 키 자격 증명 모음 toospecific 사용자 toogrant 액세스 toohello 암호를 허용 합니다. 이 뿐 아니라 모든 hello Azure 키 자격 증명 모음 읽기 및 클라이언트 쪽 암호화에 사용할 hello 키를 검색할 수 있는지를 의미 합니다.

#### <a name="resources"></a>리소스
* [Microsoft Azure 저장소에서 Azure 키 자격 증명 모음을 사용하여 Blob 암호화 및 해독](../blobs/storage-encrypt-decrypt-blobs-key-vault.md)

  이 문서에서는 어떻게 toocreate KEK hello 하 고 PowerShell을 사용 하 여 hello 자격 증명 모음에 저장 하는 방법을 포함 하 여 Azure 키 자격 증명 모음과 toouse 클라이언트 쪽 암호화 합니다.
* [Microsoft Azure 저장소용 클라이언트 쪽 암호화 및 Azure 키 자격 증명 모음](../storage-client-side-encryption.md)

  이 문서는 클라이언트 쪽 암호화에 대 한 설명을 제공 하 고 hello 저장소 클라이언트 라이브러리 tooencrypt 및 암호 해독 리소스 hello 4 개의 저장소 서비스에서 사용 하는 예제를 제공 합니다. 또한 Azure 키 자격 증명 모음에 대해서도 설명합니다.

### <a name="using-azure-disk-encryption-tooencrypt-disks-used-by-your-virtual-machines"></a>Azure 디스크 암호화를 사용 하 여 tooencrypt 디스크를 사용할 가상 컴퓨터
Azure Disk Encryption을 새로운 기능입니다. 이 기능은 tooencrypt hello OS 디스크 및 IaaS 가상 컴퓨터에서 사용 되는 데이터 디스크입니다. Windows hello 드라이브는 업계 표준 BitLocker 암호화 기술을 사용 하 여 암호화 됩니다. Linux 용 hello 디스크 hello DM 암호화 기술을 사용 하 여 암호화 됩니다. 이 Azure 키 자격 증명 모음 tooallow 있습니다 toocontrol와 통합 hello 디스크 암호화 키를 관리 합니다.

hello 솔루션 hello Microsoft Azure에서 설정 된 경우 IaaS Vm에 대 한 다음 시나리오를 지원 합니다.

* Azure Key Vault와 통합
* 표준 계층 VM: [A, D, DS, G, GS 등 시리즈 IaaS VM](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Windows 및 Linux IaaS VM에서 암호화 사용
* Windows IaaS VM에 대한 OS 및 데이터 드라이브에서 암호화 사용 안 함
* Linux IaaS VM에 대한 데이터 드라이브에서 암호화 사용 안 함
* Windows 클라이언트 OS를 실행하는 IaaS VM에서 암호화 사용
* 탑재 경로가 있는 볼륨에서 암호화 사용
* mdadm을 사용하여 디스크 스트라이프(RAID)로 구성된 Linux VM에서 암호화 사용
* 데이터 디스크에 대해 LVM을 사용하여 Linux VM에서 암호화 사용
* 저장소 공간을 사용하여 구성된 Windows VM에서 암호화 사용
* 모든 Azure 공용 지역 지원됨

hello 솔루션 시나리오, 기능 및 기술 hello 릴리스에서 다음 hello를 지원 하지 않습니다.

* 기본 계층 IaaS VM
* Linux IaaS VM에 대한 OS 드라이브에서 암호화 사용 안 함
* Hello 클래식 VM 만들기 방법을 사용 하 여 만들어진 IaaS Vm
* 온-프레미스 키 관리 서비스와의 통합
* Azure File Storage(공유 파일 시스템), NFS(네트워크 파일 시스템), 동적 볼륨, 소프트웨어 기반 RAID 시스템으로 구성된 Windows VM


> [!NOTE]
> Linux 배포를 수행 하는 hello에서 Linux OS 디스크 암호화는 현재 지원: RHEL 7.2, 7.2n, CentOS 및 Ubuntu 16.04 합니다.
>
>

이 기능은 가상 컴퓨터 디스크에 있는 모든 데이터가 휴지 상태로 Azure 저장소에 암호화되도록 합니다.

#### <a name="resources"></a>리소스
* [Windows 및 Linux IaaS VM용 Azure 디스크 암호화](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)

### <a name="comparison-of-azure-disk-encryption-sse-and-client-side-encryption"></a>Azure 디스크 암호화, SSE 및 클라이언트 쪽 암호화의 비교
#### <a name="iaas-vms-and-their-vhd-files"></a>IaaS VM 및 해당 VHD 파일
IaaS VM에서 사용되는 디스크의 경우 Azure 디스크 암호화를 사용하는 것이 좋습니다. 해당 디스크를 Azure 저장소에 사용 되는 tooback 않은 SSE tooencrypt hello VHD 파일에서 설정할 수 있지만 새로 작성된 된 데이터를 암호화만. 즉, VM을 만들고 SSE hello VHD 파일을 보유 하는 hello 저장소 계정에서 사용 하도록 설정 하는 경우 hello 변경 내용만 암호화 됩니다, 그리고 원본 VHD 파일을 hello 하지 않습니다.

Azure에서 Azure 마켓플레이스 hello에서 이미지를 사용 하는 VM을 만드는 경우는 [복사 shallow](https://en.wikipedia.org/wiki/Object_copying) hello 이미지 tooyour의 Azure 저장소에 저장소 계정 암호화 되지 않은 SSE를 사용할 수 있는 경우에 합니다. Hello VM을 만들고 hello 이미지 업데이트를 시작, 후 SSE hello 데이터 암호화 시작 됩니다. 이 따라서 최상의 toouse 완벽 하 게 암호화 하 고 싶은 경우 hello Azure 마켓플레이스 이미지에서 생성 되는 Vm에 Azure 디스크 암호화는 합니다.

온-프레미스에서 Azure에 미리 암호화 된 VM를 가져올 경우 있습니다 수 tooupload hello 암호화 키 tooAzure 주요 자격 증명 되며 온-프레미스를 사용한 해당 VM에 대 한 hello 암호화를 사용 하 여 계속 합니다. Azure 디스크 암호화 사용된 toohandle이이 시나리오입니다.

온-프레미스에서 암호화 되지 않은 VHD를 설정한 경우에 사용자 지정 이미지로 hello 갤러리에 업로드 하 고에서 VM을 프로 비전 수 있습니다. 경우 hello 리소스 관리자 템플릿을 사용 하 여이 작업을 수행을 요청할 수 있습니다 것 tooturn Azure 디스크 암호화 hello VM 부팅 하는 경우.

데이터 디스크를 추가 하 고 hello VM에 탑재 하는 경우 해당 데이터 디스크에 Azure 디스크 암호화를 켤 수 있습니다. 먼저 해당 데이터 디스크를 로컬로 암호화 하므로 하 고 저장소에 대해 지연 쓰기 hello 저장소 콘텐츠는 암호화 되므로 hello 서비스 관리 계층은 다음 실행 합니다.

#### <a name="client-side-encryption"></a>클라이언트 쪽 암호화
클라이언트 쪽 암호화는 전송 하기 전에 암호화 하 고 미사용 hello 데이터를 암호화 하기 때문에 데이터를 암호화의 hello 가장 안전한 방법입니다. 그러나 없어도 코드 tooyour 할 필요가 있는 저장소를 사용 하 여 응용 프로그램을 추가 하는 toodo 합니다. 이러한 경우에 전송 중인 데이터 및 저장 된 상태의 SSE tooencrypt hello 데이터에 대 한 HTTPs를 사용할 수 있습니다.

클라이언트 쪽 암호화를 사용하여 테이블 엔터티, 큐 메시지 및 Blob을 암호화할 수 있습니다. SSE를 사용하면 blob만 암호화할 수 있습니다. 테이블 및 큐 데이터 toobe 암호화 해야 할 경우에 클라이언트 쪽 암호화를 사용 해야 합니다.

클라이언트 쪽 암호화 hello 응용 프로그램에서 완전히 관리 됩니다. 이 hello 가장 안전한 방법 이지만 않습니다 요구 toomake 프로그래밍 방식으로 변경 내용을 tooyour 응용 프로그램 하 고 키 관리 프로세스를 제 자리에 배치 합니다. 사용이 hello 하려는 경우 추가 보안 전송 중 원하는 암호화 하 여 저장 된 데이터 toobe 합니다.

클라이언트 쪽 암호화는 더 많은 부하를 hello 클라이언트에 있고 tooaccount이에 대 한 확장성 계획에 암호화 하 고 많은 양의 데이터를 전송 하는 경우에 특히 합니다.

#### <a name="storage-service-encryption-sse"></a>SSE(저장소 서비스 암호화)
SSE는 Azure Storage에 의해 관리됩니다. 전송 중인 hello 데이터의 보안을 hello에 대 한 SSE를 사용 하는 제공 하지 않지만 tooAzure 저장 될 때 hello 데이터 암호화지 않습니다. 이 기능을 사용할 때 hello 성능에 영향을 미치지 않습니다.

SSE를 사용하여 블록 Blob, 추가 Blob 및 페이지 Blob만 암호화할 수 있습니다. Tooencrypt 테이블 데이터 또는 큐 데이터를 필요한 경우 클라이언트 쪽 암호화를 사용 하는 것이 좋습니다.

보관 파일이 나 라이브러리 새 가상 컴퓨터를 만들기 위한 기준으로 사용 하는 VHD 파일의 경우 새 저장소 계정 만들기, SSE를 사용 하도록 설정 및 다음 업로드할 수 hello VHD 파일 toothat 계정. 이러한 VHD 파일은 Azure 저장소에 의해 암호화됩니다.

VM 및 SSE hello VHD 파일을 보유 하는 hello 저장소 계정에서 사용할 수 있는 hello 디스크에 설정 된 Azure 디스크 암호화가 작동 하는지 제대로; 한 번 더 암호화 되 고 새로 작성 된 데이터에 발생 합니다.

## <a name="storage-analytics"></a>저장소 분석
### <a name="using-storage-analytics-toomonitor-authorization-type"></a>Storage Analytics toomonitor 권한 부여 유형을 사용 하 여
각 저장소 계정에 대 한 Azure 저장소 분석 tooperform 로깅을 사용 하도록 설정 하 및 메트릭 데이터를 저장할 수 있습니다. 이 좋은 도구 toouse 원하는 저장소 계정의 toocheck hello 성능 메트릭 또는 성능 문제가 발생 하는 때문에 tootroubleshoot 저장소 계정이 필요 합니다.

Hello 저장소 분석 로그에서 볼 수 있는 데이터의 다른 부분에는 저장소에 액세스할 때 사용자가 사용 하는 hello 인증 방법입니다. 예를 들어 Blob 저장소 사용 hello 저장소 계정 키 또는 공유 액세스 서명을 사용 되는지에 또는 액세스 하는 hello blob가 public 인 경우 볼 수 있습니다.

이 액세스 toostorage 호위 밀접 하 게 하는 경우에 매우 유용할 수 있습니다. 예를 들어 Blob 저장소에 모든 hello 컨테이너 tooprivate를 hello를 사용 하 여 SAS 서비스의 응용 프로그램 전체 구현 합니다. 다음 보안 위반을 나타낼 수 있습니다, hello 저장소 계정 키를 사용 하 여 blob 액세스 되는 경우 또는 hello blob는 공용 이지만 되지 않아야 하는 경우 hello 기록 toosee 정기적으로 검사할 수 있습니다.

#### <a name="what-do-hello-logs-look-like"></a>수행 hello 로그 모양을?
Hello 저장소 계정 메트릭이 사용 하도록 설정 하 고 hello Azure 포털을 통해 로깅, 분석 데이터는 시작 tooaccumulate 신속 하 게 합니다. hello 로깅 및 각 서비스에 대 한 메트릭을 별도; hello 로깅은 1 분 마다, 매시간 또는 매일 구성 하는 방법에 따라 hello 메트릭 로깅됩니다 하는 동안 해당 저장소 계정에서 작업이 없을 경우에 기록 됩니다.

hello 로그 라는 $logs hello 저장소 계정에서 컨테이너의 블록 blob에 저장 됩니다. 이 컨테이너는 저장소 분석이 사용되도록 설정되면 자동으로 만들어집니다. 이 컨테이너가 만들어지면 해당 내용은 삭제할 수 있지만 컨테이너 자체는 삭제할 수 없습니다.

Hello $logs 컨테이너 아래에서 각 서비스에 대 한 폴더 않으며 다음 하위 폴더에 내용이 hello 연도/월/일/시간입니다. 1 시간에서 hello 로그 번호가 지정 하기만 하면 됩니다. 이 어떤 hello 디렉터리 구조는 같습니다.

![로그 파일 보기](./media/storage-security-guide/image1.png)

모든 요청 tooAzure 저장소에 기록 됩니다. 다음은 hello 처음 몇 개의 필드를 표시 하는 로그 파일의 스냅숏입니다.

![로그 파일 스냅숏](./media/storage-security-guide/image2.png)

사용할 수 있는 hello 로그 tootrack 호출 tooa 저장소 계정의 모든 종류를 확인할 수 있습니다.

#### <a name="what-are-all-of-those-fields-for"></a>이러한 모든 필드의 용도는 무엇인가요?
Hello 목록이 hello hello 로그 및 용도 대 한 많은 필드를 제공 하는 문서 hello 리소스 아래에 나와 있습니다. 필드 순서 hello 목록은 다음과 같습니다.

![로그 파일의 필드 스냅숏](./media/storage-security-guide/image3.png)

GetBlob에 대 한 hello 항목에 관심이 인증 되는 방법 이므로 toolook 작업 유형 "Get-Blob"가 포함 된 항목 및 필요 hello 요청 상태를 확인 및 (4<sup>번째</sup> 열) 및 hello 인증 유형 (8<sup>번째</sup> 열)입니다.

예를 들어에 hello 처음 몇 행 위의 hello 목록에서 hello 요청 상태는 "성공"이 고 hello 권한 부여 유형을 "인증"입니다. 즉, hello 저장소 계정 키를 사용 하 여 hello 요청 유효성을 검사 합니다.

#### <a name="how-are-my-blobs-being-authenticated"></a>Blob은 어떻게 인증되나요?
우리는 다음 세 가지 경우에 관심이 있습니다.

1. hello blob는 공용 이며 없이 공유 액세스 서명 URL을 사용 하 여 액세스. 이 경우 hello 요청 상태 "AnonymousSuccess" 되며 "익명" hello 권한 부여-유형입니다.

   1.0;2015-11-17T02:01:29.0488963Z;GetBlob;**AnonymousSuccess**;200;124;37;**anonymous**;;mystorage…
2. hello blob는 전용 포트 이며 공유 액세스 서명을 사용 되었습니다. 이 경우 hello 요청 상태 "SASSuccess" 되며 hello 권한 부여-유형 "sas"입니다.

   1.0;2015-11-16T18:30:05.6556115Z;GetBlob;**SASSuccess**;200;416;64;**sas**;;mystorage…
3. hello blob는 전용 포트 이며 hello 저장소 키를 사용 하는 tooaccess 것입니다. 이 경우 hello 요청 상태는 "**성공**"및 hello 권한 부여 형식이"**인증**"입니다.

   1.0;2015-11-16T18:32:24.3174537Z;GetBlob;**Success**;206;59;22;**authenticated**;mystorage…

Microsoft 메시지 분석기 tooview hello를 사용 하 고 이러한 로그를 분석할 수 있습니다. 여기에는 검색 및 필터링 기능이 포함되어 있습니다. 에 대 한 toosearch 할 수는 예를 들어 GetBlob toosee hello 사용량이 예상 대로 인스턴스의 toomake 다른 사용자에 액세스 하지 않는 저장소 계정의 부적절 하 게 선택 되어 있는지, 즉 합니다.

#### <a name="resources"></a>리소스
* [저장소 분석](../storage-analytics.md)

  이 문서는 storage analytics의 개요 및 방법을 tooenable 해당 합니다.
* [저장소 분석 로그 형식](https://msdn.microsoft.com/library/azure/hh343259.aspx)

  이 문서에서는 hello 저장소 분석 로그 형식 설명 및 세부 정보 hello 사용 가능한 필드 본 등 인증 유형 hello 요청에 사용 되는 인증의 hello 형식을 나타냅니다.
* [Hello Azure 포털에서에서 저장소 계정을 모니터링합니다](../storage-monitor-storage-account.md)

  이 문서에서는 어떻게 tooconfigure 메트릭을 모니터링 하 고 저장소 계정에 대 한 로깅.
* [Azure 저장소 메트릭 및 로깅, AzCopy 및 Message Analyzer를 사용한 종단 간 문제 해결](../storage-e2e-troubleshooting.md)

  이 문서는 hello Storage Analytics를 사용 하 여 문제를 해결 하는 방법에 대 한 설명 하 고 toouse Microsoft 메시지 분석기 hello 하는 방법을 보여 줍니다.
* [Microsoft Message Analyzer 운영 가이드](https://technet.microsoft.com/library/jj649776.aspx)

  이 문서 hello Microsoft 메시지 분석기에 대 한 hello 참조 이며 링크 tooa 자습서, 빠른 시작 및 기능 요약을 포함 됩니다.

## <a name="cross-origin-resource-sharing-cors"></a>CORS(크로스-원본 자원 공유)
### <a name="cross-domain-access-of-resources"></a>리소스의 도메인 간 액세스
한 도메인에서 실행되는 웹 브라우저가 다른 도메인의 리소스에 대해 HTTP 요청을 수행하는 경우를 크로스-원본 HTTP 요청이라고 합니다. 예를 들어 contoso.com에서 제공되는 HTML 페이지에서 fabrikam.blob.core.windows.net에서 호스트되는 jpeg를 요청한다고 가정합니다. 보안상의 이유로 브라우저는 JavaScript와 같은 스크립트 내에서 시작된 크로스-원본 HTTP 요청을 제한합니다. 즉, 일부 JavaScript 코드 contoso.com에서 웹 페이지에서 해당 jpeg fabrikam.blob.core.windows.net에를 요청 하면 hello 브라우저 hello 요청 없도록 합니다.

이 용도 Azure 저장소와 toodo? JSON 또는 XML 데이터 파일 등의 정적 자산을 저장 하는 경우 Blob 저장소의 저장소 계정을 사용 하 여 호출 Fabrikam hello 자산에 대 한 hello 도메인 fabrikam.blob.core.windows.net, 됩니다 고 hello contoso.com에 대 한 웹 응용 프로그램 수 tooaccess 됩니다에 JavaScript를 사용 하 여 hello 도메인 다르기 때문에 있습니다. 도 toocall hello –와 같은 테이블 저장소-Azure 저장소 서비스 중 하나를 JSON 데이터 toobe hello JavaScript 클라이언트에서 처리를 반환 하는 중 어느 것에 마찬가지입니다.

#### <a name="possible-solutions"></a>가능한 해결 방법
한 가지 방법은 tooresolve tooassign "storage.contoso.com" toofabrikam.blob.core.windows.net 같은 사용자 지정 도메인입니다. hello 문제는 해당 사용자 지정 도메인 tooone 저장소 계정만 할당할 수 있습니다. 경우에 어떻게 hello 자산이 여러 저장소 계정에 저장 된?

또 다른 방법은 tooresolve hello 저장소 호출에 대 한 프록시 act toohave hello 웹 응용 프로그램입니다. 즉 파일 tooBlob 저장소에 업로드 하는 경우 hello 웹 응용 프로그램은 로컬로 작성 또는 tooBlob 저장소에 복사 하거나 해당 내용을 모두 메모리에 읽기 및 tooBlob 저장소 작성 합니다. 또는 hello 파일을 로컬로 업로드 하 고 tooBlob 저장소에 기록 하는 Web API) (예: 전용된 웹 응용 프로그램을 작성할 수 있습니다. 어떤 방법을 사용 하 든 한 tooaccount 해당 함수에 대 한 결정 hello 확장성 요구 됩니다.

#### <a name="how-can-cors-help"></a>CORS는 어떻게 도움이 될까요?
Azure 저장소 tooenable를 CORS – 교차 원본 자원 공유 있습니다. 각 저장소 계정에 대 한 hello 리소스 해당 저장소 계정에 액세스할 수 있는 도메인을 지정할 수 있습니다. 예를 들어, 경우에는 위에서 설명한에서는 수 hello fabrikam.blob.core.windows.net 저장소 계정에서 CORS를 사용 하도록 설정 하 고 tooallow 액세스 toocontoso.com 구성 합니다. 다음 hello 웹 응용 프로그램 contoso.com fabrikam.blob.core.windows.net의 hello 리소스에 직접 액세스할 수 있습니다.

한 가지 toonote CORS 액세스를 허용 하지만 필요한에 대 한 모든 public이 아닌 액세스 저장소 리소스의 인증을 제공 하지 않으며입니다. 즉,만 액세스할 수 blob는 공용 또는 공유 액세스 서명을 제공을 포함 하는 경우 적절 한 사용 권한이 hello 합니다. 테이블, 큐 및 파일의 경우에는 공용 액세스가 없으므로 SAS가 필요합니다.

기본적으로 CORS는 모든 서비스에서 사용되지 않도록 설정되어 있습니다. CORS hello REST API 또는 hello 저장소 클라이언트 라이브러리 toocall hello 메서드 tooset hello 서비스 정책 중 하나를 사용 하 여 사용할 수 있습니다. 이렇게 할 때 XML에 있는 CORS 규칙을 포함합니다. 저장소 계정에 대 한 hello Blob 서비스에 대 한 hello Set Service Properties 작업을 사용 하 여 설정 된 CORS 규칙의 예를 들면 다음과 같습니다. Azure 저장소에 대 한 hello 저장소 클라이언트 라이브러리 또는 hello REST Api를 사용 하 여 해당 작업을 수행할 수 있습니다.

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

각 행의 의미는 다음과 같습니다.

* **AllowedOrigins** 그러면 일치 하지 않는 도메인에서 요청 하 고 hello 저장소 서비스에서 데이터를 받을 수 있습니다. 이것은 contoso.com과 fabrikam.com 둘 다 특정 저장소 계정에 대한 Blob 저장소에서 데이터를 요청할 수 있음을 의미합니다. 이 tooa 와일드 카드를 설정할 수도 있습니다 (\*) tooallow 모든 도메인 tooaccess 요청 합니다.
* **AllowedMethods** hello 요청을 만드는 경우 사용할 수 있는 방법 (HTTP 요청 동사) 중 hello 목록입니다. 이 예제에서는 PUT 및 GET만 허용됩니다. 이 tooa 와일드 카드를 설정할 수 있습니다 (\*) 사용 하는 모든 메서드 toobe tooallow 합니다.
* **AllowedHeaders** hello 요청을 만드는 경우 원본 도메인 hello 헤더를 지정할 수는 hello 요청입니다. 이 예제에서는 x-ms-meta-data, x-ms-meta-target 및 x-ms-meta-abc로 시작하는 모든 메타데이터 헤더를 지정할 수 있습니다. hello 와일드 카드 문자 (\*) hello로 시작 되는 헤더 접두사를 사용할 수 지정 했음을 나타냅니다.
* **ExposedHeaders** 그러면, 응답 헤더를 hello 브라우저 toohello 요청 발급자에 의해 노출 되어야 합니다. 이 예제에서는 "x-ms-meta-"로 시작하는 모든 헤더가 노출됩니다.
* **MaxAgeInSeconds** hello 브라우저는 hello 실행 전 OPTIONS 요청을 캐시 하는 최대 크기입니다. (Hello 실행 전 요청에 대 한 자세한 내용은 다음 첫 번째 문서 hello 확인).

#### <a name="resources"></a>리소스
CORS에 대 한 자세한 내용은 방법과 tooenable, 이러한 리소스를 확인 하십시오.

* [Hello azure.com Azure 저장소 서비스에 대 한 크로스-원본 자원 공유 (CORS) 지원](../storage-cors-support.md)

  이 문서에서는 CORS 및 tooset hello hello 다른 저장소 서비스에 대 한 규칙의 방식에 대 한 개요를 제공 합니다.
* [Hello MSDN의 Azure 저장소 서비스에 대 한 크로스-원본 자원 공유 (CORS) 지원](https://msdn.microsoft.com/library/azure/dn535601.aspx)

  Hello Azure 저장소 서비스에 대 한 CORS 지원에 대 한 hello 참조 설명서입니다. 이 링크 tooarticles tooeach 저장소 서비스를 적용 하 고 예를 보여 줍니다 개이고 hello CORS 파일의 각 요소에 설명 합니다.
* [Microsoft Azure 저장소: CORS 소개(영문)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/02/03/windows-azure-storage-introducing-cors.aspx)

  이것은 링크 toohello 초기 블로그 문서 CORS 발표 하 고 보여 주는 방법을 toouse 것입니다.

## <a name="frequently-asked-questions-about-azure-storage-security"></a>Azure 저장소 보안에 대한 FAQ(질문과 대답)
1. **Hello HTTPS 프로토콜을 사용할 수 없는 경우 또는 Azure 저장소 외부로 전송 중인 I hello blob의 hello 무결성은 어떻게 확인할 수 있습니까?**

   어떤 이유로 toouse HTTPS 대신 HTTP 블록 blob을 사용 하 여 작업할 필요를 사용할 수 있는지 확인 하는 MD5 toohelp hello blob를 전송 중인 hello 무결성을 확인 합니다. 이렇게 하면 네트워크/전송 계층 오류로부터 보호되지만 항상 중간 공격을 막을 수 있는 것은 아닙니다.

   전송 수준 보안을 제공하는 HTTPS를 사용할 수 있는 경우 MD5 확인을 사용하는 것은 중복된 작업으로 불필요합니다.

   자세한 내용은 확인 하세요 hello [Azure Blob MD5 개요](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/02/18/windows-azure-blob-md5-overview.aspx)합니다.
2. **Hello 미국에 대 한 FIPS 준수에 대 한 작업 준수**

   미국에서 사용 하도록 승인 하는 암호화 알고리즘을 정의 하는 hello 미국 연방 FIPS Information Processing Standard) 중요 한 데이터의 hello 보호용 연방 정부 컴퓨터 시스템입니다. FIPS를 사용 하면 Windows 서버 또는 데스크톱 모드 지시 hello OS FIPS 검증 한 암호화 알고리즘을 사용 해야 함을 합니다. 호환 되지 않는 알고리즘을 사용 하는 응용 프로그램 hello 응용 프로그램이 중단 됩니다. .NET으로 빌드된 Framework 버전 4.5.2 이상을 hello 응용 프로그램 자동으로 전환 hello 암호화 알고리즘 toouse FIPS 호환 알고리즘 hello 컴퓨터 FIPS 모드일 때 또는 합니다.

   Microsoft은 그대로 남아 tooeach 고객 toodecide를 여부 tooenable FIPS 모드입니다. 기본적으로 제목 toogovernment 규정 tooenable FIPS 모드 없는 고객에 대 한 강력한 이유가 없습니다 것으로 생각 합니다.

   **리소스**

* [“FIPS 모드”를 더 이상 권장하지 않는 이유](http://blogs.technet.com/b/secguide/archive/2014/04/07/why-we-re-not-recommending-fips-mode-anymore.aspx)

  이 블로그 문서에서는 FIPS의 개요를 제공하고 기본적으로 FIPS 모드를 사용하지 않는 이유를 설명합니다.
* [FIPS 140 유효성 검사(영문)](https://technet.microsoft.com/library/cc750357.aspx)

  이 문서에 어떻게 Microsoft 제품 및 암호화 모듈 표준에 따라 hello FIPS hello 미국에 대 한 정보를 제공 제공합니다.
* [Windows XP 이상 버전의 Windows에서 “시스템 암호화: 암호화, 해시, 서명에 FIPS 준수 알고리즘 사용” 보안 설정 효과](https://support.microsoft.com/kb/811833)

  이 문서 hello 사용 하 여 이전 Windows 컴퓨터의 FIPS 모드에 대해 소개 합니다.

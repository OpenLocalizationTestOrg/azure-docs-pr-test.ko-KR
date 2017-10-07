---
title: "aaaConfigure Git-Azure를 사용 하 여 API 관리 서비스 | Microsoft Docs"
description: "자세한 내용은 방법 toosave 및 Git를 사용 하 여 API 관리 서비스 구성에 구성 합니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a>어떻게 toosave 및 Git를 사용 하 여 API 관리 서비스 구성 구성
> 
> 

각 API 관리 서비스 인스턴스 hello 구성과 hello 서비스 인스턴스에 대 한 메타 데이터에 대 한 정보를 포함 하는 구성 데이터베이스를 유지 합니다. 변경 내용은 hello 게시자 포털의 설정 변경, PowerShell cmdlet을 사용 하 여 또는 REST API를 호출 하 여 toohello 서비스 인스턴스에 만들 수 있습니다. 또한 toothese 메서드를 관리할 수도 있습니다 Git를 사용 하 여, 서비스 관리 시나리오를 같은 활성화 서비스 인스턴스 구성:

* 구성 버전 관리 - 서비스 구성의 서로 다른 버전 다운로드 및 저장
* 대량으로 구성 변경-서비스 구성의 toomultiple 부분에서에서 변경한 로컬 리포지토리를 hello 변경 내용을 다시 toohello 서버를 한 번의 작업와 통합
* Hello Git 도구 및 워크플로 이미 잘 알고 있다면 친숙 한 Git 도구 체인 및 워크플로-사용

다음 다이어그램 hello 해당 API 관리 서비스 인스턴스에 hello 다양 한 방법 tooconfigure의 개요를 표시 합니다.

![Git 구성][api-management-git-configure]

Hello를 사용 하 여 서비스 구성 데이터베이스를 관리 하는 hello 게시자 포털, PowerShell cmdlet 또는 REST API hello를 사용 하 여 tooyour 서비스를 변경할 때 `https://{name}.management.azure-api.net` hello hello 다이어그램의 오른쪽에 표시 된 것 처럼 끝점입니다. hello 다이어그램의 왼쪽 hello Git를 사용 하 여 서비스 구성 관리 하는 방법을 설명 하 고에 있는 서비스에 대 한 Git 리포지토리 `https://{name}.scm.azure-api.net`합니다.

단계를 수행 하는 hello Git을 사용 하 여 API 관리 서비스 인스턴스 관리의 개요를 제공 합니다.

1. 서비스의 Git 구성에 액세스
2. 서비스 구성 데이터베이스 tooyour Git 리포지토리를 저장 합니다.
3. Hello tooyour 로컬 컴퓨터 Git 리포지토리 복제
4. 끌어오기 tooyour 로컬 컴퓨터를 최신 리포지토리 hello 및 커밋하고 푸시할 변경 내용 다시 tooyour 리포지토리
5. 사용자의 리포지토리의 hello 변경 내용을 서비스 구성 데이터베이스에 배포

이 문서에서는 설명 방법을 tooenable 및 Git toomanage 서비스 구성을 사용 하 여 hello 파일 및 폴더 hello Git 리포지토리에 대 한 참조를 제공 합니다.

## <a name="access-git-configuration-in-your-service"></a>서비스의 Git 구성에 액세스
Hello 게시자 포털의 오른쪽 위 모서리 hello에에서 hello Git 아이콘을 확인 하 여 Git 구성 hello 상태를 신속 하 게 볼 수 있습니다. 이 예제에서는 hello 상태 메시지 toohello 리포지토리에 저장 되지 않은 변경 되는 것입니다. Hello API 관리 서비스 구성 데이터베이스 저장 되지 않은 아직 toohello 리포지토리 때문입니다.

![Git 상태][api-management-git-icon-enable]

tooview 및 Git 구성 설정을 구성, hello Git 아이콘을 클릭 하거나 클릭 hello **보안** 메뉴 toohello 이동 **구성 리포지토리의** 탭 합니다.

![GIT 사용][api-management-enable-git]

> [!IMPORTANT]
> 정의 되지 않은 속성 hello 저장소에 저장 되 고에 남습니다. 그 역사 할 때까지 모든 암호 비활성화 및 다시 Git 액세스를 사용 하도록 설정 합니다. 속성 안전한 곳 toomanage toostore 없는 모든 API 구성 및 정책에서 비밀 정보를 포함 한 상수 문자열 값이 제공 정책 문을에서 직접 해당 합니다. 자세한 내용은 참조 [어떻게 Azure API 관리 정책에 toouse 속성](api-management-howto-properties.md)합니다.
> 
> 

활성화 또는 비활성화 hello REST API를 사용 하 여 Git 액세스에 대 한 자세한 내용은 참조 [Git 액세스 hello REST API를 사용 하 여 설정 하거나 해제](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit)합니다.

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a>toosave hello 서비스 구성 toohello Git 리포지토리
hello 리포지토리 복제 하기 전에 hello 첫 번째 단계는 toosave hello hello 서비스 구성 toohello 저장소의 현재 상태입니다. 클릭 **구성 toorepository 저장**합니다.

![구성 저장][api-management-save-configuration]

Hello 확인 화면에 원하는 대로 변경 하 고 클릭 **확인** toosave 합니다.

![구성 저장][api-management-save-configuration-confirm]

몇 분 후 hello 구성이 저장 되 고 마지막 구성 변경 hello 및 hello 서비스 구성 및 hello 간의 hello 마지막 동기화의 hello 날짜 및 시간을 포함 하 여 hello 리포지토리 hello 구성 상태가 표시 됩니다. 정보 저장소입니다.

![구성 상태][api-management-configuration-status]

Hello 구성은 toohello 리포지토리에 저장 복제할 수 있습니다.

Hello REST API를 사용 하 여이 작업 수행에 대 한 자세한 내용은 참조 하십시오. [hello REST API를 사용 하 여 스냅숏 커밋 구성](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot)합니다.

## <a name="tooclone-hello-repository-tooyour-local-machine"></a>tooclone hello 리포지토리 tooyour 로컬 컴퓨터
저장소 tooclone hello URL tooyour 저장소, 사용자 이름 및 암호를 해야합니다. hello 사용자 이름 및 URL 표시 hello의 hello 위쪽 **구성 리포지토리의** 탭 합니다.

![Git 복제][api-management-configuration-git-clone]

hello 암호가 hello hello 맨 아래에 생성 됩니다 **구성 리포지토리의** 탭 합니다.

![암호 생성][api-management-generate-password]

해당 hello를 먼저 확인 하는 암호를 toogenerate **만료** toohello 필요한 만료 날짜 및 시간을 설정 하 고 클릭 **토큰 생성**합니다.

![암호][api-management-password]

> [!IMPORTANT]
> 이 암호를 기록해 둡니다. 두면 되 면이 페이지 hello 암호 다시 표시 되지 않습니다.
> 
> 

사용 하 여 hello Git Bash 예제 따르는 hello 도구 [Windows 용 Git](http://www.git-scm.com/downloads) 하지만 익숙한 모든 Git 도구를 사용할 수 있습니다.

Hello 원하는 폴더의 Git 도구를 열고 다음 명령 tooclone hello git 리포지토리 tooyour 로컬 컴퓨터, hello 게시자 포털에서 제공 하는 hello 명령을 사용 하 여 hello를 실행 합니다.

```
git clone https://bugbashdev4.scm.azure-api.net/
```

Hello 사용자 이름 및 메시지가 표시 되 면 암호를 제공 합니다.

오류를 수신할 경우 수정 하세요 프로그램 `git clone` tooinclude hello 사용자 이름 및 암호를 hello 다음 예제와 같이 명령입니다.

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

오류가 발생 하면 URL 인코딩 hello 명령 hello 암호 부분을 시도 합니다. 한 신속 하 게 toodo tooopen Visual Studio 이며 hello에 문제 hello 다음 명령은 **직접 실행 창**합니다. tooopen hello **직접 실행 창**, Visual Studio에서 모든 솔루션이 나 프로젝트를 엽니다 (또는 새 비어 있는 콘솔 응용 프로그램 만들기)을 선택 하 고 **Windows**, **직접 실행** 에서 hello **디버그** 메뉴.

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

사용자 이름 및 저장소 위치 tooconstruct hello git 명령 함께 hello 인코딩된 암호를 사용 합니다.

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

Hello 리포지토리 복제 되 면 볼 수 있으며 로컬 파일 시스템에서 작업. 자세한 내용은 [로컬 Git 리포지토리의 파일 및 폴더 구조 참조](#file-and-folder-structure-reference-of-local-git-repository)를 참조하세요.

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a>tooupdate hello 가장 최근 서비스 인스턴스 구성 사용 하 여 로컬 리포지토리
Hello 게시자 포털 또는 hello REST API를 사용 하 여 변경 내용을 tooyour API 관리 서비스 인스턴스를 확인 하는 경우에 hello 최신 변경 내용으로 로컬 리포지토리를 업데이트 하기 전에 이러한 변경 내용을 toohello 저장소를 저장 해야 합니다. toodo이를 클릭 하이 여 **구성 toorepository 저장** hello에 **구성 리포지토리의** hello 게시자 포털을 탭 한 다음 다음 로컬 저장소에서 명령을 hello를 발행 합니다.

```
git pull
```

실행 하기 전에 `git pull` 로컬 저장소에 대 한 hello 폴더에 있는지 확인 하십시오. Hello를 방금 완료 한 경우 `git clone` 명령, hello 다음과 같은 명령을 실행 하 여 hello 디렉터리 tooyour 리포지토리를 변경 해야 합니다.

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a>로컬 리포지토리에 toohello 서버 리포지토리에서 toopush 변경
로컬 리포지토리 toohello 서버 리포지토리에서 toopush 변경 변경 내용을 적용 하 고 toohello 서버 리포지토리 푸시 해야 합니다. toocommit 변경 내용을 로컬 리포지토리 및 명령을 다음 문제 hello 스위치 toohello 디렉터리, 프로그램 Git 명령 도구를 엽니다.

```
git add --all
git commit -m "Description of your changes"
```

모든 hello 커밋합니다 toohello 서버에서 실행 되는 toopush 다음 명령을 hello 합니다.

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a>toodeploy 모든 서비스 구성 변경 내용 toohello API 관리 서비스 인스턴스
로컬 변경 내용이 커밋된 블록과 푸시된 toohello 서버 저장소, 되 면 tooyour API 관리 서비스 인스턴스에 배포할 수 있습니다.

![배포][api-management-configuration-deploy]

Hello REST API를 사용 하 여이 작업 수행에 대 한 자세한 내용은 참조 하십시오. [Git 배포 hello REST API를 사용 하 여 tooconfiguration 데이터베이스 변경](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration)합니다.

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a>로컬 Git 리포지토리의 파일 및 폴더 구조 참조
hello hello 로컬 git 리포지토리에서 파일 및 폴더 hello 구성 정보가 hello 서비스 인스턴스에 대 한 합니다.

| 항목 | 설명 |
| --- | --- |
| 루트 api 관리 폴더 |Hello 서비스 인스턴스에 대 한 최상위 구성을 포함 |
| apis 폴더 |Hello 서비스 인스턴스의 hello api에 대 한 hello 구성을 포함 |
| groups 폴더 |Hello 서비스 인스턴스의 hello 그룹에 대 한 hello 구성을 포함 |
| policies 폴더 |Hello 서비스 인스턴스의 hello 정책이 포함 |
| portalStyles 폴더 |Hello 서비스 인스턴스의 hello 개발자 포털 사용자 지정에 대 한 hello 구성 포함 |
| products 폴더 |Hello 서비스 인스턴스의 hello 제품에 대 한 hello 구성을 포함 |
| templates 폴더 |Hello 서비스 인스턴스의 hello 전자 메일 템플릿 hello 구성을 포함 |

각 폴더는 하나 이상의 파일 및 하나 이상의 폴더, 예를 들어 각 API, 제품 또는 그룹에 대한 폴더를 포함할 수 있습니다. 각 폴더 내의 hello 파일 hello 폴더 이름으로 설명 된 hello 엔터티 형식에 대 한 사항은 적용 됩니다.

| 파일 형식 | 목적 |
| --- | --- |
| json : |Hello 해당 엔터티에 대 한 구성 정보 |
| html |종종 hello 개발자 포털에 표시 되는 hello 엔터티에 대 한 설명 |
| xml |정책 설명 |
| css |개발자 포털 사용자 지정에 대한 스타일 시트 |

이러한 파일 만들고 사용할 수 있는, 삭제, 편집, 로컬 파일 시스템에서 관리 하 고 hello 변경 내용은 뒤로 toohello API 관리 서비스 인스턴스를 배포 합니다.

> [!NOTE]
> hello 다음 엔터티 hello Git 리포지토리에 포함 되지 않은 및 Git를 사용 하 여 구성할 수 없습니다.
> 
> * 사용자
> * 구독
> * 속성
> * 스타일 이외의 개발자 포털 엔터티
> 
> 

### <a name="root-api-management-folder"></a>루트 api 관리 폴더
hello 루트 `api-management` 폴더에는 `configuration.json` 형식에 따라 hello에 hello 서비스 인스턴스에 대 한 최상위 정보가 포함 된 파일입니다.

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

hello 처음 네 개의 설정 (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, 및 `UserRegistrationTermsConsentRequired`)에 나오는 설정에 따라 hello toohello 매핑할 **Identities** hello 탭 **보안** 섹션.

| Id 설정 | 너무 맵|
| --- | --- |
| RegistrationEnabled |**익명 사용자에 게 toosign 옵트인 페이지 리디렉션** 확인란 |
| UserRegistrationTerms |**사용자 등록 시 사용 약관** 텍스트 상자 |
| UserRegistrationTermsEnabled |**등록 페이지에 사용 약관 표시** 확인란 |
| UserRegistrationTermsConsentRequired |**동의 필요** 확인란 |

![Id 설정][api-management-identity-settings]

다음 네 개의 설정을 hello (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, 및 `DelegationValidationKey`)에 나오는 설정에 따라 hello toohello 매핑할 **위임** hello 탭 **보안** 섹션.

| 위임 설정 | 너무 맵|
| --- | --- |
| DelegationEnabled |**로그인 및 등록 위임** 확인란 |
| DelegationUrl |**위임 끝점 URL** 텍스트 상자 |
| DelegatedSubscriptionEnabled |**제품 구독 위임** 확인란 |
| DelegationValidationKey |**유효성 검사 키 위임** 텍스트 상자 |

![위임 설정][api-management-delegation-settings]

마지막 설정은 hello `$ref-policy`, hello 서비스 인스턴스에 대 한 글로벌 정책 문을 파일 toohello 매핑합니다.

### <a name="apis-folder"></a>apis 폴더
hello `apis` 폴더 hello 다음 항목을 포함 하는 hello 서비스 인스턴스의 각 API에 대 한 폴더를 포함 합니다.

* `apis\<api name>\configuration.json`-hello API에 대 한 hello 구성 이며 hello 백 엔드 서비스 URL 및 hello 작업에 대 한 정보를 포함 합니다. 이 hello toocall 인 경우 반환 되는 동일한 정보 [특정 API 가져오기](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) 와 `export=true` 에 `application/json` 형식입니다.
* `apis\<api name>\api.description.html`-hello API에 대 한 hello 설명을 이므로 toohello 해당 `description` hello 속성 [API 엔터티](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties)합니다.
* `apis\<api name>\operations\`-이 폴더에 들어 `<operation name>.description.html` toohello 작업 hello API에에서 매핑하는 파일입니다. 각 파일 hello toohello 매핑하는 API에는 단일 작업에 대 한 hello 설명을 포함 `description` hello 속성 [작업 엔터티에](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) hello REST API에에서 있습니다.

### <a name="groups-folder"></a>groups 폴더
hello `groups` 폴더 hello 서비스 인스턴스에 정의 된 각 그룹에 대 한 폴더를 포함 합니다.

* `groups\<group name>\configuration.json`-이 hello 그룹에 대 한 hello 구성 합니다. 이 hello toocall hello 인 경우 반환 되는 동일한 정보 [특정 그룹 가져오기](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) 작업 합니다.
* `groups\<group name>\description.html`-hello 그룹의 설명을 hello 이므로 해당 toohello `description` hello 속성 [엔터티 그룹](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties)합니다.

### <a name="policies-folder"></a>policies 폴더
hello `policies` 폴더에는 서비스 인스턴스에 대 한 hello 정책 문을 포함 합니다.

* `policies\global.xml` -서비스 인스턴스에 대 한 전역 범위에 정의된 정책을 포함하고 있습니다.
* `policies\apis\<api name>\` -API 범위에 정책을 정의 한 경우 해당 정책이 이 폴더에 포함되어 있습니다.
* `policies\apis\<api name>\<operation name>\`폴더에이 폴더에 포함 된 작업 범위에서 정의 된 모든 정책이 있는 경우 `<operation name>.xml` 각 작업에 대 한 정책 문을 toohello 매핑하는 파일입니다.
* `policies\products\`-포함 하는이 폴더에 포함 된 제품 범위에서 정의 된 모든 정책이 있는 경우 `<product name>.xml` 각 제품에 대 한 정책 문을 toohello 매핑하는 파일입니다.

### <a name="portalstyles-folder"></a>portalStyles 폴더
hello `portalStyles` 폴더 hello 서비스 인스턴스에 대 한 개발자 포털 사용자 지정에 대 한 구성 및 스타일 시트에 포함 되어 있습니다.

* `portalStyles\configuration.json`-hello 개발자 포털에서 사용 하는 hello 스타일 시트의 hello 이름이 포함 된
* `portalStyles\<style name>.css`-각 `<style name>.css` hello 개발자 포털에 대 한 스타일을 포함 하는 파일 (`Preview.css` 및 `Production.css` 기본적으로).

### <a name="products-folder"></a>products 폴더
hello `products` 폴더 hello 서비스 인스턴스에 정의 된 각 제품에 대 한 폴더를 포함 합니다.

* `products\<product name>\configuration.json`-이 hello 제품에 대 한 hello 구성 합니다. 이 hello toocall hello 인 경우 반환 되는 동일한 정보 [특정 제품 가져오기](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) 작업 합니다.
* `products\<product name>\product.description.html`-hello 제품의 hello 설명 이므로 toohello 해당 `description` hello 속성 [product 엔터티](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) hello REST API에에서 있습니다.

### <a name="templates"></a>템플릿
hello `templates` hello에 대 한 구성 폴더에 포함 되어 [전자 메일 템플릿을](api-management-howto-configure-notifications.md) hello 서비스 인스턴스의 합니다.

* `<template name>\configuration.json`-이 hello 전자 메일 템플릿의 hello 구성 합니다.
* `<template name>\body.html`-hello hello 전자 메일 템플릿의 본문입니다.

## <a name="next-steps"></a>다음 단계
다른 방법으로 toomanage에 대 한 내용은 해당 서비스 인스턴스를 참조 하세요.

* Hello 다음 PowerShell cmdlet을 사용 하 여 서비스 인스턴스 관리
  * [서비스 배포 PowerShell cmdlet 참조](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [서비스 관리 PowerShell cmdlet 참조](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* Hello 게시자 포털에서 서비스 인스턴스 관리
  * [첫 번째 API 관리](api-management-get-started.md)
* Hello REST API를 사용 하 여 서비스 인스턴스 관리
  * [API 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a>비디오 개요 보기
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png





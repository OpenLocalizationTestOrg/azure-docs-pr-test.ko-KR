---
title: "aaaAzure 응용 프로그램 서비스 로컬 캐시 개요 | Microsoft Docs"
description: "이 문서에서 설명 하는 방법을 tooenable, 크기 조정 및 쿼리 hello hello Azure 앱 서비스 로컬 캐시 기능 상태"
services: app-service
documentationcenter: app-service
author: SyntaxC4
manager: yochayk
editor: 
tags: optional
keywords: 
ms.assetid: e34d405e-c5d4-46ad-9b26-2a1eda86ce80
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/04/2016
ms.author: cfowler
ms.openlocfilehash: 220331ac7e15352a434d63266701071024d868c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-local-cache-overview"></a>Azure 앱 서비스 로컬 캐시 개요
Azure 웹앱의 콘텐츠는 Azure 저장소에 저장되며 영구적 방식으로 콘텐츠 공유로 표시됩니다. 이 디자인은 다양 한 응용 프로그램 의도 한 toowork 및 hello 특성 뒤에:  

* hello 콘텐츠 hello 웹 응용 프로그램의 여러 가상 컴퓨터 (VM) 인스턴스에서 공유 됩니다.
* hello 콘텐츠 영속적 이며 웹 응용 프로그램을 실행 하 여 수정할 수 있습니다.
* 진단 데이터 파일과 로그 파일 hello에서 사용할 수 있는 동일한 콘텐츠 폴더를 공유 합니다.
* 업데이트 hello 콘텐츠 폴더 직접 새 콘텐츠를 게시 합니다. 즉시 보기 hello hello SCM 웹 사이트를 통해 콘텐츠 동일 하 고 실행 중인 웹 응용 프로그램 (일반적으로 ASP.NET 같은 일부 기술은 않습니다 웹 앱으로 다시 시작 일부 파일 변경 내용 tooget hello 최신 콘텐츠) hello 할 수 있습니다.

많은 웹앱에서 이러한 기능 중 하나 또는 모두를 사용하지만 일부 웹앱에서는 고가용성으로 실행할 수 있는 읽기 전용 콘텐츠 저장소 성능만 뛰어나면 됩니다. 이러한 앱은 특정 로컬 캐시의 VM 인스턴스 이점을 활용할 수 있습니다.

hello Azure 앱 서비스 로컬 캐시 기능은 콘텐츠는 웹 역할의 보기를 제공합니다. 이 콘텐츠는 사이트 시작 시 비동기적으로 만들어지는 저장소 콘텐츠의 쓰기-삭제(write-but-discard) 캐시입니다. Hello 캐시 준비 되 면 hello 사이트는 hello 캐시 된 콘텐츠에 대 한 전환 된 toorun입니다. 로컬 캐시에서 실행 되는 웹 앱 hello 이점을 뒤에

* Azure 저장소의 콘텐츠를 액세스할 때 발생 하는 toolatencies 영향을 받지 않습니다.
* 계획 된 안전할 toohello 업그레이드 또는 계획 되지 않은 가동 중지 시간 및 hello 콘텐츠 공유를 제공 하는 서버에서 발생 하는 Azure 저장소와 기타 중단 않은 것입니다.
* 응용 프로그램 다시 시작 횟수 toostorage 공유 변경 인해 갖게 됩니다.

## <a name="how-local-cache-changes-hello-behavior-of-app-service"></a>로컬 캐시에서 응용 프로그램 서비스의 hello 동작을 변경 하는 방법
* hello 로컬 캐시는 hello 웹 응용 프로그램의 hello /site 및 /siteextensions 폴더의 복사본입니다. 웹 응용 프로그램 시작 시 hello 로컬 VM 인스턴스에서 생성 됩니다. hello 웹 앱 당 hello 로컬 캐시 크기가 제한 된 기본적으로 too300 MB too2 GB를 늘릴 수 있습니다.
* hello 로컬 캐시는 읽기 / 쓰기입니다. 그러나 hello 웹 앱을 가상 컴퓨터를 이동 하거나 다시 시작을 가져옵니다 때 들이 변경한 내용은 무시 됩니다. Hello 콘텐츠 저장소에 중요 한 데이터를 저장 하는 앱에 대 한 로컬 캐시를 사용 하지 마십시오.
* 웹 앱은 현재 에서처럼 toowrite 로그 파일과 진단 데이터를 계속 수 있습니다. 그러나 로그 파일 및 데이터를 로컬로 저장 됩니다 hello VM에서. 그런 다음 정기적으로 toohello 공유 콘텐츠 저장소에는 복사 합니다. hello 복사 toohello 공유 콘텐츠 저장소는 최상의 노력-다시 쓸 VM 인스턴스의 tooa 갑자기 크래시 인해 손실 될 수 있습니다.
* 로그 파일이 hello 및 로컬 캐시를 사용 하는 웹 응용 프로그램 데이터 폴더의 hello 폴더 구조에서 변경이 않았습니다. 이제 하위 폴더가 있습니다 hello 저장소 로그 파일 및 데이터 폴더의 "고유 식별자" + 타임 스탬프의 hello 명명 패턴을 따릅니다. Hello 하위 폴더의 각 tooa VM 인스턴스 hello 웹 응용 프로그램 실행 중이거나 실행에 해당 합니다.  
* Toohello 공유 콘텐츠 저장소 hello 게시 메커니즘 중 하나를 통해 게시 변경 내용을 toohello 웹 앱을 게시 합니다. 이것은 의도적인 hello 콘텐츠 toobe 지속적인 게시 확인 하겠습니다. hello 웹 앱의 toorefresh hello의 로컬 캐시를 toobe 다시 시작 해야 합니다. 가이 것 처럼 보일 과도 한 단계는? toomake hello 수명 주기 원활 하 게,이 문서의 뒷부분에 나오는 hello 정보를 참조 하십시오.
* D:\Home는 toohello 로컬 캐시를 가리킵니다. D:\local은 toohello 임시 VM 특정 저장소를 가리키는 계속 됩니다.
* hello hello SCM 사이트의 기본 콘텐츠 보기에는 공유 콘텐츠 저장소는 hello toobe를 계속 됩니다.

## <a name="enable-local-cache-in-app-service"></a>앱 서비스에서 로컬 캐시 사용
로컬 캐시는 예약된 앱 설정 조합을 사용하여 구성됩니다. 메서드를 다음 hello를 사용 하 여 이러한 응용 프로그램 설정을 구성할 수 있습니다.

* [Azure 포털](#Configure-Local-Cache-Portal)
* [Azure 리소스 관리자](#Configure-Local-Cache-ARM)

### <a name="configure-local-cache-by-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 로컬 캐시를 구성 합니다.
<a name="Configure-Local-Cache-Portal"></a>

앱 설정 `WEBSITE_LOCAL_CACHE_OPTION` = `Always`  

![Azure 포털 앱 설정: 로컬 캐시](media/app-service-local-cache/app-service-local-cache-configure-portal.png)

### <a name="configure-local-cache-by-using-azure-resource-manager"></a>방법: Azure Resource Manager를 사용하여 로컬 캐시 구성
<a name="Configure-Local-Cache-ARM"></a>

```

...

{
    "apiVersion": "2015-08-01",
    "type": "config",
    "name": "appsettings",
    "dependsOn": [
        "[resourceId('Microsoft.Web/sites/', variables('siteName'))]"
    ],

"properties": {
        "WEBSITE_LOCAL_CACHE_OPTION": "Always",
        "WEBSITE_LOCAL_CACHE_SIZEINMB": "300"
    }
}

...
```

## <a name="change-hello-size-setting-in-local-cache"></a>로컬 캐시에서 hello 크기 설정 변경
기본적으로 hello 로컬 캐시 크기는 **300MB**합니다. 복사 된 /siteextensions 폴더 hello 저장소 뿐만 아니라 모든 로그 및 데이터 폴더를 만든 로컬 콘텐츠 및 hello /site가 있습니다. 이 제한 tooincrease, hello 응용 프로그램 설정을 사용 하 여 `WEBSITE_LOCAL_CACHE_SIZEINMB`합니다. Hello 크기를 늘릴 수를 너무**2GB** (2000 MB) 웹 앱 당 합니다.

## <a name="best-practices-for-using-app-service-local-cache"></a>앱 서비스 로컬 캐시 사용에 대한 모범 사례
Hello와 함께에서 로컬 캐시를 사용 하는 것이 좋습니다 [스테이징 환경을](../app-service-web/web-sites-staged-publishing.md) 기능입니다.

* Hello 추가 *스티커* 앱 설정 `WEBSITE_LOCAL_CACHE_OPTION` hello 값을 가진 `Always` tooyour **프로덕션** 슬롯입니다. 사용 중인 경우 `WEBSITE_LOCAL_CACHE_SIZEINMB`, 스티커 설정 tooyour 프로덕션 슬롯으로 추가할 수도 있습니다.
* 만들기는 **준비** 슬롯 및 tooyour 스테이징 슬롯을 게시 합니다. 일반적으로 hello 준비 슬롯 toouse 로컬 캐시 tooenable hello 프로덕션 슬롯에 대 한 로컬 캐시의 hello 이점 발생 하는 경우 준비에 대 한 완벽 한 빌드-배포-테스트 수명 주기를 설정 하지 않습니다.
* 스테이징 슬롯에 대해 사이트를 테스트합니다.  
* 준비가 되면 스테이징 슬롯과 프로덕션 슬롯 간의 [교환 작업](../app-service-web/web-sites-staged-publishing.md#Swap)을 실행합니다.  
* 스티커 설정 이름이 스티커 tooa 슬롯을 포함합니다. 따라서 hello 스테이징 슬롯 가져옵니다 프로덕션 환경으로 교체 하는 경우 hello 로컬 캐시 앱 설정을 상속 합니다. hello에는 새로 슬롯 몇 분 후 hello 로컬 캐시에 대해 실행 되 고 됩니다 될 준비 슬롯 준비의 일환으로 교환 후 프로덕션을 교환 됩니다. 따라서 hello 슬롯 교환 완료 되 면 프로덕션 슬롯 hello 로컬 캐시에 대해 실행 됩니다.

## <a name="frequently-asked-questions-faq"></a>질문과 대답(FAQ)
### <a name="how-can-i-tell-if-local-cache-applies-toomy-web-app"></a>로컬 캐시 toomy 웹 응용 프로그램을 적용 하는 경우 어떻게 알 수 있습니까?
웹 앱 고성능, 신뢰할 수 있는 콘텐츠 저장소 필요 하 고 런타임 시 hello 콘텐츠 저장소 toowrite 중요 한 데이터를 사용 하지 않는의 총 크기는 2GB 미만, 다음 hello 대답이 "yes"! /site 및 /siteextensions 폴더 tooget hello의 총 크기, "Azure 웹 앱 디스크 사용" hello 사이트 확장을 사용할 수 있습니다.  

### <a name="how-can-i-tell-if-my-site-has-switched-toousing-local-cache"></a>내 사이트 toousing 로컬 캐시를 전환 하는 경우 어떻게 알 수 있습니까?
스테이징 환경을 사용 하 여 hello 로컬 캐시 기능을 사용 중인 경우 로컬 캐시는 준비 될 때까지 hello 스왑 작업이 완료 되지 않습니다. toocheck 사이트가 로컬 캐시에 대해 실행 되는 경우, hello 작업자 프로세스 환경 변수를 확인할 수 있습니다 `WEBSITE_LOCALCACHE_READY`합니다. Hello 지침을 사용 하 여 hello에 [작업자 프로세스 환경 변수](https://github.com/projectkudu/kudu/wiki/Process-Threads-list-and-minidump-gcdump-diagsession#process-environment-variable) 페이지 tooaccess hello 여러 인스턴스에서 작업자 프로세스 환경 변수입니다.  

### <a name="i-just-published-new-changes-but-my-web-app-does-not-seem-toohave-them-why"></a>방금 새 변경 내용을 게시 하지만 웹 응용 프로그램 toohave 보이지 않아 해당 합니다. 그 이유는
웹 앱에서 로컬 캐시를 사용 해야 합니다 toorestart 사이트 tooget hello 최신 변경 합니다. Toopublish 변경 tooa 프로덕션 사이트를 원하지 않습니까? Hello 슬롯 옵션 hello 이전 모범 사례 섹션에서 참조 하십시오.

### <a name="where-are-my-logs"></a>로그는 어디에 있습니까?
로컬 캐시를 사용하는 경우 로그 폴더와 데이터 폴더가 서로 약간 다르게 표시됩니다. 그러나 hello 하위 폴더가 남아의 구조 동일 hello, 제외 하 고 hello 하위 폴더는 hello와 하위 폴더에서 사이 "VM 고유 식별자" + 타임 스탬프 형식을 지정 합니다.

### <a name="i-have-local-cache-enabled-but-my-web-app-still-gets-restarted-why-is-that-i-thought-local-cache-helped-with-frequent-app-restarts"></a>로컬 캐시를 사용하도록 설정했지만 웹앱이 여전히 다시 시작됩니다. 그 이유는 무엇입니까? 로컬 캐시는 빈번한 앱 다시 시작에 도움이 된다고 생각했습니다.
로컬 캐시는 저장소 관련 웹앱 다시 시작을 방지하는 데 도움이 됩니다. 그러나 웹 앱 hello VM의 계획 된 인프라 업그레이드 하는 동안 다시 시작을 거쳐 여전히 수 없습니다. hello 로컬 캐시 사용 경험이 있는 전반적인 응용 프로그램 다시 시작 해야 적은 합니다.

### <a name="does-local-cache-exclude-any-directories-from-being-copied-toohello-faster-local-drive"></a>가 로컬 캐시 제외 되는 디렉터리 복사 더 빠르게 로컬 드라이브 toohello?
Hello 저장소 콘텐츠를 복사 하는 hello 단계의 일환으로 리포지토리 라고 하는 모든 폴더를 제외 됩니다. 이렇게 하면 시나리오 사이트 콘텐츠 일 tooday 작업 hello 웹 응용 프로그램에서에서 필요로 할 수 있는 소스 제어 리포지토리에 포함 될 수 있습니다. 

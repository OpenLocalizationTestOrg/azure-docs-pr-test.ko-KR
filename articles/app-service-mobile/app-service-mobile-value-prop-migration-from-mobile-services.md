---
title: "모바일 서비스를 사용하고 있습니다. 앱 서비스가 어떤 도움을 주나요?"
description: "앱 서비스가 기존 모바일 서비스 프로젝트에 제공하는 이점을 알아봅니다."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 26b68a11-8352-4f78-acd2-e4e0ec177781
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 22397b6b448b418d5b54a457c3bafaf5c68ecc7b
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="getting-started"> </a>모바일 서비스를 사용하고 있습니다. 앱 서비스가 어떤 도움을 주나요?
## <a name="overview"></a>개요
기존 모바일 서비스는 안전하며 계속 지원됩니다. 그러나 *Azure 앱 서비스* 플랫폼은 현재 모바일 서비스에서 사용할 수 없는 다음과 같은 많은 이점을 모바일 앱에 제공합니다.

* 웹 클라이언트와 모바일 클라이언트를 둘 다 포함하는 앱을 위한 더 간단하고 쉽고 비용 효과적인 제품
* 웹 작업, 사용자 지정 CName, 향상된 모니터링을 포함하는 새로운 호스트 기능
* 트래픽 관리자와의 완성 인도 통합
* 하이브리드 연결뿐만 아니라 VNet을 사용하여 온-프레미스 리소스 및 VPN에 연결
* NewRelic 또는 AppInsights를 사용하여 앱에 대한 모니터링, 경고 및 문제 해결
* 보다 풍부한 기본 계산 리소스 및 가격 책정
* 기본 제공되는 자동 크기 조정, 부하 분산 및 성능 모니터링
* 기본 제공되는 스테이징, 백업, 롤백 및 프로덕션에서 테스트 기능

## <a name="new-hosting-features"></a>새로운 호스팅 기능
*Azure App Service*에서 *Mobile App* 백 엔드 코드는 Web App 및 API App과 동일한 컨테이너에서 실행됩니다. 따라서 현재 모바일 서비스에 없는 다음 일부 기능을 포함하여 이 컨테이너의 모든 기능을 이용할 수 있습니다.

* 웹 작업을 통해 연속 실행되는 백 엔드 논리 추가
* 백 엔드 코드가 항상 실행되도록 유지
* 사용자 지정 CName을 사용하여 모바일 백 엔드 끝점에 친숙하고 안정적인 이름 제공
* 트래픽 관리자를 사용하여 앱 지역 크기 조정
* 원하는 모든 라이브러리 및 패키지를 포함합니다.
* (.NET에 대해) MVC를 포함한 ASP.NET의 기능 활용
* (Node.js에 대해) 일반적인 MVC 라이브러리를 포함하여 노드 에코 시스템의 순수 JavaScript 라이브러리를 활용합니다.

## <a name="access-on-premises-data-using-vnet"></a>VNet을 사용하여 온-프레미스 데이터 액세스
현재 Mobile Services를 사용하면 이미 하이브리드 연결을 사용하여 온-프레미스 리소스에 액세스할 수 있습니다. 그러나 VPN 솔루션이 선호되는 경우가 있습니다. *Azure 앱 서비스* 에서는 Azure VNet을 모바일 앱 백 엔드 코드에 사용할 수 있습니다.

## <a name="use-your-favorite-backend-language"></a>좋아하는 백 엔드 언어 사용
*Azure 앱 서비스* 는 최신 런타임에 대한 액세스를 포함하여 ASP.NET 및 Node.js 플랫폼에 대한 광범위하고 풍부한 지원을 제공합니다.

## <a name="set-up-automatic-scale"></a>자동 크기 조정 설정
모바일 서비스에서는 백 엔드 코드의 모든 인스턴스가 작은 VM에서 실행되었습니다. *Azure 앱 서비스* 를 사용하면 훨씬 다양한 옵션 집합에서 VM의 크기를 선택할 수 있습니다. 다양한 성능 메트릭에 따라 들어오는 고객 부하에 맞게 크기를 신속하게 확장하거나 축소할 수도 있습니다.

## <a name="be-in-the-know"></a>풍부한 정보 제공
모니터링 및 사용자와 팀에 자동으로 알리는 경고를 사용하여 실시간으로 문제에 대응합니다. New Relic과 AppInsights의 고급 앱 분석 및 모니터링 기능을 통합하여 모바일 앱의 성능을 보다 완전하게 파악합니다. *Azure 앱 서비스* 에서는 프로그래밍 방식으로 또는 Azure 포털을 통해 다양한 성능 메트릭에 기반하여 경고를 설정할 수 있습니다.

## <a name="keep-your-assets-safe"></a>자산을 안전하게 유지
백 엔드 및 데이터베이스를 자동으로 백업합니다. 코드와 데이터가 재해로부터 보호되고 쉽게 복원되므로 안심하고 비즈니스를 운영할 수 있습니다.

## <a name="ready-stage-go"></a>준비, 스테이징, 실행
*Azure 앱 서비스* 에서는 모바일 앱에 대한 비공개 테스트 및 스테이징 환경을 여러 개 만들 수 있습니다. 배포 전에 이러한 환경을 사용하여 테스트를 수행합니다. 가동 중지 시간 없이 프로덕션으로 교환합니다. 웹앱이 미리 로드되어 최상의 고객 경험을 보장합니다.

이 *자습서* 에 따라 기존 모바일 서비스에 [앱 서비스](app-service-mobile-migrating-from-mobile-services.md)를 이용하기 시작할 수 있습니다.

---
title: "Azure Active Directory의 Cloud App Discovery 개선 사항 | Microsoft Docs"
description: "Cloud App Discovery를 사용한 응용 프로그램 찾기 및 관리, 이점 및 작동 방식에 대한 정보를 제공합니다."
services: active-directory
keywords: "Cloud App Discovery, 응용 프로그램 관리"
documentationcenter: 
author: curtand
manager: femila
tags: ignite
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2017
ms.author: curtand
ms.reviewer: nigu
ms.openlocfilehash: 59af2a5de5936d15456058aaeacfc334b9b34d4c
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="cloud-app-discovery-enhancements-in-azure-active-directory"></a>Azure Active Directory의 Cloud App Discovery 개선 사항 
80% 이상의 직원이 승인되지 않은 SaaS 앱을 업무 목적으로 사용한다고 인정합니다. 이제 Azure AD의 Cloud App Discovery와 Microsoft Cloud App Security 데이터 및 분석 기능을 통합하여 비관리 클라우드 앱을 더 쉽게 식별할 수 있습니다. 이 새로운 통합에는 이전에 필요한 것과 다른 설정 단계가 필요합니다.

## <a name="what-can-i-do-now-with-the-improvements-to-cloud-app-discovery-in-azure-ad"></a>이제 Azure AD의 Cloud App Discovery 개선 사항으로 무엇을 할 수 있나요?

* **클라우드 앱 사용에 대한 심층 가시성** 이제 Azure AD의 Cloud App Discovery가 모든 조직 네트워크 트래픽 및 모든 장치에서 **15,000개 이상의 앱**을 검색합니다. 
* **에이전트 필요 없음** 이 새로운 버전의 Cloud App Discovery에서는 사용자 장치에 에이전트를 설치할 필요가 없습니다. 대신, 방화벽 및 프록시에서 가져온 로그 파일에 따라 검색이 수행됩니다. 장치 또는 운영 체제에 관계없이 모든 조직 네트워크 트래픽에서 앱을 검색할 수 있습니다.
* **지속적인 분석 및 알림** 이제 Azure AD의 Cloud App Discovery에서 자세한 지속적인 위험 분석과 사용 중인 새 앱이 있을 때 알림을 제공합니다. 이제 인바운드 트래픽, 아웃바운드 트래픽, 검색된 앱의 최상위 사용자와 관련된 정보 등 조직의 클라우드 앱 사용을 자세히 파악할 수 있습니다.

Active Directory Premium이 없는 경우 자세한 내용은 [Azure Active Directory 가격 책정](https://azure.microsoft.com/pricing/details/active-directory/)을 참조하세요.

이 링크를 사용하여 [Azure AD의 새로운 Cloud App Discovery 환경](https://portal.cloudappsecurity.com)을 탐색합니다.

## <a name="next-steps"></a>다음 단계
다음 링크를 사용하여 Azure AD에서 Cloud App Discovery를 설정합니다.

* [Cloud App Discovery 사용 시작](cloudappdiscovery-get-started.md)
* [스냅숏 보고서 만들기](cloudappdiscovery-set-up-snapshots.md)
* [연속 보고 구성](https://docs.microsoft.com/cloud-app-security/discovery-docker)
* [사용자 지정 로그 구문 분석기 사용](https://docs.microsoft.comcommit/cloud-app-security/custom-log-parser)
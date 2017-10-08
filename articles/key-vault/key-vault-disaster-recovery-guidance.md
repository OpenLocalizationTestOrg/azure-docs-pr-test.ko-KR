---
title: "Azure 키 자격 증명 모음에 영향을 주는 Azure 서비스 중단의 hello 이벤트에서 aaaWhat toodo | Microsoft Docs"
description: "어떤 toodo hello Azure 키 자격 증명 모음에 영향을 주는 Azure 서비스 중단 이벤트에 알아봅니다."
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a>Azure 주요 자격 증명 모음 가용성 및 중복성
Azure 주요 자격 증명의 여러 계층의 중복 toomake 키와 암호 남아 있는지 사용할 수 있는 tooyour 응용 프로그램 hello의 개별 구성 요소 실패를 서비스 하는 경우에 있는지 기능 합니다.

hello 내용의 주요 자격 증명 모음 내에서 복제 됩니다 hello 지역과 보조 지역 tooa 150 마일 이상 떨어져 있지만 hello 내 동일한 지리적 위치입니다. 따라서 키와 암호의 내구성이 매우 높습니다. Hello 참조 [Azure 지역 쌍이](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) 특정 지역 쌍에 대 한 자세한 내용은 문서.

Hello 주요 자격 증명 모음 서비스 내에서 개별 구성 요소 실패 hello 지역 내의 다른 구성 요소 단계 tooserve 기능 저하 없이 인지 사용자 요청 toomake입니다. 모든 작업 tootrigger tootake를 불필요이 있습니다. 자동으로 발생 하 고 투명 하 게 tooyou 됩니다.

해당 지역에서 Azure 키 자격 증명 모음 구성 하는 hello 요청은 자동으로 hello 드문 경우에는 전체 Azure 지역을 사용할 수 없다는 라우팅됩니다 (*장애 조치*) tooa 보조 지역입니다. 요청은 다시 라우팅됩니다 hello 기본 지역을 사용할 수 있는 다시 (*다시 실패*) toohello 기본 지역입니다. 다시 않아도 tootake 조치가 자동으로 수행 하기 때문에 합니다.

몇 가지 주의 사항이 toobe 인식

* 지역 장애 조치의 hello 이벤트를 hello 서비스 toofail 몇 분 정도 걸릴 수 있습니다. 이 시간 동안 만들어진 요청 hello 장애 조치가 완료 될 때까지 실패할 수 있습니다.
* 장애 조치가 완료되면 주요 자격 증명 모음은 읽기 전용 모드입니다. 이 모드에서 지원되는 요청은 다음과 같습니다.
  * 주요 자격 증명 모음 나열
  * 주요 자격 증명 모음 속성 가져오기
  * 암호 나열
  * 암호 가져오기
  * 키 나열
  * 키(키의 속성) 가져오기
  * 암호화
  * 암호 해독
  * 래핑
  * 래핑 취소
  * Verify
  * 로그인
  * 백업
* 장애 조치가 장애 복구되면 모든 요청 유형( 읽기 *및* 쓰기 요청 포함)을 사용할 수 있습니다.


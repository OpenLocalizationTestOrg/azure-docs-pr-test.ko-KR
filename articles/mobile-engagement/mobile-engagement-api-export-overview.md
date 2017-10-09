---
title: "aaaMobile Engagement 내보내기 API 개요"
description: "원시 데이터 내보내기에 대 한 기본 사항 hello 생성 한 사용자의 장치 tooleverage에서 고유한 도구에 알아봅니다."
services: mobile-engagement
documentationcenter: mobile
author: kpiteira
manager: erikre
editor: 
ms.assetid: 9380d47b-d7fa-4d4c-888f-97e6482196bb
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 04/26/2016
ms.author: kapiteir
ms.openlocfilehash: f55be29a29878e74f6a33419f08a5574a07a7478
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="mobile-engagement-export-api-overview"></a>Mobile Engagement 내보내기 API 개요
## <a name="introduction"></a>소개
이 문서에서는 원시 데이터 내보내기에 대 한 hello 기본 사항에서에서 생성 된 사용자의 장치 tooleverage 것 고유한 도구 살펴봅니다.

## <a name="pre-requisites"></a>필수 조건
Mobile Engagement에서 hello 원시 데이터 내보내기에 필요 합니다.

* API 인증 설치 toobe 수 toouse hello Api (참조 [인증 수동 설치](mobile-engagement-api-authentication-manual.md)),
* Hello 또는 hello REST Api를 사용 하 여 [.net SDK](mobile-engagement-dotnet-sdk-service-api.md),
* Azure Storage 계정.

> [!NOTE]
> 또한 hello 뛰어난 것이 좋습니다 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/), 적어도 그대로 hello 개발 단계 동안 Azure 저장소와 상호 작용 하기 위한 UI는 쉽게 toouse 제공 합니다.
> 
> 

## <a name="what-can-be-exported"></a>무엇을 내보낼 수 있습니까?
Mobile Engagement 사용 하면 해당 사용자가 toocollect 많은 종류의 데이터 및 따라서 여러 유형의 내보내기 적합 toothese 다른 데이터 형식입니다.
두 가지 필수 내보내기 유형이 있습니다.

* 스냅숏: tooexport 데이터는 상태를 나타내는 및는 Mobile Engagement가 없는 기록을 일반적으로 사용 합니다. 예를 들어 토큰(앱 정보), 토큰 또는 푸시 캠페인 피드백을 포함합니다. 따라서 이러한 유형의 내보내기 없는 관련 tooa 날짜입니다.
* 기록: 이러한 내보내기 유형은 예를 들어 이벤트 또는 작업과 같은 시간에 따라 누적되는 데이터에 사용됩니다.

hello 표에서 거쳤으며 hello 가능한 내보내기를 모두 설명합니다.

| 내보내기 형식 | 데이터 형식 | 설명 |
| --- | --- | --- |
| 스냅숏 |푸시(Push) |장치 ID/사용자 ID 단위별 푸시 캠페인 피드백의 내보내기 생성 |
| 스냅숏 |태그 |Hello에 연결 하는 태그 (응용 프로그램 정보) tooeach 장치의 내보내기를 생성합니다. |
| 스냅숏 |장치 |대부분의 hello technicals (모델, 로캘, 표준 시간대,...), hello 태그, 처음 볼된 때와 같은 장치에 대 한 hello 데이터의 내보내기를 생성 하는 중... |
| 스냅숏 |위임 |모든 hello 유효한 토큰의 내보내기의 생성합니다. |
| 기록 |작업 |지정된 된 기간 동안에 각 장치에 대 한 모든 hello 활동의 내보내기를 생성합니다. |
| 기록 |이벤트 |지정된 된 기간 동안에 각 장치에 대 한 모든 hello 활동의 내보내기를 생성합니다. |
| 기록 |작업 |지정된 된 기간 동안에 각 장치에 대 한 모든 hello 작업의 내보내기를 생성합니다. |
| 기록 |오류 |지정된 된 기간 동안에 내보내기의 각 장치에 대 한 모든 hello 오류를 생성합니다. |

## <a name="how-does-it-work"></a>작동 원리
내보내기는 대용량 데이터 파일을 생성할 수 있는 장기 실행 작업입니다. 이러한 이유로, 호출 된 tooreturn 파일 toodownload 즉시 일 수 없습니다.
Mobile Engagement에서 주문 tooexport 데이터를 toocreate 해야 합니다는 **내보내기 작업** 일반적으로 지정할 수 있는 API를 통해:

* 내보내기 (스냅숏 또는 기록)의 hello 형식
* hello 데이터 형식
* hello **Azure Storage 컨테이너** (쓰기 액세스 권한이 있는 유효한 SAS 포함) hello 내보내기의 hello 결과 기록 될 위치입니다.
* 예를 들어 예제 컨테이너 URL 매개 변수는 https://[StorageAccountName].blob.core.windows.net/[ContainerName]?[SASWritePermissionsToken]이 됩니다.  

다음은 실제 사례입니다. https://testazmeexport.blob.core.windows.net/test1234azme?sv=2015-12-11&ss=b&srt=sco&sp=rwdlac&se=2016-12-17T04:59:26Z&st=2016-12-16T20:59:26Z&spr=https&sig=KRF3aVWjp2NEJDzjlmoplmu0M9HHlLdkBWRPAFmw90Q%3D

시작 하 여 작업 toobe 몇 분 정도 걸릴 수 있습니다 및 많은 사용자 또는 활동을 사용 하 여 앱에 대 한 작은 앱 tooseveral 시간에 대 한 몇 초에서 실행할 수 있습니다 다음 note 하십시오.

가능한 toocheck는 hello 작업을 만든 후 해당 상태 toosee 여전히 실행 중 또는 완료 된 경우.

Hello 작업이, 성공적으로 수행 되 면 hello 결과 데이터 파일은 저장소 컨테이너를 제공 하는 hello에서 사용할 수 있습니다.


---
title: "다양 한 상태의 나 BizTalk 서비스의 상태에 허용 되는 aaaTasks | Microsoft Docs"
description: "서로 다른 MABS 상태에 허용 되는 작업/작업과 hello: 중지, 시작, 다시 시작, 일시 중단, 다시 시작, 삭제, 크기 조정, 구성 및 백업 구성 업데이트"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: aea738f3-ec76-4099-a41b-e17fea9e252f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/08/2016
ms.author: mandia
ms.openlocfilehash: 643307ba6fa9b05c82b867912feab249c42b65dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-you-can-and-cant-do-using-hello-biztalk-service-state"></a>무엇을 사용 하 여 수행할 수 없는 hello BizTalk 서비스 상태

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Hello hello BizTalk 서비스의 현재 상태에 따라에 몇 가지 작업을 수 또는 hello BizTalk 서비스에서 수행할 수 없습니다.

예를 들어 hello Azure 클래식 포털에서에서 새 BizTalk 서비스를 제공 합니다. Hello BizTalk 서비스에는 성공적으로 완료 하면 `active` 상태입니다. Hello 활성 상태의 중지 하거나 일시 중단 및 hello BizTalk 서비스를 삭제할 수 있습니다. 경우 hello BizTalk 서비스를 중지 및 중지 오류가 발생 하면 실행 한 다음 BizTalk 서비스 hello tooa `StopFailed` 상태입니다. Hello에 `StopFailed` 상태 이면 hello BizTalk 서비스를 다시 시작할 수 있습니다. 다시 시작할 때와 같은 허용 되지 않는 작업을 시도 하면 hello 다음 오류가 발생 합니다.

`Operation not allowed`

## <a name="view-hello-possible-states"></a>Hello 가능한 상태 보기

hello 다음 테이블 목록 hello 작업 또는 hello BizTalk 서비스는 특정 상태에 있을 때 수행할 수 있는 작업입니다. ✔ hello 작업은 해당 상태에 있는 동안 허용을 의미 합니다. 빈 항목 상태에 있는 동안 hello 작업을 수행할 수 없습니다 것을 의미 합니다.

| 서비스 상태 | 시작 | 중지 | 다시 시작 | 일시 중단 | 다시 시작 | 삭제 | 확장 | 업데이트 <br/> 구성 | Backup |
| --- | --- | --- | --- | --- | --- | --- |--- | --- | --- |
| Active |  | ✔ | ✔ | ✔ |  | ✔ |✔ |✔ |✔ |
| 사용 안 함 |  |  |  |  |  | ✔ | |  |  | 
| 일시 중단 |  |  |  |  | ✔ | ✔ | |  | ✔ |
| 중지됨 | ✔ |  | ✔ |  |  | ✔ | |  | ✔ |
| 서비스 업데이트 실패 |  |  |  |  |  | ✔ | |  |  | 
| 사용 안 함 실패 |  |  |  |  |  | ✔ | |  |  | 
| 사용 실패 |  |  |  |  |  | ✔ | |  |  | 
| 시작 실패 <br/> 중지 실패 <br/> 다시 시작 실패 | ✔ | ✔ | ✔ |  |  | ✔ | | ✔ | |
| 일시 중단 실패 <br/> 계속 실패|  |  |  | ✔ | ✔ | ✔ | |  |  | 
| 생성 실패 <br/> 복원 실패 |  |  |  |  |  | ✔ | |  |  | 
| 구성 업데이트 실패  |  |  | ✔ |  |  | ✔ | |✔ | |
| 크기 조정 실패 |  |  |  |  |  | ✔ |✔ | |  |  | 



## <a name="see-also"></a>참고 항목
* [Hello Azure 클래식 포털을 사용 하 여 BizTalk 서비스 만들기](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [BizTalk 서비스의 hello 대시보드, 모니터 및 배율 탭에서 수행할 수 있는 작업](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [BizTalk 서비스의 hello Developer, Basic, Standard 및 Premium edition 결과가](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [어떻게 tooback 하거나 BizTalk 서비스를 복원 합니다.](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [BizTalk Services에 설명된 제한](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>
* [BizTalk 서비스에 대 한 hello 서비스 버스 및 액세스 제어 발급자 이름과 발급자 키 값을 검색 합니다.](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>
* [Azure BizTalk 서비스 SDK를 hello 어떻게 사용 하 여 시작 합니까](http://go.microsoft.com/fwlink/p/?LinkID=302335)


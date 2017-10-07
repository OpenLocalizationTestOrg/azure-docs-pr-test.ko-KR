---
title: "aaaAdministration 및 BizTalk 서비스의 개발 작업 목록 | Microsoft Docs"
description: "계획 및 작업은 Azure BizTalk 서비스를 배포하는 데 도움을 줍니다."
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: 0ab70b5b-1a88-4ba5-b329-ec51b785010e
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: 544c6b23fcbc2267598b713dbe1626699099d181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="administration-and-development-task-list-in-biztalk-services"></a>BizTalk 서비스의 관리 및 개발 작업 목록

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="getting-started"></a>시작하기
Microsoft Azure BizTalk 서비스를 사용할 때는 몇 가지 온-프레미스와 클라우드 기반 구성 요소 tooconsider 합니다. 시작 tooget hello 프로세스 흐름을 고려 합니다.  

| 단계 | 담당자 | 작업 | 관련 링크 |
| --- | --- | --- | --- |
| 1. |관리자 |Hello Microsoft 계정 또는 조직 계정을 사용 하 여 Microsoft Azure 구독 만들기 |[Azure 클래식 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885) |
| 2. |관리자 |BizTalk 서비스 만들기 또는 프로비전 |[Azure 클래식 포털을 사용하여 BizTalk 서비스 만들기](http://go.microsoft.com/fwlink/p/?LinkID=302280) |
| 3. |관리자 |사용자 또는 회사의 BizTalk 서비스 배포 등록 |[등록 하 고 hello BizTalk 서비스 포털에서 BizTalk 서비스 배포를 업데이트 합니다.](https://msdn.microsoft.com/library/azure/hh689837.aspx) |
| 4. |관리자 |Hello 응용 프로그램 BizTalk 어댑터 서비스 tooconnect tooan 온-프레미스의 업무 (LOB) 시스템을 사용 하거나 큐 또는 항목 대상을 사용 하는 경우 적용 됩니다.  Azure 서비스 버스 Namespace hello를 만듭니다. 이 네임 스페이스, 서비스 버스 발급자 이름 및 값 toohello 개발자 서비스 버스 발급자 키를 제공 합니다. |[방법: 서비스 버스 서비스 네임스페이스 만들기 또는 수정](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md) 및 [발급자 이름 및 발급자 키 값 가져오기](biztalk-issuer-name-issuer-key.md) |
| 5. |Developer |Hello SDK를 설치 하 고 Visual Studio에서 hello BizTalk 서비스 프로젝트를 만듭니다. |[Azure BizTalk 서비스 SDK 설치](https://msdn.microsoft.com/library/azure/hh689760.aspx) 및 [Azure에서 다양한 메시징 끝점 만들기](https://msdn.microsoft.com/library/azure/hh689766.aspx) |
| 6. |Developer |BizTalk 서비스는 Azure에서 호스트 하 여 BizTalk 서비스 프로젝트 tooyour를 배포 합니다. |[배포 및 hello BizTalk 서비스 프로젝트를 새로 고침](https://msdn.microsoft.com/library/azure/hh689881.aspx) |
| 7. |관리자 |EDI를 사용하는 경우 적용합니다.  파트너를 추가 하 고 hello Microsoft Azure BizTalk Services 포털에서 계약을 만들 수 있습니다. 규약을 만들 때 hello 브리지 및/또는 hello 개발자 toohello 규약 설정에 의해 생성 되는 변환을 추가할 수 있습니다. |[BizTalk 서비스 포털에서 EDI, AS2 및 EDIFACT 구성](https://msdn.microsoft.com/library/azure/hh689853.aspx) |
| 8. |관리자 |Hello Azure 클래식 포털을 사용 하 여, 모니터링할 성능 메트릭을 비롯 하 여 BizTalk 서비스의 hello 상태입니다. |[BizTalk 서비스: 대시보드, 모니터 및 크기 조정 탭](http://go.microsoft.com/fwlink/p/?LinkID=302281) |
| 9. |관리자 |Microsoft Azure BizTalk 서비스 포털 hello를 사용 하 여 hello 브리지 파일에 의해 처리 된 대로 BizTalk 서비스와 메시지 추적에 의해 사용 되는 hello 아티팩트 관리 합니다. |[Hello BizTalk 서비스 포털을 사용 하 여](https://msdn.microsoft.com/library/azure/dn874043.aspx) |
| 10. |관리자 |백업 계획 tooback을 hello BizTalk 서비스를 만듭니다. |[BizTalk 서비스에서 무중단 업무 방식 및 재해 복구](https://msdn.microsoft.com/library/azure/dn509557.aspx) |

## <a name="next-steps"></a>다음 단계
[자습서 및 샘플](https://msdn.microsoft.com/library/azure/hh689895.aspx)

[Visual Studio에서 hello 프로젝트 만들기](https://msdn.microsoft.com/library/azure/hh689811.aspx)

[Azure BizTalk 서비스 SDK 설치](https://msdn.microsoft.com/library/azure/hh689760.aspx)

## <a name="concepts"></a>개념
[Visual Studio에서 hello 프로젝트 만들기](https://msdn.microsoft.com/library/azure/hh689811.aspx)  
[EDI, AS2 및 EDIFACT 메시징 (비즈니스 tooBusiness)](https://msdn.microsoft.com/library/azure/hh689898.aspx)  

## <a name="other-resources"></a>기타 리소스
[원본, 대상 및 브리지 메시징 끝점 추가](https://msdn.microsoft.com/library/azure/hh689877.aspx)  
[메시지 맵 및 변환 학습 및 만들기](https://msdn.microsoft.com/library/azure/hh689905.aspx)  
[BizTalk 어댑터 서비스 (BAS) hello를 사용 하 여](https://msdn.microsoft.com/library/azure/hh689889.aspx)  
[Azure BizTalk 서비스](http://go.microsoft.com/fwlink/p/?LinkID=303664)


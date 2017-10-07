---
title: "Azure 앱 서비스에 대 한 aaaBest 사례"
description: "Azure 앱 서비스에 대한 모범 사례 및 문제 해결에 대해 알아봅니다."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: f3359464-fa44-4f4a-9ea6-7821060e8d0d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: dariagrigoriu
ms.openlocfilehash: a1d3127f5a746aa43f7b56b45f17c45df9087bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-app-service"></a>Azure 앱 서비스에 대한 모범 사례
이 문서는 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)를 사용하는 모범 사례를 요약합니다. 

## <a name="colocation"></a>공동 배치
예: 웹 응용 프로그램 및 데이터베이스 솔루션을 작성 하는 Azure 리소스 hello 효과 서로 다른 지역에에서 있는 경우 hello 다음을 포함할 수 있습니다.

* 리소스 간 통신에 대한 대기 시간 증가
* 아웃 바운드 데이터에 대 한 통화 요금 지역 간 hello에 설명한 것 처럼 전송 [Azure 가격 책정 페이지](https://azure.microsoft.com/pricing/details/data-transfers)합니다.

공동 배치 hello 동일한 지역은 웹 앱과 같은 솔루션을 작성 하는 Azure 리소스에 가장 적합 하 고 toohold 내용 또는 데이터는 데이터베이스 또는 저장소 계정을 사용 합니다. 경우에 있는지 확인 해야 리소스를 만드는 hello 특정 비즈니스 했거나 해당 하지 toobe 사유를 디자인 하지 않는 한 동일한 Azure 지역. 앱 서비스 앱 toohello 이동할 수 hello를 활용 하 여 데이터베이스와 동일한 지역 [앱 서비스 복제 기능](app-service-web-app-cloning-portal.md) 앱 프리미엄 앱 서비스 계획에 대 한 현재 사용할 수 있습니다.   

## <a name="memoryresources"></a>앱에서 예상보다 더 많은 메모리를 사용하는 경우
응용 프로그램은 모니터링을 통해 표시 된 대로 예상 보다 더 많은 메모리 또는 서비스 권장 사항을 고려 hello 알 있습니다 [응용 프로그램 서비스 자동 복구 기능](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites)합니다. 메모리 임계값에 따라 사용자 지정 작업을 이동은 hello 자동 복구 기능에 대 한 hello 옵션 중 하나입니다. Span hello 스펙트럼 hello 작업자 프로세스를 재활용 하 여 메모리 덤프 자리를 tooon 완화를 통해 전자 메일 알림 tooinvestigation에서 작업 합니다. 자동 복구 구성 될 수 있으므로 web.config를 통해 친숙 한 사용자 인터페이스를 통해 hello에 대 한이 블로그 게시물에 설명 된 대로 [앱 서비스 지원 사이트 확장](https://azure.microsoft.com/blog/additional-updates-to-support-site-extension-for-azure-app-service-web-apps)합니다.   

## <a name="CPUresources"></a>앱에서 예상보다 더 많은 CPU를 사용하는 경우
모니터링을 통해 표시 된 대로 CPU 스파이크를 반복 하는 앱에서 발생 하거나 예상 보다 더 많은 CPU 사용 확인 하거나 서비스 권장 사항을 스케일 업 또는 hello 앱 서비스 계획을 확장 합니다. 바뀌기 응용 프로그램을 사용 하는 경우 응용 프로그램 상태 비저장, 크기 조정 아웃 하면 더 많은 유연성 및 눈금 가능성이 높은 반면 hello 유일한 옵션은 수직 확장 합니다. 

"상태 저장" 및 "상태 비저장" 응용 프로그램 비교에 대한 자세한 내용은 [Microsoft Azure 웹앱에서 확장 가능한 종단 간 다중 계층 응용 프로그램 계획](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/DEV-B414#fbid=?hashlink=fbid)비디오를 시청할 수 있습니다. 앱 서비스 크기 조정 및 자동 크기 조정 옵션에 대한 자세한 내용은 [Azure 앱 서비스에서 웹앱 크기 조정](web-sites-scale.md)을 참조하세요.  

## <a name="socketresources"></a>소켓 리소스를 모두 사용한 경우
소진 아웃 바운드 TCP 연결에 대 한 일반적인 이유는 구현 된 tooreuse TCP 연결 되지 않는 클라이언트 라이브러리 또는 HTTP 연결 유지 활용 하지와 같은 높은 수준의 프로토콜의 경우 hello hello를 사용 합니다. 각 구성 되었거나 아웃 바운드 연결의 효율적인 다시 사용 하기 위해 코드에 액세스 하 여 앱 서비스 계획 tooensure에서 hello 응용 프로그램에서 참조 하는 hello 라이브러리에 대 한 hello 설명서를 검토 하십시오. 또한 올바른 생성 및 릴리스 또는 정리 tooavoid 누수 연결에 대 한 hello 라이브러리 설명서 지침에 따라 합니다. 이러한 클라이언트 라이브러리 및 조사 중인 진행 영향 toomultiple 인스턴스를 확장 하 여 완화할 수 있습니다.  

## <a name="appbackup"></a>앱 백업이 실패하는 경우
응용 프로그램 백업 실패 이유는 두 가지 가장 일반적인 이유 hello: 잘못 된 저장소 설정 및 데이터베이스 구성이 잘못 되었습니다. 이러한 오류는 변경 내용 toostorage 또는 데이터베이스 리소스 또는 방법에 대 한 변경 내용을 않은 경우에 일반적으로 발생 tooaccess 이러한 리소스 (예: 자격 증명 hello 백업 설정에서 선택 하는 hello 데이터베이스에 대 한 업데이트) 합니다. 일반적으로 백업 일정에 따라 실행 하 고 액세스 toostorage (에 대 한 출력 파일을 백업 하는 hello) 및 데이터베이스 (복사 및 해야 hello 백업에 포함 된 내용을 toobe 읽는). 이러한 리소스 중 하나는 것 tooaccess 오류가 hello 일관 된 백업 실패 합니다. 

백업 실패를 발생 하는 경우에 어떤 유형의 오류가 발생 하는 가장 최근의 결과 toounderstand를 검토 하십시오. 저장소 액세스 실패의 경우 hello 검토 하 고 hello 백업 구성에 사용 된 hello 저장소 설정을 업데이트 하십시오. 데이터베이스 액세스 실패의 경우 hello 하십시오 검토 및 응용 프로그램 설정;의 일부로 연결 문자열 업데이트 설정한 다음 tooupdate 백업 구성 tooproperly hello 필요한 데이터베이스를 포함 합니다. 응용 프로그램 백업에 대 한 자세한 내용은 hello를 참조 하십시오 [Azure 앱 서비스의 웹 앱 백업](web-sites-backup.md) 설명서입니다.

## <a name="nodejs"></a>Node.js 응용 프로그램을 새 앱 서비스 배포 tooAzure를가 하는 경우
Node.js 앱에 대 한 azure 앱 서비스 기본 구성에는 가장 일반적인 응용 프로그램의 의도 한 toobest 짝패 hello 요구 사항입니다. Node.js 응용 프로그램에 대 한 구성을 튜닝 하는 개인 설정 된 tooimprove 성능을 활용 거 나 CPU/메모리/네트워크 리소스에 대 한 리소스 사용을 최적화를 하는 경우의 모범 사례 및 문제 해결 단계를 검토할 수 있습니다. 이 문서에 설명 hello iisnode 설정 해야 할 수 있습니다 tooconfigure Node.js 응용 프로그램에 대 한 설명 다양 한 시나리오 또는 앱 직면할 수 있는 문제 및 표시 방법을 hello tooaddress 이러한 문제: [모범 사례 및 Azure 앱 서비스에서 Node 응용 프로그램에 대 한 문제 해결 가이드](app-service-web-nodejs-best-practices-and-troubleshoot-guide.md)합니다.   


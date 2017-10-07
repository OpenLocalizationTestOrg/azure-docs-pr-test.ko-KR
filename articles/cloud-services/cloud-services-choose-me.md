---
title: "aaaAzure 계산 옵션-클라우드 서비스 | Microsoft Docs"
description: "Azure 계산 호스팅 옵션 및 작동 방식에 대해 알아봅니다. 앱 서비스, 클라우드 서비스 및 가상 컴퓨터"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
ms.assetid: ed7ad348-6018-41bb-a27d-523accd90305
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: e7f109a54c61cc2f37644d39a61d2d932a374587
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-choose-cloud-services-or-something-else"></a>클라우드 서비스 또는 다른 항목을 선택해야 합니까?
Azure 클라우드 서비스 hello 선택 하는 있습니까? Azure는 응용 프로그램을 실행하기 위한 여러 호스팅 모델을 제공합니다. 각 서비스의 다른 집합을 제공, 정확히 무엇 중 어느 것에 따라 달라 집니다 선택 있는 toodo 합니다.

[!INCLUDE [compute-table](../../includes/compute-options-table.md)]

<a name="tellmecs"></a>

## <a name="tell-me-about-cloud-services"></a>클라우드 서비스에 대한 설명
클라우드 서비스는 [PaaS(Platform-as-a-Service)](https://azure.microsoft.com/overview/what-is-paas/) 의 예입니다. 마찬가지로 [앱 서비스](../app-service-web/app-service-web-overview.md),이 기술은 toosupport 설계 된 응용 프로그램을 확장 가능 하 고 안정적 이며 및 저렴 toooperate입니다. 하지만 응용 프로그램 서비스에서 Vm을 하므로 호스팅되는 것 처럼도 클라우드 서비스는 hello Vm 보다 상세하게, 해야 합니다. 클라우드 서비스 VM에 원하는 소프트웨어를 설치하여 원격으로 실행할 수 있습니다.

![cs_diagram](./media/cloud-services-choose-me/diagram.png)

더욱 긴밀하게 제어할수록 사용 편의성은 낮아집니다. Hello 추가 제어 옵션 필요 하지 않으면는 사용자가 일반적으로 더 쉽고 빠르게 tooget 웹 응용 프로그램 및 tooCloud 서비스에 비해 앱 서비스에서 웹 앱에서 실행 합니다.

Cloud Service 역할의 두 가지 형식이 있습니다. hello만 차이점 두 hello은 hello 가상 컴퓨터 역할 호스팅 방법입니다.

* **웹 역할**  
IIS를 통해 앱을 자동으로 배포하고 호스팅합니다.

* **작업자 역할**  
IIS를 사용하지 않고 앱을 독립 실행형으로 실행합니다.

예를 들어, 간단한 응용 프로그램은 단일 웹 역할만 사용하여 웹 사이트를 제공할 수 있습니다. 더 복잡 한 응용 프로그램 웹 역할 toohandle를 사용할 수 있습니다 다음 사용자 로부터 들어오는 요청 처리를 위해 tooa 작업자 역할에서 해당 요청을 전달 합니다. (이 통신에는 [서비스 버스](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)나 [Azure 큐](../storage/common/storage-introduction.md)를 사용할 수 있습니다.)

Hello 앞의 그림 알 수 있듯이 모든 hello Vm hello에서 실행 하는 단일 응용 프로그램에서 동일한 클라우드 서비스입니다. 사용자가 액세스 hello 응용 프로그램이 단일 공용 IP 주소를 통해, 요청과 함께 자동으로 부하 분산 된 hello 응용 프로그램의 Vm 전체의 합니다. hello 플랫폼 [고 확장할 수 있으며 배포](cloud-services-how-to-scale.md) 하드웨어 오류의 단일 지점이 방지 하는 방법에서 클라우드 서비스 응용 프로그램에서 Vm을 hello 합니다.

응용 프로그램을 가상 컴퓨터에서 실행 하는 경우에 것이 중요 한 toounderstand 클라우드 서비스 PaaS 하지 IaaS를 제공 합니다. 항목에 대 한 한 가지 방법은 toothink 다음과 같습니다: Azure 가상 컴퓨터와 같은 IaaS를 먼저 만든 및 응용 프로그램을 실행 하는 hello 환경을 구성 다음이 환경에 응용 프로그램을 배포 합니다. 대부분이 세계의 관리를 담당 패치가 적용 된 새 버전의 각 VM에 hello 운영 체제를 배포 하는 등 작업을 수행 하는 합니다. PaaS 반면 것이 hello 환경이 이미 있는 것 처럼 합니다. Toodo를 하면 응용 프로그램을 배포 합니다. 새 버전의 hello 운영 체제를 배포 하는 등을 실행 하는 hello 플랫폼의 관리를 자동으로 처리 됩니다.

## <a name="scaling-and-management"></a>확장 및 관리
클라우드 서비스로 가상 컴퓨터를 만들지 않습니다. 각각의 개수를 보려면와 같은 Azure에 알려 주는 구성 파일을 제공 하는 대신, **3 웹 역할 인스턴스에** 및 **두 작업자 역할 인스턴스**, 고 hello 플랫폼을 만듭니다.  사용자는 이들 지원 VM의 [실제 크기](cloud-services-sizes-specs.md) 를 선택하지만 명시적으로 직접 만들는지는 않습니다. 응용 프로그램에 더 큰 부하 toohandle 필요한 경우 더 많은 Vm에 대 한 요청 하 고 Azure 이러한 인스턴스를 만듭니다. Hello 부하가 감소 하는 경우 해당 인스턴스를 종료 하 고 해당 작업에 대 한 부담을 중지할 수 있습니다.

일반적으로 클라우드 서비스 응용 프로그램을 2 단계 프로세스를 통해 사용할 수 있는 toousers를 수 있습니다. 개발자 첫 번째 [업로드 응용 프로그램 hello](cloud-services-how-to-create-deploy.md) toohello 플랫폼의 준비 영역입니다. Hello 개발자가 준비 되 면 toomake hello 응용 프로그램에 라이브, 프로덕션으로 hello Azure 포털 tooswap 준비를 사용 합니다. 이 [스테이징 및 프로덕션 사이 전환](cloud-services-nodejs-stage-application.md) 중단 시간 없이를 실행 중인 응용 프로그램에서 사용자에 게 영향을 주지 않고 새 버전을 업그레이드 된 tooa 될 수 있는 수행할 수 있습니다.

## <a name="monitoring"></a>모니터링
클라우드 서비스는 모니터링도 제공합니다. Azure 가상 컴퓨터와 같은 오류가 발생 한 물리적 서버를 검색 하 고 새 컴퓨터에 해당 서버에서 실행 중이 던 hello Vm을 다시 시작 합니다. 하지만 클라우드 서비스는 하드웨어 오류뿐만 아니라 오류가 발생한 VM과 응용 프로그램도 검색합니다. 각 웹 및 작업자 역할 내 에이전트는 달리 가상 컴퓨터, 따라서 수 toostart 새 Vm 및 오류가 발생할 때 응용 프로그램 인스턴스.

hello 클라우드 서비스 PaaS 특성에는 다른 내용이 있습니다. 가장 중요 한 hello 중 하나는이 기술을 기반으로 하는 응용 프로그램 쓸지 toorun 올바르게 모든 웹 또는 작업자 역할 인스턴스가 실패 하는 경우입니다. 이 응용 프로그램이 유지 관리 하지 않아야 하는 클라우드 서비스에 상태 tooachieve hello 자체 Vm의 파일 시스템입니다. TooCloud 서비스 Vm에 대해 쓰기가 실행 된 Vm의 Azure 가상 컴퓨터를 만든 경우와 달리 영구; 되지 가상 컴퓨터 데이터 디스크 것도 있습니다. 대신, 응용 프로그램은 명시적으로 클라우드 서비스 모든 상태 tooSQL 데이터베이스 쓰기 blob, 테이블 또는 기타 외부 저장소. 클라우드 서비스의 중요 한 목표를 모두 쉽게 tooscale 및 더욱 안전 toofailure 하면 이러한 방식으로 응용 프로그램을 구축 있습니다.

## <a name="next-steps"></a>다음 단계
[.NET으로 클라우드 서비스 앱 만들기](cloud-services-dotnet-get-started.md)  
[Node.js로 클라우드 서비스 앱 만들기](cloud-services-nodejs-develop-deploy-app.md)  
[PHP로 클라우드 서비스 앱 만들기](../cloud-services-php-create-web-role.md)  
[Python에서 클라우드 서비스 앱 만들기](cloud-services-python-ptvs.md)


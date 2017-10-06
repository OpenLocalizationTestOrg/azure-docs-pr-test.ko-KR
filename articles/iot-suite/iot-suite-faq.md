---
title: aaaAzure IoT Suite FAQ | Microsoft Docs
description: "IoT Suite에 대한 질문과 대답"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a>IoT Suite에 대한 질문과 대답

참고 항목, 연결 된 팩터리 특정 hello [FAQ](iot-suite-faq-cf.md)합니다.

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a>미리 구성 하는 hello 솔루션에 대 한 hello 소스 코드는 어디서 찾을 수 있습니까?

hello 소스 코드는 다음 GitHub 리포지토리에 hello에 저장 됩니다.
* [미리 구성된 원격 모니터링 솔루션][lnk-remote-monitoring-github]
* [예측 유지 관리 미리 구성된 솔루션][lnk-predictive-maintenance-github]
* [연결된 팩터리 미리 구성된 솔루션](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a>Toohello 최신 버전의 hello 원격 모니터링 미리 구성 된 솔루션 사용 하 여 hello IoT Hub 장치 관리 기능을 업데이트 하려면 어떻게 해야 합니까?

* Hello https://www.azureiotsuite.com/ 사이트에서 미리 구성 된 솔루션을 배포 하는 경우 항상 hello hello 솔루션의 최신 버전의 새 인스턴스를 배포 합니다.
* Hello 명령줄을 사용 하는 미리 구성 된 솔루션을 배포 하는 경우에 새로운 코드와 함께 기존 배포를 업데이트할 수 있습니다. 참조 [배포 클라우드] [ lnk-cloud-deployment] hello GitHub에서에서 [리포지토리][lnk-remote-monitoring-github]합니다.

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a>새 장치 메서드 toohello 원격 모니터링 미리 구성 된 솔루션에 대 한 지원을 추가 하려면 어떻게 해야 합니까?

Hello 섹션을 참조 [새 메서드 toohello 시뮬레이터에 대 한 지원을 추가] [ lnk-add-method] hello에 [미리 구성 된 솔루션을 사용자 지정] [ lnk-customize] 문서.

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a>hello 시뮬레이션 된 장치를 무시 하 고 원하는 속성 변경 내용 이유?
Hello에는 솔루션 미리 구성 원격 모니터링, 시뮬레이션 된 hello 장치 코드만 사용 하 여 hello **Desired.Config.TemperatureMeanValue** 및 **Desired.Config.TelemetryInterval** 원하는 속성 tooupdate hello 속성을 보고 합니다. 다른 모든 desired 속성 변경 요청은 무시됩니다.

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a>내 장치가 hello hello 솔루션 대시보드 장치 목록에 나타나지 않으면 이유?

hello hello 솔루션 대시보드 장치 목록에는 장치는 쿼리 tooreturn hello 목록을 사용합니다. 현재 쿼리는 10K 이상의 장치를 반환할 수 없습니다. 쿼리에 대 한 검색 조건을 hello 더 제한적인 수행 하십시오.

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a>Hello azureiotsuite.com에 미리 구성 된 솔루션에서 Azure 포털을 삭제 하는 hello에서 리소스 그룹을 삭제할 차이?

* Hello 미리 구성 된 솔루션을 삭제 하면 [azureiotsuite.com][lnk-azureiotsuite], hello 미리 구성 된 솔루션을 만든 경우 프로 비전 된 모든 hello 리소스를 삭제 합니다. 추가 리소스 toohello 리소스 그룹을 추가한 경우 이러한 리소스도 삭제 됩니다. 
* Hello에 hello 리소스 그룹을 삭제 하는 경우 [Azure 포털][lnk-azure-portal]만 해당 리소스 그룹의 hello 리소스를 삭제 합니다. 또한 toodelete hello Azure Active Directory 응용 프로그램 hello에 미리 구성 하는 hello 솔루션과 관련 된 해야 [Azure 클래식 포털][lnk-classic-portal]합니다.

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a>하나의 구독에 프로비전할 수 있는 IoT Hub 인스턴스는 몇 개인가요?

기본적으로 [구독당 10개의 IoT Hub][link-azuresublimits]를 프로비전할 수 있습니다. 만들 수는 [Azure 지원 티켓] [ link-azuresupportticket] tooraise이 한이도입니다. 결과적으로 모든 미리 구성 된 솔루션은 새 IoT 허브를 프로 비전 이후 수 too10 프로 비전 미리 지정된 된 구독에서 솔루션을 구성 합니다. 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a>하나의 구독에 프로비전할 수 있는 Azure Cosmos DB 인스턴스는 몇 개인가요?

50개입니다. 만들 수는 [Azure 지원 티켓] [ link-azuresupportticket] tooraise 제한이 있지만 기본적으로 하나만 제공할 수 있습니다 구독 당 50 개의 Cosmos DB 인스턴스. 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a>하나의 구독에 프로비전할 수 있는 무료 Bing 지도 API는 몇 개인가요?

2개입니다. 두 개의 Enterprise용 내부 트랜잭션 Level 1 Bing Maps 계획을 Azure 구독에서 만들 수 있습니다. 원격 모니터링 솔루션 hello hello 내부 트랜잭션 수준 1 계획과 기본적으로 프로 비전 됩니다. 결과적으로, 솔루션에서 수정 없이 구독을 모니터링 하 고 원격 tootwo를 하나만 제공할 수 있습니다.

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a>정적 맵이 있는 원격 모니터링 솔루션 배포에서는 대화형 Bing 맵을 어떻게 추가하나요?

1. [Azure Portal][lnk-azure-portal]에서 엔터프라이즈용 Bing 맵 API QueryKey를 가져옵니다. 
   
   1. Toohello hello에 엔터프라이즈에 대 한 Bing Maps API 인 리소스 그룹 이동 [Azure 포털][lnk-azure-portal]합니다.
   2. **모든 설정**을 클릭한 다음 **키 관리**를 클릭합니다. 
   3. **MasterKey**와 **QueryKey** 등, 두 개의 키를 볼 수 있습니다. Hello 값을 복사 **QueryKey**합니다.
      
      > [!NOTE]
      > 엔터프라이즈용 Bing 맵 API 계정이 없는 경우 Hello에서 새로 만든 [Azure 포털] [ lnk-azure-portal] 클릭 하 여 + 새 toocreate 프롬프트 엔터프라이즈 및 수행에 대 한 Bing Maps API를 검색 합니다.
      > 
      > 
2. Hello hello에서 최신 코드를 끌어올 [Azure IoT-원격 액세스 모니터링][lnk-remote-monitoring-github]합니다.
3. 실행 중인 로컬 또는 클라우드 hello 명령줄 배포 지침 hello 저장소 hello /docs/ 폴더에 배포 합니다. 
4. 클라우드 배포를 봐 hello에 대 한 루트 폴더의 또는 로컬 실행 한 후 *. user.config 파일 배포 중에 생성 합니다. 텍스트 편집기에서 이 파일을 엽니다. 
5. 복사한 tooinclude hello 값 변경 hello 다음 줄에서는 프로그램 **QueryKey**: 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a>DreamSpark용 Microsoft Azure가 있는 경우 사전 구성된 솔루션을 만들 수 있나요?

현재는 [DreamSpark용 Microsoft Azure][lnk-dreamspark] 계정을 사용하여 사전 구성된 솔루션을 만들 수 없습니다. 하지만 몇 분 이내에 [Azure용 평가판 계정][lnk-30daytrial]을 만들면 사전 구성된 솔루션을 만들 수 있습니다.

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a>CSP(클라우드 솔루션 공급자) 구독이 있는 경우 미리 구성된 솔루션을 만들 수 있나요?

현재는 CSP(클라우드 솔루션 공급자) 구독이 있는 미리 구성된 솔루션을 만들 수 없습니다. 하지만 몇 분 이내에 [Azure용 평가판 계정][lnk-30daytrial]을 만들면 사전 구성된 솔루션을 만들 수 있습니다.

### <a name="how-do-i-delete-an-aad-tenant"></a>AAD 테넌트를 어떻게 삭제하나요?

Eric Golpe의 블로그 게시물 [Azure AD 테넌트 삭제 연습(영문)][lnk-delete-aad-tennant]을 참조하세요.

### <a name="next-steps"></a>다음 단계

탐색할 수도 있습니다 hello 중 일부 다른 기능 및 hello IoT Suite 미리 구성 된 솔루션의 기능:

* [예측 정비 사전 구성 솔루션 개요][lnk-predictive-overview]
* [연결된 팩터리 미리 구성된 솔루션 개요](iot-suite-connected-factory-overview.md)
* [Hello 접지에서 IoT 보안][lnk-security-groundup]

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance

---
title: "Microsoft Azure에서 클라우드 대장간 시작 aaaGetting | Microsoft Docs"
description: "Microsoft Azure에서 OSS 또는 Pivotal Cloud Foundry 실행"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 2a15ffbf-9f86-41e4-b75b-eb44c1a2a7ab
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/19/2017
ms.author: seanmck
ms.openlocfilehash: 56300d5a0a75b5a9f46145a49ed3f5daa774375a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-foundry-on-azure"></a>Azure의 Cloud Foundry

Cloud Foundry는 다양한 언어 및 프레임워크로 개발되는 12개 요소(12-factor) 응용 프로그램을 빌드하고, 배포하고, 운영하기 위한 오픈 소스 PaaS(Platform-as-a-Service)입니다. 이 문서에서는 Azure 및 시작할 수 있는 방법에서 클라우드 대장간 실행에 대 한 hello 옵션 설명 합니다.

## <a name="cloud-foundry-offerings"></a>Cloud Foundry 제품

두 가지 방법으로 Azure에서 사용할 수 있는 toorun 클라우드 대장간 형식의: 오픈 소스 클라우드 대장간 (OSS CF) 및 중요 클라우드 대장간 (PCF). OSS CF는는 완전히 [오픈 소스](https://github.com/cloudfoundry) hello 클라우드 대장간 Foundation에서 관리 하는 클라우드 대장간의 버전입니다. 중요 클라우드 대장간은 중요 소프트웨어 inc.에서 클라우드 대장간은 엔터프라이즈 배포 보면 hello 차이점 hello 두 가지 제공 합니다.

### <a name="open-source-cloud-foundry"></a>오픈 소스 Cloud Foundry

먼저 BOSH 디렉터를 배포 하 고 다음 클라우드 대장간, hello를 사용 하 여를 배포 하 여 Azure에서 클라우드 대장간 OSS를 배포할 수 있습니다 [GitHub에서 제공 된 지침](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md)합니다. OSS CF 사용에 대 한 더 toolearn 참조 hello [설명서](https://docs.cloudfoundry.org/) hello 클라우드 대장간 Foundation에서 제공 합니다.

Microsoft는 커뮤니티 채널을 따라 hello 통해 OSS CF에 대 한 최상의 지원:

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a>[Cloud Foundry Slack](https://slack.cloudfoundry.org/)의 bosh-azure-cpi 채널
- [cf-bosh mailing list](https://lists.cloudfoundry.org/pipermail/cf-bosh)
- Hello에 대 한 GitHub 문제 [CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) 및 [service broker](https://github.com/Azure/meta-azure-service-broker/issues)

>[!NOTE]
> 같은 hello 가상 컴퓨터 클라우드 대장간을 실행 하 여 Azure 리소스에 대 한 지원 수준은 hello Azure 지원 계약을 기반으로 합니다. 최상의 커뮤니티 지원은 toohello 클라우드 대장간 관련 구성 요소를만 적용 됩니다.

### <a name="pivotal-cloud-foundry"></a>Pivotal Cloud Foundry

중요 클라우드 대장간 포함 hello 소유 관리 도구 및 엔터프라이즈 지원은 집합과 함께 hello OSS 배포로 동일한 핵심 플랫폼입니다. Azure에서 PCF toorun Pivotal에서 라이선스를 획득 해야 합니다. Azure 마켓플레이스 hello에서 hello PCF 제안을 90 일 평가판 라이선스를 포함합니다.

hello 도구 포함 [중요 Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), 배포 및 클라우드 대장간 foundation의 관리를 간소화 하는 웹 응용 프로그램 및 [중요 응용 프로그램 관리자](https://docs.pivotal.io/pivotalcf/console/), 관리 하기 위한 웹 응용 프로그램 사용자 및 응용 프로그램입니다.

또한 위의 OSS CF에 대해 나열 된 지원 채널을 toohello, PCF 라이선스 있습니다 toocontact Pivotal 지원에 대 한를 가진 합니다. Microsoft 및 Pivotal도 사용 하도록 설정한 toocontact 할 수 있도록 지원 워크플로 어느 쪽에 있고 hello 문제가에 따라 적절히 라우팅할 질문 합니다.

## <a name="azure-service-broker"></a>Service Broker

클라우드 대장간 hello이 권장 ["12 단계 app"](https://12factor.net/) 방법을 확실 하 게 구분 상태 비저장 응용 프로그램 프로세스 및 서비스를 백업 하는 상태 저장을 승격 하 합니다. [서비스 브로커](https://docs.cloudfoundry.org/services/api.html) 일관 된 방식으로 tooprovision을 제공 하 고 백업 서비스 tooapplications 바인딩합니다. hello [Azure service broker](https://github.com/Azure/meta-azure-service-broker) hello 중 일부 Azure 저장소 및 SQL Azure를 포함 하 여이 채널을 통해 핵심 Azure 서비스를 제공 합니다.

중요 클라우드 대장간을 사용 하는 경우 hello service broker는 또한 [타일로 사용할 수 있는](https://docs.pivotal.io/azure-sb/installing.html) hello 중요 네트워크에서에서 합니다.

## <a name="related-resources"></a>관련 리소스

### <a name="visual-studio-team-services-plugin"></a>Visual Studio Team Services 플러그인

클라우드 대장간 적합된 tooagile 소프트웨어 개발, CI (연속 통합) 및 지속적인 업데이트 (CD)의 hello 사용입니다. VSTS Visual Studio Team Services () toomanage 프로젝트를 사용 하 고 tooset 클라우드 대장간 대상 CI/CD 파이프라인 구성 하려는 경우에 hello을 사용할 수 있습니다 [VSTS 클라우드 대장간 빌드 확장](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension)합니다. hello 플러그 인을 사용 하면 간단한 tooconfigure 있으며 Azure 또는 다른 실행에 관계 없이 배포 tooCloud 대장간, 자동화 환경입니다.

## <a name="next-steps"></a>다음 단계

- [중요 클라우드 대장간 hello Azure Marketplace에서 배포](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
- [응용 프로그램 tooCloud 대장간 Azure에서 배포](./cloudfoundry-deploy-your-first-app.md)

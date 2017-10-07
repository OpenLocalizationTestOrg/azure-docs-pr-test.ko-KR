---
title: "Azure에서 SharePoint 서버 팜의 aaaCreate | Microsoft Docs"
description: "Azure 포털 마켓플레이스 hello를 사용 하 여 Azure에서 새 SharePoint 2016 또는 SharePoint 2013 팜을 빠르게 만듭니다."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a>Azure 포털 마켓플레이스 hello를 사용 하 여 SharePoint 서버 팜 만들기

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a>SharePoint 2013 팜
Hello Microsoft Azure 포털 마켓플레이스 미리 구성 된 SharePoint Server 2013 팜을 신속 하 게 만들 수 있습니다. 그러면 개발 및 테스팅 환경에 기본 또는 고가용성 SharePoint 팜이 필요하거나 SharePoint Server 2013을 조직의 협력 솔루션으로 평가하는 경우 상당한 시간을 절약할 수 있습니다.

> [!NOTE]
> hello **SharePoint 서버 팜의** hello Azure 포털의 hello Azure Marketplace에서에서 항목이 제거 되었습니다. Hello로 대체 되었습니다 **SharePoint 2013 비 HA 팜** 및 **SharePoint 2013 HA 팜** 항목입니다.
>
>

기본 SharePoint 팜 hello이이 구성에서 3 개의 가상 컴퓨터가 구성 됩니다.

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

이 팜 구성을 간소화된 SharePoint 앱 개발 설정이나 SharePoint 2013의 최초 평가에 사용할 수 있습니다.

toocreate hello 기본 (3 개 서버) SharePoint 팜:

1. [여기](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/)를 클릭합니다.
2. **배포**를 클릭합니다.
3. Hello에 **SharePoint 2013 비 HA 팜** 창에서 클릭 **만들기**합니다.
4. Hello hello 단계에서 설정을 지정 **SharePoint 2013 만들 비 HA 팜** 창과 클릭 **만들기**합니다.

이 구성에서 9 개의 가상 컴퓨터의 hello 고가용성 SharePoint 팜 구성 됩니다.

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

SharePoint 팜에 대 한이 팜 구성 tootest 높은 클라이언트 부하, hello 외부 SharePoint 사이트의 고가용성 및 SQL Server AlwaysOn 가용성 그룹을 사용할 수 있습니다. 또한 고가용성 환경에서 SharePoint app 개발에 이 구성을 사용할 수 있습니다.

toocreate hello 고가용성 (9-서버) SharePoint 팜:

1. [여기](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/)를 클릭합니다.
2. **배포**를 클릭합니다.
3. Hello에 **SharePoint 2013 HA 팜** 창에서 클릭 **만들기**합니다.
4. Hello hello 7 단계에서 설정을 지정 **SharePoint 2013 HA 팜 만들기** 창과 클릭 **만들기**합니다.

> [!NOTE]
> Hello를 만들 수 없습니다 **SharePoint 2013 비 HA 팜** 또는 **SharePoint 2013 HA 팜** Azure 무료 평가판으로 합니다.
>
>

hello Azure 포털 인터넷 연결 웹 사이트를 사용 하 여 클라우드 전용 가상 네트워크에 이러한 팜 모두를 만듭니다. 사이트 간 VPN 또는 express 경로 연결 백 tooyour 조직 네트워크가 있습니다.

> [!NOTE]
> Hello 기본 만들거나 빌드하면 고가용성 SharePoint 팜에 hello Azure 포털을 사용 하 여 기존 리소스 그룹을 지정할 수 없습니다. 이 제한 해결 toowork Azure PowerShell을 사용한 이러한 팜에는 만듭니다. 자세한 내용은 [Azure PowerShell을 사용하여 SharePoint 2013 개발/테스트 팜 만들기](https://technet.microsoft.com/library/mt743093.aspx#powershell)를 참조하세요.
>
>

## <a name="sharepoint-2016-farms"></a>SharePoint 2016 팜
참조 [이 여기서](https://technet.microsoft.com/library/mt723354.aspx) hello 지침 toobuild hello 다음 SharePoint Server 2016이 단일 서버 팜 합니다.

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a>Hello SharePoint 팜을 관리
원격 데스크톱 연결을 통해 이러한 팜 hello 서버를 관리할 수 있습니다. 자세한 내용은 참조 [toohello 가상 컴퓨터에 로그온](quick-create-portal.md#connect-to-virtual-machine)합니다.

Hello 중앙 관리 SharePoint 사이트 내 사이트, SharePoint 응용 프로그램 및 기타 기능을 구성할 수 있습니다. 자세한 내용은 [SharePoint 구성](http://technet.microsoft.com/library/ee836142.aspx)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* Azure 인프라 서비스에서 추가 [SharePoint 구성](https://technet.microsoft.com/library/dn635309.aspx) 을 검색합니다.

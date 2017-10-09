---
title: "Azure에서 aaaManaging 역할 클라우드 Visual Studio와 함께 서비스 | Microsoft Docs"
description: "Tooadd 및 제거 하는 Azure에서 역할에에서 Visual Studio를 사용 하 여 서비스 클라우드 하는 방법에 대해 알아봅니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a>Visual Studio에서 Azure Cloud Services의 역할 관리
Azure 클라우드 서비스를 만든 후에 새 역할 tooit 추가 하거나 기존 역할에서 제거할 수 있습니다. 또한 기존 프로젝트 가져오고 tooa 역할 변환 수 있습니다. 예를 들어, ASP.NET 웹 응용 프로그램을 가져오고 웹 역할로 지정할 수 있습니다.

## <a name="adding-a-role-tooan-azure-cloud-service"></a>추가 역할 tooan Azure 클라우드 서비스
단계를 수행 하는 hello Visual Studio에서 웹 또는 작업자 역할 tooan Azure 클라우드 서비스 프로젝트를 추가 하는 과정을 안내 합니다.

1. Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.

1. **솔루션 탐색기**, hello 프로젝트 노드를 확장 합니다.

1. 마우스 오른쪽 단추로 클릭 hello **역할** 노드 toodisplay hello 상황에 맞는 메뉴입니다. Hello 상황에 맞는 메뉴에서 선택 **추가**, 다음 hello 현재 솔루션에서 기존 웹 역할 또는 작업자 역할을 선택 하거나 웹 또는 작업자 역할 프로젝트를 만듭니다. 또한 ASP.NET 웹 응용 프로그램 프로젝트와 같은 적절한 프로젝트를 선택하고 역할 프로젝트에 연결할 수 있습니다.

    ![메뉴 옵션 tooadd 역할 tooan Azure 클라우드 서비스 프로젝트](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a>Azure 클라우드 서비스에서 역할 제거
hello 다음 단계 과정을 안내 하면 Visual Studio에서 Azure 클라우드 서비스 프로젝트에서 웹 또는 작업자 역할을 제거 합니다.

1. Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.

1. **솔루션 탐색기**, hello 프로젝트 노드를 확장 합니다.

1. Hello 확장 **역할** 노드.

1. 마우스 오른쪽 단추로 클릭 hello 사용할 노드 tooremove, 마우스, hello 상황에 맞는 메뉴에서 선택 **제거**합니다. 

    ![메뉴 옵션 tooadd 역할 tooan Azure 클라우드 서비스](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a>역할 tooan Azure 클라우드 서비스 프로젝트를 다시 추가 중
클라우드 서비스 프로젝트에서 역할 제거 하지만 나중에 다시 tooadd hello 역할 프로젝트 toohello hello 역할 선언과 기본 특성을, 끝점 및 진단 정보 등 추가 됩니다. 추가 리소스 및 참조가 없는 toohello 추가 `ServiceDefinition.csdef` 파일 또는 toohello `ServiceConfiguration.cscfg` 파일입니다. Toomanually tooadd이 정보를 표시할 경우 해야 이러한 파일에 다시 추가 합니다.

예를 들어 웹 서비스 역할을 제거할 수 있습니다 및 나중 tooadd이이 역할에서 다시 솔루션으로 합니다. 이 작업을 수행하는 경우 오류가 발생합니다. tooprevent이이 오류를 tooadd hello 있는 `<LocalResources>` XML hello로 다시 hello 뒤에 나오는 요소 `ServiceDefinition.csdef` 파일입니다. Hello hello에 대 한 hello name 특성의 일부로 hello 프로젝트에 다시 추가한 웹 서비스 역할의 사용 하 여 hello 이름을  **<LocalStorage>**  요소입니다. 이 예제에서는 hello hello 웹 서비스 역할의 이름은 **WCFServiceWebRole1**합니다.

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a>다음 단계
- [Visual Studio에서 Azure 클라우드 서비스에 대 한 hello 역할 구성](vs-azure-tools-configure-roles-for-cloud-service.md)

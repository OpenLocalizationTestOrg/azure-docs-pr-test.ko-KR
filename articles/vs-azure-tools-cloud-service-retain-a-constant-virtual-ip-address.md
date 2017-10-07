---
title: "aaaHow tooretain Azure 클라우드 서비스에 대 한 일정 한 가상 IP 주소 | Microsoft Docs"
description: "Azure 클라우드 서비스의 가상 IP 주소 (VIP) hello tooensure 하지 않는 변경 하는 방법에 대해 알아봅니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4a58e2c6-7a79-4051-8a2c-99182ff8b881
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 9e27121797ffb61517b8d2c2661ec44ff7298968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="retain-a-constant-virtual-ip-address-for-an-azure-cloud-service"></a>Azure 클라우드 서비스의 가상 IP 주소를 일정하게 유지
Azure에서 호스트 되는 클라우드 서비스를 업데이트 하면 tooensure hello 가상 IP 주소 (VIP) hello 서비스의 변경 되지 않게 할 수 있습니다. 많은 도메인 관리 서비스 도메인 이름 등록에 대 한 hello DNS 도메인 이름 ()를 사용 합니다. DNS는 hello VIP 남아 hello 동일한 경우에 작동 합니다. Hello를 사용할 수 있습니다 **게시 마법사** 업데이트에 클라우드 서비스의 VIP는 경우 변경 되지 않습니다 hello Azure Tools tooensure 합니다. 방법에 대 한 자세한 내용은 클라우드 서비스에 대 한 DNS 도메인 관리 toouse 참조 [Azure 클라우드 서비스에 대 한 사용자 지정 도메인 이름 구성](cloud-services/cloud-services-custom-domain-name.md)합니다.

## <a name="publish-a-cloud-service-without-changing-its-vip"></a>VIP를 변경하지 않고 클라우드 서비스 게시
클라우드 서비스의 VIP hello tooAzure hello 프로덕션 환경과 같은 특정 환경에서 배포할 먼저 때 할당 됩니다. hello 배포를 명시적으로 삭제 하거나 hello 배포는 hello 배포에 의해 암시적으로 삭제 하는 경우에 hello VIP 변경 프로세스를 업데이트 합니다. tooretain hello VIP를 삭제 하면 안, 배포 하 고 Visual Studio 배포를 자동으로 삭제 되지는 않습니다 있는지 확인 해야 합니다. 

Hello에서 배포 설정을 지정할 수 있습니다 **게시 마법사**를 지 원하는 여러 가지 배포 옵션입니다. 새로 배포 또는 업데이트 배포를 증분 또는 동시에 진행하도록 지정할 수 있습니다. 업데이트 배포의 두 종류 hello VIP를 유지합니다. 이러한 다양한 유형의 배포에 대한 정의는 [Azure 응용 프로그램 게시 마법사](vs-azure-tools-publish-azure-application-wizard.md)를 참조하세요. 또한 클라우드 서비스의 hello 이전 배포 되어 오류가 발생 한 경우의 삭제 여부를 제어할 수 있습니다. 해당 옵션을 올바르게 설정 하지 hello VIP가 예기치 않게 변경 될 수 있습니다.

## <a name="update-a-cloud-service-without-changing-its-vip"></a>VIP를 변경하지 않고 클라우드 서비스 업데이트
1. Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다. 

2. **솔루션 탐색기**, hello 프로젝트를 마우스 오른쪽 단추로 클릭 합니다. Hello 바로 가기 메뉴에서 선택 **게시**합니다.

    ![게시 메뉴](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/solution-explorer-publish-menu.png)

3. Hello에 **Azure 응용 프로그램 게시** 대화 상자, 선택 hello Azure 구독 toowhich toodeploy 원하는 합니다. 필요한 경우 로그인하고 **다음**을 선택합니다.

    ![Azure 응용 프로그램 게시 로그인 페이지](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-signin.png)

4. Hello에 **일반 설정** 탭에서 배포 하는, hello hello 클라우드 서비스 toowhich의 hello 이름이 확인 **환경**, hello **빌드 구성을**, 및 hello **서비스 구성** 모두 정확 합니다.

    ![Azure 응용 프로그램 게시 일반 설정 탭](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-common-settings.png)

5. Hello에 **고급 설정** 탭에서 해당 hello 확인 **배포 레이블** 및 hello **저장소 계정** 올바른지 합니다. 해당 hello 확인 **실패 시 배포 삭제** 확인란의 선택을 취소 하 고 해당 hello 확인 **배포 업데이트** 확인란을 선택 합니다. Hello 선택을 취소 하 여 **실패 시 배포 삭제** VIP 배포 하는 동안 오류가 발생 하면 손실 되지 되도록 확인란을 있습니다. Hello를 선택 하 여 **배포 업데이트** 배포는 삭제 되지 않습니다 및 VIP는 손실 되지 않습니다 응용 프로그램을 다시 게시할 때 확인 확인란을 합니다. 

    ![Azure 응용 프로그램 게시 고급 설정 탭](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-advanced-settings.png)

6. toofurther hello 역할 toobe 업데이트 되는 방법을 지정, 선택 **설정** 다음 너무**배포 업데이트**합니다. **증분 업데이트** 또는 **동시 업데이트**를 선택한 다음 **확인**을 선택합니다. 선택 **증분 업데이트** tooupdate 응용 프로그램의 각 인스턴스가 차례로 하므로 응용 프로그램을 hello 하는 항상 사용할 수 있습니다. 선택 **동시 업데이트** tooupdate hello에서의 응용 프로그램의 모든 인스턴스가 동시 합니다. 동시 업데이트는 속도가 더 있지만 hello 업데이트 과정 인해 서비스를 사용할 수 있습니다. 작업을 마쳤으면 **다음**을 선택합니다.

    ![Azure 응용 프로그램 게시 배포 설정 페이지](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-deployment-update-settings.png)

7. Hello에 **Azure 응용 프로그램 게시** 대화 상자에서 **다음** hello까지 **요약** 페이지가 표시 됩니다. 설정을 확인한 다음 **게시**를 선택합니다.
   
    ![Azure 응용 프로그램 게시 요약 페이지](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-summary.png)

## <a name="next-steps"></a>다음 단계
- [Hello Visual Studio Azure 응용 프로그램 게시 마법사를 사용 하 여](vs-azure-tools-publish-azure-application-wizard.md)


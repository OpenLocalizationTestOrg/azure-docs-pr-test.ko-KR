---
title: "Azure Data Factory에서 데이터 관리 게이트웨이 통해 aaaHigh 가용성 | Microsoft Docs"
description: "이 문서에서는 노드를 더 많이 추가하여 데이터 관리 게이트웨이를 확장하고, 노드에서 실행할 수 있는 동시 작업 수를 늘려 강화하는 방법을 설명합니다."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: abnarain
ms.openlocfilehash: 925f63728e23596bca2655636f6535b509fce0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway---high-availability-and-scalability-preview"></a>데이터 관리 게이트웨이 - 고가용성 및 확장성(미리 보기)
이 문서에서는 데이터 관리 게이트웨이를 사용하여 고가용성 및 확장성 솔루션을 구성하는 방법에 대해 설명합니다.    

> [!NOTE]
> 이 문서에서는 사용자가 이미 데이터 관리 게이트웨이에 대한 기본 사항을 잘 알고 있다고 가정합니다. 그렇지 않은 경우 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)를 참조하세요.

>**이 미리 보기 기능은 데이터 관리 게이트웨이 버전 2.12.xxxx.x 이상에서 공식적으로 지원됩니다**. 버전 2.12.xxxx.x 이상을 사용하고 있는지 확인하세요. Hello 최신 버전의 데이터 관리 게이트웨이 다운로드 [여기](https://www.microsoft.com/download/details.aspx?id=39717)합니다.

## <a name="overview"></a>개요
Hello 포털에서 단일 논리 게이트웨이 통해 여러 온-프레미스 컴퓨터에 설치 되는 데이터 관리 게이트웨이에 연결할 수 있습니다. 이러한 컴퓨터를 **노드**라고 합니다. 너무를 만들 수 있습니다**4 개 노드** 논리 게이트웨이에 연결 된입니다. 논리 게이트웨이에 대 한 여러 개의 노드 (설치 된 게이트웨이 통해 온-프레미스 컴퓨터)의 hello 이점은 다음과 같습니다.  

- 온-프레미스 및 클라우드 데이터 저장소 간의 데이터 이동 성능을 향상시킵니다.  
- 어떤 이유로 작동이 hello 노드 중 하나에 다른 노드는 hello 데이터 이동에 계속 사용할 수 있습니다. 
- 유지 관리를 위해 오프 라인 toobe 필요 hello 노드 중 하나, 다른 노드는 hello 데이터 이동에 계속 사용할 수 있습니다.

Hello 수를 구성할 수도 있습니다 **동시 데이터 이동 작업** 온-프레미스와 클라우드 간의 데이터 이동의 hello 기능 위로 노드 tooscale에서 실행할 수 있는 데이터 저장소입니다. 

Hello Azure 포털을 사용 하 여 결정 하는 데 도움이 됩니다. 이러한 노드 hello 상태를 모니터링할 수 있는지 여부를 tooadd 또는 hello 논리 게이트웨이에서 노드를 제거 합니다. 

## <a name="architecture"></a>아키텍처 
hello 다음 다이어그램에서는 확장성의 hello 아키텍처 개요 및 데이터 관리 게이트웨이 hello의 가용성 기능: 

![데이터 관리 게이트웨이 - 고가용성 및 확장성](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-high-availability-and-scalability.png)

A **논리 게이트웨이** 는 hello 게이트웨이 hello Azure 포털에서에서 tooa 데이터 팩터리를 추가 합니다. 이전에는 온-프레미스 Windows 컴퓨터 하나만 논리 게이트웨이가 설치된 데이터 관리 게이트웨이와 연결할 수 있었습니다. 이 온-프레미스 게이트웨이 컴퓨터를 노드라고 합니다. 이제, 연결할 수 있습니다를 너무**4 개의 실제 노드가** 논리 게이트웨이 사용 합니다. 여러 노드가 있는 논리 게이트웨이를 **다중 노드 게이트웨이**라고 합니다.  

이러한 노드는 모두 **활성** 상태입니다. 온-프레미스와 클라우드 간 데이터 이동 작업 toomove 데이터를 처리할 수 모두 데이터 저장소입니다. 디스패처와 작업자 역할로 hello 노드 중 하나 Hello 그룹의 다른 노드에 작업자 노드입니다. A **발송자** 노드의 데이터 이동 작업/작업 hello 클라우드 서비스에서 끌어와 tooworker 노드 (자체 포함)를 디스패치합니다. A **작업자** 온-프레미스와 클라우드 간 데이터 이동 작업 toomove 데이터를 실행 하는 노드가 데이터 저장소입니다. 모든 노드는 작업자입니다. 하나의 노드만 디스패처 및 작업자가 모두 될 수 있습니다.    

일반적으로 하나의 노드가 시작할 수 있습니다 및 **확장할** tooadd 더 많은 노드를 기존 노드에 hello hello 데이터 이동 부하로 초과 됩니다. 수도 있습니다 **수직** hello toorun hello 노드에서 허용 되는 동시 작업 수를 늘려 게이트웨이 노드의 데이터 이동 기능 hello 합니다. 이 기능은 단일 노드 게이트웨이 (hello 확장성 및 가용성 기능을 사용할 경우에)를 통해 사용할 수도 있습니다. 

여러 개의 노드가 게이트웨이에 모든 노드에 걸쳐 동기화 hello 데이터 저장소 자격 증명을 유지합니다. 노드를 연결 문제가 있는 경우에 hello 자격 증명 동기화 수 있습니다. 게이트웨이 사용 하는 온-프레미스 데이터 저장소에 대 한 자격 증명을 설정 하는 경우 자격 증명 hello 발송자/작업자 노드에 저장 합니다. hello 발송자 노드 다른 작업자 노드와 동기화 합니다. 이 프로세스 라고 **자격 증명을 동기화**. 노드 간 통신 채널 hello 될 수 있습니다 **암호화 된** 공개 SSL/TLS 인증서가 있습니다. 

## <a name="set-up-a-multi-node-gateway"></a>다중 노드 게이트웨이 설정
이 섹션에서는 다음 두 문서 또는 이러한 문서에 대 한 개념에 익숙한 hello를 통해 수행한 가정 합니다. 

- [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) -hello 게이트웨이의 상세한 개요를 제공 합니다.
- [온-프레미스 및 클라우드 저장소 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) - 단일 노드가 있는 게이트웨이를 사용하기 위한 단계별 지침이 포함된 연습을 제공합니다.  

> [!NOTE]
> 온-프레미스 Windows 컴퓨터에 데이터 관리 게이트웨이 설치 하기 전에 필수 구성 요소에 나열 된 참조 [hello 주 문서](data-factory-data-management-gateway.md#prerequisites)합니다.

1. Hello에 [연습](data-factory-move-data-between-onprem-and-cloud.md#create-gateway), 논리 게이트웨이 만드는 동안 hello를 사용 하도록 설정 **고가용성 및 확장성** 기능입니다. 

    ![데이터 관리 게이트웨이- 고가용성 및 확장성 사용](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-enable-high-availability-scalability.png)
2. Hello에 **구성** 페이지에서 사용 하 여 **Express 설치 프로그램** 또는 **수동 설치** tooinstall hello 첫 번째 노드 (온-프레미스 Windows 컴퓨터)에 게이트웨이 연결 합니다.

    ![데이터 관리 게이트웨이 - 기본 설치 또는 수동 설치](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-express-manual-setup.png)

    > [!NOTE]
    > Hello 빠른 설치 옵션을 사용 하는 경우 hello에 노드 통신 암호화 하지 않고 수행 됩니다. hello 노드 이름은 hello 컴퓨터 이름과 달라 서입니다. Hello 노드 통신 toobe 암호화 하거나 사용자가 선택한 노드 이름을 toospecify를 원하는 경우 수동 설치 프로그램을 사용 합니다. 노드 이름은 나중에 편집할 수 없습니다.
3. **기본 설치**를 선택하는 경우
    1. Hello 메시지 hello 게이트웨이 성공적으로 설치 후의 뒤에 표시 됩니다.

        ![데이터 관리 게이트웨이 - 성공적인 기본 설치](media/data-factory-data-management-gateway-high-availability-scalability/express-setup-success.png)
    2. 수행 하 여 hello 게이트웨이에 대 한 데이터 관리 구성 관리자를 시작 [이러한 지침](data-factory-data-management-gateway.md#configuration-manager)합니다. Hello 게이트웨이 이름, 노드 이름, 상태 등을 참조 합니다.

        ![데이터 관리 게이트웨이 - 성공적인 설치](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)
4. **수동 설치**를 선택하는 경우 :
    1. Hello Microsoft 다운로드 센터에서에서 hello 설치 패키지를 다운로드, tooinstall 게이트웨이 컴퓨터에서 실행 합니다.
    2. 사용 하 여 hello **인증 키** hello에서 **구성** 페이지 tooregister hello 게이트웨이 합니다.
    
        ![데이터 관리 게이트웨이 - 성공적인 설치](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-authentication-key.png)
    3. Hello에 **새 게이트웨이 노드** 페이지에서 사용자 지정을 제공할 수 있습니다 **이름** toohello 게이트웨이 노드에 있습니다. 기본적으로 노드 이름은 hello 컴퓨터 이름과 달라 서입니다.    

        ![데이터 관리 게이트웨이 - 이름 지정](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-name.png)
    4. Hello 다음 페이지에서 너무 여부를 선택할 수**에 노드 통신에 대 한 암호화를 사용 하도록 설정**합니다. 클릭 **Skip** toodisable 암호화 (기본값).

        ![데이터 관리 게이트웨이 - 암호화 사용](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-node-encryption.png)  
    
        > [!NOTE]
        > 암호화 모드의 변경을 단일 게이트웨이 노드 hello 논리 게이트웨이에 있을 때만 지원 됩니다. 다음 단계에는 여러 노드를 게이트웨이 경우 toochange hello 암호화 모드 hello지 않습니다: 노드 하나를 제외 하 고 hello 노드를 모두 삭제 hello 암호화 모드를 변경 하 고 hello 노드를 다시 추가 하십시오.
        > 
        > TLS/SSL 인증서 사용에 대한 요구 사항 목록은 [TLS/SSL 인증서 요구 사항](#tlsssl-certificate-requirements) 섹션을 참조하세요. 
    5. Hello 게이트웨이 성공적으로 설치한 후에 구성 관리자를 실행 하십시오.
    
        ![수동 설치 - 구성 관리자 시작](media/data-factory-data-management-gateway-high-availability-scalability/manual-setup-launch-configuration-manager.png)   
    6. 연결 상태를 보여 주는 hello 노드 (온-프레미스 Windows 컴퓨터)에서 데이터 관리 게이트웨이 구성 관리자를 참조 **게이트웨이 이름**, 및 **노드 이름을**합니다.  

        ![데이터 관리 게이트웨이 - 성공적인 설치](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)

        > [!NOTE]
        > Azure VM에 hello 게이트웨이 프로 비전 하는 경우 사용할 수 있습니다 [GitHub에서이 Azure 리소스 관리자 템플릿을](https://github.com/xiaoyingLJ/vms-with-multiple-data-management-gateway)합니다. 이 스크립트 논리 게이트웨이 만듭니다, 그리고 데이터 관리 게이트웨이 소프트웨어가 설치 된 Vm을 설정 하 고 hello 논리 게이트웨이와 해당 어셈블리가 등록. 
6. Azure 포털에서 시작 hello **게이트웨이** 페이지: 
    1. Hello 데이터 팩터리 포털의 홈 페이지 hello, 클릭 **연결 된 서비스**합니다.
    
        ![데이터 팩터리 홈페이지](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-home-page.png)
    2. hello 선택 **게이트웨이** toosee hello **게이트웨이** 페이지:
    
        ![데이터 팩터리 홈페이지](media/data-factory-data-management-gateway-high-availability-scalability/linked-services-gateway.png)
    4. Hello 참조 **게이트웨이** 페이지:   

        ![단일 노드가 있는 게이트웨이 보기](media/data-factory-data-management-gateway-high-availability-scalability/gateway-first-node-portal-view.png) 
7. 클릭 **노드 추가** hello 도구 모음 tooadd 노드 toohello 논리 게이트웨이에 있습니다. Toouse 빠른 설치를 계획 하는 경우 노드 toohello 게이트웨이로 추가 될 hello 온-프레미스 컴퓨터에서이 단계를 수행 합니다. 

    ![데이터 관리 게이트웨이 - 노드 추가 메뉴](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)
8. 단계는 hello 첫 번째 노드를 유사한 toosetting 합니다. hello Configuration Manager UI hello 수동 설치 옵션을 선택 하는 경우 hello 노드 이름을 설정할 수 있습니다. 

    ![구성 관리자 - 두 번째 게이트웨이 설치](media/data-factory-data-management-gateway-high-availability-scalability/install-second-gateway.png)
9. Hello 게이트웨이 hello 노드에서 성공적으로 설치 된 후 hello 구성 관리자 도구는 hello 화면에 다음을 표시 합니다.  

    ![구성 관리자 - 성공적인 두 번째 게이트웨이 설치](media/data-factory-data-management-gateway-high-availability-scalability/second-gateway-installation-successful.png)
10. Hello를 열면 **게이트웨이** 페이지 hello 포털에서 일도 일어나지 두 게이트웨이 노드: 

    ![Hello 포털에서 두 개의 노드가 있는 게이트웨이](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)
11. toodelete 게이트웨이 노드를 클릭 하 여 **노드 삭제** hello 도구 모음의 hello 사용할 노드 toodelete, 마우스 클릭 한 다음 선택 **삭제** hello 도구 모음에서 합니다. 이 작업 hello 그룹에서 hello 선택 된 노드를 삭제합니다. Note이 이렇게 hello 노드 (온-프레미스 Windows 컴퓨터)에서 hello 데이터 관리 게이트웨이 소프트웨어를 제거 하지 않습니다. 사용 하 여 **프로그램 추가 / 제거** hello 온-프레미스 toouninstall hello 게이트웨이에서 제어판에서. Hello 노드에서 게이트웨이 제거 하면 hello 포털에서 자동으로 삭제 됩니다.   

## <a name="upgrade-an-existing-gateway"></a>기존 게이트웨이 업그레이드
기존 게이트웨이 toouse hello 고가용성 및 확장성 기능을 업그레이드할 수 있습니다. 이 기능은 버전의 hello 데이터 관리 게이트웨이가 있는 노드과만 작동 > 2.12.xxxx = 합니다. Hello 버전의 hello 설치 되어 있는 컴퓨터에 설치 된 데이터 관리 게이트웨이 볼 수 있습니다 **도움말** hello 데이터 관리 게이트웨이 구성 관리자를 탭 합니다. 

1. Hello 게이트웨이 hello 온-프레미스 컴퓨터 toohello 최신 버전에 따라 업데이트를 다운로드 하 고 hello에서 MSI 설치 패키지를 실행 하 여 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=39717)합니다. 자세한 내용은 [설치](data-factory-data-management-gateway.md#installation) 섹션을 참조하세요.  
2. Azure 포털 toohello를 이동 합니다. Hello 시작 **Data Factory 페이지** 데이터 팩토리에 대 한 합니다. 연결 된 서비스 타일 toolaunch hello 클릭 **연결 된 서비스 페이지**합니다. 선택 hello 게이트웨이 toolaunch hello **게이트웨이 페이지**합니다. 클릭 하 고 사용 하도록 설정 **미리 보기 기능** hello 다음 이미지와 같이: 

    ![데이터 관리 게이트웨이 - 미리 보기 기능 활성화](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-existing-gateway-enable-high-availability.png)   
2. Hello 미리 보기 기능 hello 포털에서 활성화 되 면 모든 페이지를 닫습니다. Hello를 다시 열고 **게이트웨이 페이지** toosee hello 새 미리 보기 사용자 인터페이스 (UI).
 
    ![데이터 관리 게이트웨이 - 성공적인 미리 보기 기능 활성화](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview-success.png)

    ![데이터 관리 게이트웨이 - 미리 보기 UI](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview.png)

    > [!NOTE]
    > Hello 업그레이드 하는 동안 hello 첫 번째 노드의 이름을 hello 컴퓨터 hello 이름이입니다. 
3. 이제 노드를 추가합니다. Hello에 **게이트웨이** 페이지 **노드 추가**합니다.  

    ![데이터 관리 게이트웨이 - 노드 추가 메뉴](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)

    Hello 노드를 이전 섹션 tooset hello에서에서 지침을 따릅니다. 

### <a name="installation-best-practices"></a>설치 모범 사례

- Hello 컴퓨터는 최대 절전 모드 없음 있도록 hello 게이트웨이에 대 한 hello 호스트 컴퓨터에 전원 관리 옵션을 구성 합니다. Hello 호스트 컴퓨터 최대 절전 모드로 전환 하는 경우 hello 게이트웨이 toodata 요청 응답 하지 않습니다.
- Hello 게이트웨이에 연결 된 hello 인증서를 백업 합니다.
- 이상적인 성능을 위해 모든 노드에서 비슷한 구성(권장)을 유지해야 합니다. 
- 두 개 이상의 노드가 tooensure 고가용성을 추가 합니다.  

### <a name="tlsssl-certificate-requirements"></a>TLS/SSL 인증서 요구 사항
다음은 게이트웨이 노드 간의 통신 보안에 사용 되는 hello TLS/SSL 인증서에 대 한 hello 요구 사항입니다.

- hello 인증서는 공개적으로 신뢰할 수 있는 X509 해야 v3 인증서입니다.
- 모든 게이트웨이 노드에서 이 인증서를 신뢰해야 합니다. 
- 공용(타사) CA(인증 기관)에서 발급한 인증서를 사용하는 것이 좋습니다.
- Windows Server 2012 R2에서 지원하는 SSL 인증서의 키 크기는 모두 지원됩니다.
- CNG 키를 사용하는 인증서는 지원하지 않습니다.
- 와일드카드 인증서가 지원됩니다. 


## <a name="monitor-a-multi-node-gateway"></a>다중 노드 게이트웨이 모니터링
### <a name="multi-node-gateway-monitoring"></a>다중 노드 게이트웨이 모니터링
Hello Azure 포털에서에서 게이트웨이 노드의 상태와 함께 각 노드에서 리소스 사용률 (CPU, 메모리, network(in/out), 등)의 거의 실시간으로 스냅숏을 볼 수 있습니다. 

![데이터 관리 게이트웨이 - 다중 노드 모니터링](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)

사용 하도록 설정할 수 **고급 설정** hello에 **게이트웨이** toosee 같은 메트릭이 고급 페이지 **네트워크**(in/out), **role&자격증명상태**, 게이트웨이 문제를 디버깅 하는 데 도움이 되 고 **동시 작업** (실행 / 제한)는 수 수 수정 / 하는 동안 그에 따라 변경 된 성능 조정 합니다. hello 다음 표에서 설명 hello에 있는 열의 **게이트웨이 노드** 목록:  

모니터링 속성 | 설명
:------------------ | :---------- 
이름 | Hello 논리 게이트웨이 및 노드 hello 게이트웨이에 연결 된 이름입니다.  
가동 상태 | Hello 논리 게이트웨이 및 게이트웨이 노드 hello의 상태입니다. 예를 들어 온라인/오프라인/제한 등이 있습니다. 이러한 상태에 대한 자세한 내용은 [게이트웨이 상태](#gateway-status) 섹션을 참조하세요. 
버전 | Hello 버전의 hello 논리 게이트웨이 및 게이트웨이 노드마다 표시 됩니다. hello 버전의 hello 논리 게이트웨이 hello 그룹의 노드는 대부분의 버전에 따라 결정 됩니다. Hello 논리 게이트웨이 설치 프로그램에서 다른 버전으로 노드가 hello 논리 게이트웨이 함수 버전 번호가 같은 제대로 hello와 hello 노드만 합니다. 다른 hello 제한 된 모드에 있는 고 toobe (만 실패 하는 경우 자동 업데이트)를 수동으로 업데이트 해야 합니다. 
사용 가능한 메모리 | 게이트웨이 노드에서 사용 가능한 메모리입니다. 이 값은 거의 실시간 스냅숏입니다. 
CPU 사용률 | 게이트웨이 노드의 CPU 사용률입니다. 이 값은 거의 실시간 스냅숏입니다. 
네트워킹(수신/송신) | 게이트웨이 노드의 네트워크 사용률입니다. 이 값은 거의 실시간 스냅숏입니다. 
동시 작업(실행/제한) | 각 노드에서 실행되는 작업 또는 태스크의 수입니다. 이 값은 거의 실시간 스냅숏입니다. 제한은 hello 각 노드에 대 한 최대 동시 작업을 의미합니다. 이 값은 hello 컴퓨터 크기에 따라 정의 됩니다. Hello 제한 tooscale 고급 시나리오에서 동시 작업 실행을 늘릴 수 있는 CPU / 메모리 / 활용도 낮은, 있지만 네트워크 작업 시간이 초과 되 면 합니다. 이 기능은 단일 노드 게이트웨이 (hello 확장성 및 가용성 기능을 사용할 경우에)를 통해 사용할 수도 있습니다. 자세한 내용은 [크기 조정 고려 사항](#scale-considerations) 섹션을 참조하세요. 
역할 | 두 유형의 역할, 즉 디스패처 및 작업자가 있습니다. 모든 노드는 작업자은 모두 사용 하는 tooexecute 작업 수 있습니다. 클라우드 서비스에서 사용 되는 toopull 작업/작업 이므로 toodifferent 작업자 노드 (자체 포함)를 발송 발송자 노드가 하나만 있습니다. 

![데이터 관리 게이트웨이 - 고급 다중 노드 모니터링](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-advanced.png)

### <a name="gateway-status"></a>게이트웨이 상태

hello 다음 표에서의 가능한 상태는 **게이트웨이 노드**: 

가동 상태  | 설명/시나리오
:------- | :------------------
온라인 | 노드가는 tooData 팩터리 서비스를 연결 합니다.
오프라인 | 노드가 오프라인 상태입니다.
업그레이드 중 | hello 노드 자동 업데이트 되 고 있습니다.
제한적 | TooConnectivity 문제 때문입니다. 기한 tooHTTP 포트 8050 문제, 서비스 버스 연결 문제 또는 자격 증명 동기화 문제 수 있습니다. 
비활성 | 노드는 과반수 노드 다른 hello 구성에서 다른 구성이입니다.<br/><br/> Tooother 노드를 연결할 수 없을 때 노드를 활성화 하지 수 있습니다. 


hello 다음 표에서의 가능한 상태는 **논리 게이트웨이**합니다. 게이트웨이 상태 hello hello 게이트웨이 노드 상태에 따라 달라 집니다. 

가동 상태 | 설명
:----- | :-------
등록이 필요합니다. | 노드가 없습니다은 아직 등록 된 toothis 논리 게이트웨이
온라인 | 게이트웨이 노드가 온라인 상태입니다.
오프라인 | 온라인 상태의 노드가 없습니다.
제한적 | 이 게이트웨이의 모든 노드가 정상 상태가 아닙니다. 이 상태는 일부 노드가 중단되었을 수 있다는 경고입니다. <br/><br/>디스패처/작업자 노드에서 toocredential 동기화 문제가 원인일 수 있습니다. 

### <a name="pipeline-activities-monitoring"></a>파이프라인/활동 모니터링
Azure 포털 hello 경험이 세부적인 노드 수준의 세부 정보를 모니터링 하는 파이프라인을 제공 합니다. 예를 들어 어떤 활동이 어떤 노드에서 실행되었는지를 보여 줍니다. 이 정보는 toonetwork 제한 때문에 예를 들어 특정 노드에 대 한 성능 문제를 이해 하는 데 도움이 될 수 있습니다. 

![데이터 관리 게이트웨이 - 파이프라인에 대한 다중 노드 모니터링](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-pipelines.png)

![데이터 관리 게이트웨이 - 파이프라인 세부 정보](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-pipeline-details.png)

## <a name="scale-considerations"></a>크기 조정 고려 사항

### <a name="scale-out"></a>확장
Hello 때 **사용 가능한 메모리가 적으면** hello 및 **CPU 사용량이 많습니다**, 컴퓨터 간에 hello 부하 확장을 사용 하면 새 노드를 추가 합니다. 활동은 tootime 아웃 또는 게이트웨이 노드를 오프 라인 상태로 유지 인해 실패 한 경우 노드 toohello 게이트웨이 추가 하는 경우 도움이 됩니다.
 
### <a name="scale-up"></a>강화
Hello 사용 가능한 메모리 및 CPU, 사용 되지 않습니다 hello 유휴 용량이 0입니다. 하지만 경우 조정 해야 hello 노드에서 실행할 수 있는 동시 작업 수를 늘려 합니다. 작업 시간이 초과 되 면 hello 게이트웨이 오버 로드 때문에 때를 tooscale를 할 수 있습니다. 다음 이미지는 hello와 같이 hello 노드에 대 한 최대 용량을 늘릴 수 있습니다. 와 toostart 더블링 하는 것이 좋습니다.  

![데이터 관리 게이트웨이 - 크기 조정 고려 사항](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-scale-considerations.png)


## <a name="known-issuesbreaking-changes"></a>알려진 문제점 및 변경 내용

- 현재 단일 논리 게이트웨이에 대 한 toofour 실제 게이트웨이 노드를 만들 수 있습니다. 노드가 4 개 이상 성능상의 이유로 해야 할 경우 전자 메일 보내기 너무[DMGHelp@microsoft.com](mailto:DMGHelp@microsoft.com)합니다.
- 다시 hello 현재 논리 게이트웨이에서 다른 논리 게이트웨이 tooswitch에서 hello 인증 키가 있는 게이트웨이 노드를 등록할 수 없습니다. toore 레지스터 hello 노드에서 hello 게이트웨이 제거 하 고, 다시 hello 게이트웨이, 다른 논리 게이트웨이 hello에 대 한 hello 인증 키로 등록 합니다. 
- HTTP 프록시에 필요한 경우 모든 게이트웨이 노드를 diahost.exe.config 및 diawp.exe.config, hello 프록시를 설정 하 고 hello 서버 관리자 toomake 모든 노드가 동일한 diahost.exe.config 및 diawip.exe.config hello가 있는지를 사용 합니다. 자세한 내용은 [프록시 설정 구성](data-factory-data-management-gateway.md#configure-proxy-server-settings) 섹션을 참조하세요. 
- 게이트웨이 구성 관리자에서 노드 통신용 toochange 암호화 모드 하나만 제외 하 고 hello 포털에서 모든 hello 노드를 삭제 합니다. Hello 암호화 모드를 변경한 후 다시 노드를 추가 합니다.
- 공식 SSL 인증서를 사용 하 여 tooencrypt hello에 노드 통신 채널을 선택 하는 경우. 자체 서명 된 인증서는 다른 컴퓨터에 인증 기관 목록에 동일한 인증서를 신뢰할 수 있습니다 hello로 연결 문제가 발생할 수 있습니다. 
- Hello 노드 버전이 hello 논리 게이트웨이 버전 보다 낮은 경우 노드 tooa 논리는 게이트웨이 등록할 수 없습니다. 더 낮은 버전 node(downgrade)를 등록할 수 있도록 포털에서 hello 논리 게이트웨이의 모든 노드를 삭제할 것입니다. 논리 게이트웨이의 모든 노드를 삭제 하면 수동으로 설치 및 노드 toothat 논리 새 게이트웨이 등록 합니다. 이 경우 기본 설치는 지원되지 않습니다.
- 빠른 설치 tooinstall 노드 tooan 기존 논리 게이트웨이 클라우드 자격 증명을 사용 하 여 여전히은 사용할 수 없습니다. Hello 설정 탭에서 hello 게이트웨이 구성 관리자에서에서 hello 자격 증명이 저장 되는 위치를 확인할 수 있습니다.
- 빠른 설치 tooinstall 노드 tooan 기존 논리 게이트웨이 노드 암호화가 설정에 사용할 수 없습니다. 인증서를 추가 하는 수동으로 포함 하는 hello 암호화 모드 설정, 빠른 설치는 옵션이 더 이상 없습니다. 
- 온-프레미스 환경에서 파일을 복사하는 경우 localhost 또는 로컬 드라이브에서 모든 노드를 통해 액세스할 수 없으므로 \\localhost 또는 C:\files를 더 이상 사용하면 안됩니다. 대신를 사용 하 여 \\ServerName\files toospecify 파일의 위치입니다.


## <a name="rolling-back-from-hello-preview"></a>Hello 미리 보기에서 롤백 
hello 미리 보기에서 다시 tooroll 한 노드를 제외한 모든 노드를 삭제 합니다. 노드를 삭제 하지만 hello 논리 게이트웨이에 노드가 하나 이상 있는지 확인 문제가 되지 않습니다. Hello 컴퓨터에 게이트웨이 제거 하 여 또는 hello Azure 포털을 사용 하 여 노드를 삭제할 수 있습니다. Hello hello에서 Azure 포털에서에서 **Data Factory** 페이지에서 연결 된 서비스 toolaunch hello **연결 된 서비스** 페이지. 선택 hello 게이트웨이 toolaunch hello **게이트웨이** 페이지. Hello 게이트웨이 페이지 hello 게이트웨이에 연결 된 hello 노드를 볼 수 있습니다. hello 페이지 hello 게이트웨이에서 노드를 삭제할 수 있습니다.
 
를 삭제 한 후 클릭 **미리 보기 기능** 에 동일한 Azure 포털 페이지 hello 및 hello 미리 보기 기능을 사용 하지 않도록 설정 합니다. 게이트웨이 tooone 노드 GA (일반 공급) 게이트웨이 다시 설정 했습니다.


## <a name="next-steps"></a>다음 단계
Hello 다음 문서를 검토 합니다.
- [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) -hello 게이트웨이의 상세한 개요를 제공 합니다.
- [온-프레미스 및 클라우드 저장소 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) - 단일 노드가 있는 게이트웨이를 사용하기 위한 단계별 지침이 포함된 연습을 제공합니다. 

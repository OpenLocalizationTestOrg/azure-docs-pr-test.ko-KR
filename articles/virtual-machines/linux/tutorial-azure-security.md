---
title: "Azure의 aaaAzure 보안 센터 및 Linux 가상 컴퓨터 | Microsoft Docs"
description: "Azure Security Center를 사용하여 Azure Linux 가상 컴퓨터의 보안을 유지하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/07/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7aa0de35fb311457e769f152c8575ec43e41c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a>Azure Security Center를 사용하여 가상 컴퓨터 보안 모니터링

Azure Security Center를 사용하면 Azure 리소스 보안 사례에 대한 가시성을 얻을 수 있습니다. Security Center는 통합 보안 모니터링 기능을 제공합니다. 다른 방법으로는 눈에 띄지 않을 수 있는 위협을 검색할 수 있습니다. 이 자습서에서는 Azure Security Center에 대해 알아보고 다음을 수행하는 방법에 대해 설명합니다.
 
> [!div class="checklist"]
> * 데이터 수집 설정
> * 보안 정책 설정
> * 구성 상태 문제 보기 및 수정
> * 검색된 위협 검토  

## <a name="security-center-overview"></a>Security Center 개요

Security Center는 잠재적인 VM(가상 컴퓨터) 구성 문제 및 대상이 되는 보안 위협을 식별합니다. 여기에는 네트워크 보안 그룹이 누락된 VM, 암호화되지 않은 디스크 및 RDP(원격 데스크톱 프로토콜) 무차별 암호 대입 공격이 포함될 수 있습니다. hello 정보는 읽기 쉬운 그래프의 hello 보안 센터 대시보드에 표시 됩니다.

tooaccess hello hello hello 메뉴에서 Azure 포털의에서 보안 센터 대시보드에서 **보안 센터**합니다. Hello 대시보드에서 Azure 환경의 hello 보안 상태를 볼 현재 권장 사항 수를 찾을 고 hello 위협 경고의 현재 상태를 볼 수 있습니다. 자세한 내용은 각 수준 높은 toosee를 확장할 수 있습니다.

![Security Center 대시보드](./media/tutorial-azure-security/asc-dash.png)

보안 센터가 발견 되는 문제에 대 한 데이터 검색 tooprovide 권장 사항을 초과 합니다. 예를 들어 연결된 네트워크 보안 그룹 없이 VM을 배포한 경우 Security Center에서 수행할 수 있는 재구성 단계와 함께 권장 사항을 표시합니다. 보안 센터의 hello 컨텍스트를 벗어나지 않고 자동화 된 업데이트 관리를 가져옵니다.  

![권장 사항](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a>데이터 수집 설정

VM 보안 구성으로 파악할 수 있습니다, 전에 tooset 보안 센터 데이터 컬렉션을 해야 합니다. Azure 저장소 계정 toohold 수집 된 데이터를 만들고 데이터 컬렉션을 켠 포함 됩니다. 

1. Hello 보안 센터 대시보드에서 **보안 정책**, 한 다음 구독을 선택 합니다. 
2. **데이터 수집**에서 **설정**을 선택합니다.
3. 저장소 계정 toocreate 선택 **저장소 계정을 선택**합니다. 그런 다음 **확인**을 선택합니다.
4. Hello에 **보안 정책** 블레이드를 **저장**합니다. 

hello 보안 센터 데이터 수집 에이전트는 다음 모든 Vm에 설치 하 고 데이터 수집을 시작 합니다. 

## <a name="set-up-a-security-policy"></a>보안 정책 설정

보안 정책은 사용 되는 toodefine hello 항목을 보안 센터 데이터를 수집 하 고 필요한 사항을 권장 됩니다. Azure 리소스의 다양 한 보안 정책을 toodifferent 집합을 적용할 수 있습니다. 기본적으로 Azure 리소스가 모든 정책 항목에 대해 평가되지만, 모든 Azure 리소스 또는 리소스 그룹에 대해 개별 정책 항목을 해제할 수 있습니다. Azure Security Center 보안 정책에 대한 자세한 내용은 [Azure Security Center에서 보안 정책 설정](../../security-center/security-center-policies.md)을 참조하세요. 

모든 Azure 리소스에 대 한 보안 정책을 tooset:

1. Hello 보안 센터 대시보드에서 선택 **보안 정책**, 한 다음 구독을 선택 합니다.
2. **방지 정책**을 선택합니다.
3. 켜기 또는 Azure 리소스 tooapply tooall 정책 항목을 해제 합니다.
4. 설정 선택 작업을 완료했으면 **확인**을 선택합니다.
5. Hello에 **보안 정책** 블레이드를 **저장**합니다. 

특정 리소스 그룹에 대 한 정책을 tooset:

1. Hello 보안 센터 대시보드에서 선택 **보안 정책**, 한 다음 리소스 그룹을 선택 합니다.
2. **방지 정책**을 선택합니다.
3. 켜기 또는 원하는 tooapply toohello 리소스 그룹 정책 항목을 해제 합니다.
4. **상속**에서 **고유**를 선택합니다.
5. 설정 선택 작업을 완료했으면 **확인**을 선택합니다.
6. Hello에 **보안 정책** 블레이드를 **저장**합니다.  

또한 이 페이지에서 특정 리소스 그룹에 대한 데이터 수집도 해제할 수 있습니다.

다음 예제는 hello, 명명 된 리소스 그룹에 대 한 고유한 정책을 만든 후 *myResoureGroup*합니다. 이 정책에서는 디스크 암호화 및 웹 응용 프로그램 방화벽 권장 사항이 모두 해제되어 있습니다.

![고유 정책](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a>VM 구성 상태 보기

데이터 수집 설정 되었으며 보안 정책을 설정, 보안 센터 tooprovide 알림 및 권장 사항을 시작 합니다. Vm이 배포 된 대로 hello 데이터 컬렉션 에이전트가 설치 됩니다. 보안 센터 hello에 대 한 데이터 채운 다음 새 Vm입니다. VM 구성 상태에 대한 자세한 내용은 [Security Center에서 VM 보호](../../security-center/security-center-virtual-machine-recommendations.md)를 참조하세요. 

데이터 수집 되 면 각 VM 및 관련된 Azure 리소스에 대 한 리소스 상태 hello 집계 됩니다. hello 정보는 읽기 쉬운 차트에 표시 됩니다. 

tooview 리소스 상태:

1.  Hello 보안 센터 대시보드에서 **리소스 보안 상태**선택, **계산**합니다. 
2.  Hello에 **계산** 블레이드를 **가상 컴퓨터**합니다. 이 보기에는 모든 Vm에 대 한 hello 구성 상태 요약을 제공합니다.

![상태 계산](./media/tutorial-azure-security/compute-health.png)

toosee는 VM에 대 한 모든 권장 사항을 hello VM을 선택 합니다. 권장 사항 및 업데이트 관리는 hello이이 자습서의 다음 섹션에서 자세히 다룹니다.

## <a name="remediate-configuration-issues"></a>구성 문제 해결

보안 센터 구성 데이터로 toopopulate 시작 된 후 권장 사항은 수행 됨 기반 hello 보안 정책 설정. 예를 들어, VM으로 설정 된 연결된 네트워크 보안 그룹 없이 권장 하나 toocreate를 이루어집니다. 

모든 권장 사항 목록 toosee: 

1. Hello 보안 센터 대시보드에서 선택 **권장 사항을**합니다.
2. 특정 권장 사항을 선택합니다. Hello 권장 구성에 적용 되는 대 한 모든 리소스의 목록이 표시 됩니다.
3. tooapply 권장 사항, 특정 리소스를 선택 합니다. 
4. 수정 단계에 대 한 hello 지침을 따릅니다. 

실행 가능한 단계는 보안 센터 대부분의 경우에서 보안 센터를 종료 하지 않고 tooaddress 권장을 수행할 수 있습니다. 다음 예제는 hello, 보안 센터 무제한 인바운드 규칙이 있는 네트워크 보안 그룹을 검색 합니다. Hello hello 권장 구성 페이지에서 선택할 수 있습니다 **인바운드 규칙 편집** 단추입니다. hello 필요한 toomodify hello 규칙 되는 UI에 표시 됩니다. 

![권장 사항](./media/tutorial-azure-security/remediation.png)

권장 사항이 해결되면 해결되었다고 표시됩니다. 

## <a name="view-detected-threats"></a>검색된 위협 보기

또한 tooresource 구성 권장 사항, 보안 센터 위협 검색 경고를 표시 합니다. hello 보안 경고 기능은 각 VM, Azure 네트워킹 로그 및 Azure 리소스에 대 한 연결 된 파트너 솔루션 toodetect 보안 위협을에서 수집 된 데이터를 집계 합니다. Security Center 위협 검색 기능에 대한 자세한 내용은 [Azure Security Center 검색 기능](../../security-center/security-center-detection-capabilities.md)을 참조하세요.

hello 보안 경고 기능을 사용 하려면 hello 보안 센터에서 증가 하는 계층 toobe 가격 *무료* 너무*표준*합니다. 30 일 **무료 평가판** 은 toothis 더 높은 가격 책정 계층을 이동 하는 경우 사용할 수 있습니다. 

toochange hello 가격 책정 계층:  

1. Hello 보안 센터 대시보드에서 **보안 정책**, 한 다음 구독을 선택 합니다.
2. **가격 책정 계층**을 선택합니다.
3. Hello 새 계층을 선택한 다음 선택 **선택**합니다.
4. Hello에 **보안 정책** 블레이드를 **저장**합니다. 

Hello 가격 책정 계층을 변경 했으면 보안 위협을 감지 되 면 hello 보안 경고 그래프 toopopulate를 시작 합니다.

![보안 경고](./media/tutorial-azure-security/security-alerts.png)

경고 tooview 정보를 선택 합니다. 예를 들어 hello 위협, hello 검색 시간, 모든 위협 시도에 대 한 설명을 참조할 수 있으며 hello 권장된 업데이트 관리. 다음 예제는 hello에 RDP 무차별 암호 대입 공격 294 실패 한 RDP 시도와 검색 되었습니다. 권장되는 해결 방법이 제공됩니다.

![RDP 공격](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a>다음 단계
이 자습서에서는 Azure Security Center를 설정한 다음 Security Center에서 VM을 검토했습니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * 데이터 수집 설정
> * 보안 정책 설정
> * 구성 상태 문제 보기 및 수정
> * 검색된 위협 검토

Jenkins, GitHub 및 Docker를 사용 하 여 CI/CD 파이프라인 만들기에 대 한 자세한 toohello 다음 자습서 toolearn를 진행 합니다.

> [!div class="nextstepaction"]
> [Jenkins, GitHub 및 Docker를 사용하여 CI/CD 인프라 만들기](tutorial-jenkins-github-docker-cicd.md)


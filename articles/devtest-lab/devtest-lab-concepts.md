---
title: "aaaDevTest 랩 개념 | Microsoft Docs"
description: "Hello DevTest Labs의 기본 개념에 알아봅니다 및 관리 하 고 Azure 가상 컴퓨터를 모니터링 하기 쉬운 toocreate 하 게 수, 하는 방법"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 105919e8-3617-4ce3-a29f-a289fa608fb2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: d9f1d948002c4d3121e5bdd4e65eb8b54cd91f9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="devtest-labs-concepts"></a>DevTest Lab 개념
## <a name="overview"></a>개요
다음 목록 hello 주요 DevTest Labs 개념 및 정의 포함 되어 있습니다.

## <a name="labs"></a>랩
랩은 제한 및 할당량을 지정 하 여 해당 리소스를 관리 하는 더 나은 수 있는 가상 컴퓨터 (Vm) 등의 리소스 그룹을 포함 하는 hello 인프라 합니다.

## <a name="virtual-machine"></a>가상 컴퓨터
Azure VM은 Azure에서 제공하는 여러 유형의 [확장성 있는 주문형 컴퓨팅 리소스](https://docs.microsoft.com/azure/app-service-web/choose-web-site-cloud-service-vm) 중 하나입니다. Azure Vm 제공 toobuy 않고도 가상화의 유연성을 hello 및 toomaintain 여전히 필요 하지만,를 실행 하는 hello 물리적 하드웨어를 유지 관리를 구성, 패치 및 hello 소프트웨어 설치 등의 특정 작업을 수행 하 여 VM을 hello 하에서 실행 합니다.

[Azure에서의 Windows 가상 컴퓨터 개요](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-overview)에서는 VM을 만들기 전에 고려해야 하는 요구 사항, 만드는 방법 및 관리하는 방법을 설명합니다.

## <a name="claimable-vm"></a>클레임할 수 있는 VM
Azure Claimable VM은 권한이 있는 랩 사용자면 누구나 사용할 수 있는 가상 컴퓨터입니다. 랩 관리자는 특정 기본 이미지 및 아티팩트 Vm을 준비 하 고 tooa 공유 풀 저장할 수 있습니다. 다음 랩 사용자는 해당 특정 구성을 사용 하 여 하나 필요로 할 경우 작업 hello 풀에서 VM을 요구할 수 없습니다.

Claimable 된 VM에 처음 tooany 특정 사용자를 할당 되지 않은 있지만 "Claimable 가상 컴퓨터"에서 모든 사용자의 목록에 표시 됩니다. VM 사용자가 권한이 클레임 되 후에 "가상 컴퓨터 내" 영역 tootheir 위로 이동 하 고 다른 사용자가 claimable는 더 이상.

## <a name="environment"></a>Environment
DevTest Labs 환경 tooa 랩에서 Azure 리소스 컬렉션을 나타냅니다. [이 블로그 게시물](https://blogs.msdn.microsoft.com/devtestlab/2016/11/16/connect-2016-news-for-azure-devtest-labs-azure-resource-manager-template-based-environments-vm-auto-shutdown-and-more/) 설명 방법을 toocreate 다중 VM 환경에서 Azure 리소스 관리자 템플릿 합니다.

## <a name="base-images"></a>기본 이미지
기본 이미지는 모든 hello 도구 및 설정 사전 설치 된 VM 이미지 및 구성 된 tooquickly VM을 만듭니다. 있습니다 수 VM을 프로 비전 기존 자료를 선택 하 고 아티팩트 tooinstall를 추가 하 여 테스트 에이전트입니다. 있습니다 수 다음 hello 저장 VM을 프로 비전 기본 hello 자료를 사용할 수 tooreinstall hello 테스트 에이전트의 각 프로 비전에 대 한 필요 없이 있도록 hello VM으로 합니다.

## <a name="artifacts"></a>아티팩트
아티팩트는 사용 되는 toodeploy 및 VM 프로 비전 된 후 응용 프로그램을 구성 합니다. 아티팩트는 다음과 같을 수 있습니다.

* 에이전트, Fiddler 및 Visual Studio와 같은 VM-hello에 tooinstall 원하는 도구입니다.
* 리포지토리 복제 같은 VM-hello에 toorun 되도록 동작입니다.
* 응용 프로그램 tootest 한다는 것입니다.

아티팩트는 [Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md) 지침 tooperform 배포를 포함 하 고 구성을 적용 하는 JSON 파일입니다.

## <a name="artifact-repositories"></a>아티팩트 리포지토리
아티팩트 리포지토리는 아티팩트가 체크 인되는 Git 리포지토리입니다. 아티팩트 저장소 재사용을 사용 하도록 설정 하 고 공유 하 여 조직의 toomultiple 랩 추가할 수 있습니다.

## <a name="formulas"></a>수식
수식 추가 toobase 이미지에서 빠른 VM 프로 비전 하기 위한 메커니즘을 제공합니다. DevTest Labs의 수식에는 기본 속성 사용 되는 값 toocreate 랩 VM의 목록입니다.
식, 기본 이미지, VM 크기, 가상 네트워크 및 아티팩트-예:-의 속성 설정 같은 hello로 Vm 사용 필요 없이 toospecify 속성만 때마다 만들 수 있습니다. Hello 기본 값으로 사용할 수는 수식에서 VM을 만들 때-하거나 수정 합니다.

## <a name="policies"></a>정책
정책은 랩에서의 비용 제어에 도움이 됩니다. 예를 들어 정의 된 일정에 따라 Vm을 종료 하는 정책 tooautomatically를 만들 수 있습니다.

## <a name="caps"></a>캡
대문자는 랩에서 메커니즘 toominimize 낭비입니다. 예를 들어, 사용자 또는 환경에서 만들 수 있는 Vm의 cap toorestrict hello 수를 설정할 수 있습니다.

## <a name="security-levels"></a>보안 수준
보안 액세스는 Azure 역할 기반 액세스 제어(RBAC)를 통해 결정됩니다. toounderstand works 액세스 하는 방법을, RBAC에 정의 된 대로 toounderstand hello 간의 차이점 권한, 역할, 범위는 데 도움이 됩니다.

* 권한-권한 정의 된 액세스 tooa 특정 작업 (예: 읽기 액세스 tooall 가상 컴퓨터)입니다.
* 역할-역할은 그룹화 하 고 할당 된 tooa 사용자 수 있는 사용 권한 집합이 있습니다. 예를 들어 hello *구독 소유자* 역할에는 구독 내의 tooall 리소스에 액세스 합니다.
* 범위-범위는 리소스 그룹, 단일 연구소 또는 hello 전체 구독 같은 Azure 리소스의 hello 계층 내의 수준입니다.

DevTest Labs의 hello 범위는 두 가지 유형의 역할 toodefine 사용자의 사용 권한: 랩 소유자 및 랩 사용자입니다.

* 랩 소유자-랩 소유자가 hello 랩에서 tooany 리소스에 액세스 합니다. 따라서 랩 소유자 수 정책 수정, 읽기 및 쓰기 Vm, hello 가상 네트워크를 변경 등에입니다.
* 랩 사용자 - 랩 사용자는 VM, 정책 및 가상 네트워크와 같은 모든 랩 리소스를 볼 수 있지만 정책 또는 다른 사용자가 만든 VM을 수정할 수 없습니다.

toosee toocreate 사용자 정의 역할에서 DevTest Labs toohello 문서를 참조 하는 방법 [toospecific 랩 정책 사용자 권한 부여](devtest-lab-grant-user-permissions-to-specific-lab-policies.md)합니다.

범위는 계층적이므로 사용자가 특정 범위에서 사용 권한을 가진 경우 포함된 모든 하위 수준 범위에서 해당 사용 권한이 자동으로 부여됩니다. 예를 들어, 사용자가 구독 소유자의 toohello 역할에 할당 한 경우 다음 있는데 tooall 리소스에 액세스 한 구독에서 모든 가상 컴퓨터, 모든 가상 네트워크 및 모든 랩 포함 따라서 구독 소유자는 자동으로 랩 소유자의 hello 역할을 상속합니다. 그러나 hello 반대 사실이 아닙니다. 랩 소유자에 게는 hello 구독 수준 보다 낮은 범위 tooa 랩에 액세스 합니다. 따라서 수 toosee 가상 컴퓨터 또는 가상 네트워크 또는 랩 hello 외부에 있는 모든 리소스 랩 소유자 되지 않습니다.

## <a name="azure-resource-manager-templates"></a>Azure 리소스 관리자 템플릿
반복적으로 일관 된 상태로 배포 및 hello 인프라/Azure 솔루션의 구성 정의 모든 hello 수 있는 Azure 리소스 관리자 템플릿을 사용 하 여이 문서에 설명 된 개념을 구성할 수 있습니다.

[Hello 구조 및 Azure 리소스 관리자 템플릿 구문을 이해](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates#template-format) hello 서식 파일의 서로 다른 섹션에 제공 되는 Azure 리소스 관리자 템플릿 및 hello 속성의 hello 구조를 설명 합니다.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>다음 단계
[DevTest Lab에서 랩 만들기](devtest-lab-create-lab.md)

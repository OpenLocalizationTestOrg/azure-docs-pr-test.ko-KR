---
title: "Jenkins 연속 통합 하기 위해 Azure VM 에이전트를 aaaUse 합니다."
description: "Jenkins 슬레이브로 Azure VM 에이전트입니다."
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a>Jenkins와 연속 통합을 위해 Azure VM 에이전트를 사용합니다.

이 퀵 스타트의 방법을 toouse hello Jenkins Azure VM 에이전트 플러그 인 toocreate Azure에서 요청 시 (Ubuntu) Linux 에이전트를 보여 줍니다.

## <a name="prerequisites"></a>필수 조건

toocomplete이 빠른이 시작:

* Jenkins 마스터 아직 없는 경우 hello로 시작할 수 있습니다 [솔루션 템플릿](install-jenkins-solution-template.md) 
* 너무 참조[Azure CLI 2.0과 함께 Azure 서비스 사용자를 만들](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) Azure 서비스 사용자를 아직 없는 않는 경우.

## <a name="install-azure-vm-agents-plugin"></a>Azure VM 에이전트 플러그 인 설치

Hello에서 시작 하는 경우 [솔루션 템플릿을](install-jenkins-solution-template.md), hello Jenkins 마스터에 hello Azure VM 에이전트 플러그 인이 설치 됩니다.

그렇지 않으면 hello 설치 **Azure VM 에이전트** hello Jenkins 대시보드 내에서 플러그 인 합니다.

## <a name="configure-hello-plugin"></a>Hello 플러그 인 구성

* Hello Jenkins 대시보드 내에서 클릭 **Jenkins 관리-> 시스템 구성->**합니다. Hello 페이지의 맨 아래 toohello 스크롤하여 hello 드롭다운이 있는 hello 섹션을 찾아 **새로운 클라우드 추가**합니다. Hello 메뉴에서 선택 **Microsoft Azure VM 에이전트**
* Hello Azure 자격 증명 드롭다운에서 기존 계정을 선택 합니다.  새 tooadd **Microsoft Azure 서비스 사용자** hello 다음 값을 입력: 구독 ID, 클라이언트 ID, 클라이언트 암호 및 OAuth 2.0 토큰 끝점입니다.

![Azure 자격 증명](./media/jenkins-azure-vm-agents/service-principal.png)

* 클릭 **확인 구성** toomake 해당 hello 프로필 구성이 올바른지 합니다.
* Hello 구성을 저장 하 고 toohello 다음 단계를 계속 합니다.

## <a name="template-configuration"></a>템플릿 구성

### <a name="general-configuration"></a>일반 구성
다음을 사용 하 여 toodefine Azure VM 에이전트에 대 한 템플릿을 구성 합니다. 

* 클릭 **추가** tooadd 서식 파일입니다. 
* 새 템플릿의 이름을 제공합니다. 
* Hello 레이블에 대 한 "ubuntu"를 입력 합니다. 이 레이블은 hello 작업 구성 하는 동안 사용 됩니다.
* Hello 콤보 상자에서 원하는 지역을 hello를 선택 합니다.
* Select hello v M 크기를 권장합니다.
* Hello Azure 저장소 계정 이름을 지정 하거나 빈 toouse hello 기본 이름이 "jenkinsarmst" 둡니다
* Hello 보존 시간을 분 단위로 지정 합니다. 이 설정은 Jenkins 유휴 에이전트를 자동으로 삭제 하기 전에 대기할 수 있는 시간 (분) hello 수를 정의 합니다. 유휴 에이전트 toobe 자동으로 삭제 하지 않을 경우 0을 지정 합니다.

![일반 구성](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a>이미지 구성

Linux (Ubuntu) 에이전트 toocreate 선택 **참조 이미지** 및 사용 하 여 hello 구성을 한 예로 다음과 같은 합니다. 너무 참조[Azure 마켓플레이스](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) hello에 대 한 최신 Azure 이미지를 지원 합니다.

* 이미지 게시자: Canonical
* 이미지 제품: UbuntuServer
* 이미지 SKU: 14.04.5-LTS
* 이미지 버전: 최신
* OS 유형: Linux
* 시작 방법: SSH
* 관리자 자격 증명 제공
* VM 초기화 스크립트의 경우 다음을 입력합니다.
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![이미지 구성](./media/jenkins-azure-vm-agents/image-config.png)

* 클릭 **확인 템플릿** tooverify hello 구성 합니다.
* **Save**를 클릭합니다.

## <a name="create-a-job-in-jenkins"></a>Jenkins에서 작업 만들기

* Hello Jenkins 대시보드 내에서 클릭 **새 항목**합니다. 
* 이름을 입력하고 **프리스타일 프로젝트**를 선택하고 **확인**을 클릭합니다.
* Hello에 **일반** 탭, 선택 "프로젝트를 실행할 수 있는 제한" 및 "ubuntu" 레이블 식의 유형입니다. 이제 "ubuntu" hello 드롭다운에 표시 됩니다.
* **Save**를 클릭합니다.

![작업 설정](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a>새 프로젝트 빌드

* Toohello Jenkins 대시보드를 다시 이동 합니다.
* 만든 마우스 오른쪽 단추로 클릭 hello 새 작업을 클릭 한 다음 **이제 빌드**합니다. 빌드가 시작됩니다. 
* Hello 빌드가 완료 되 면 너무 이동**콘솔 출력이**합니다. Hello 빌드가 Azure에서 원격으로 수행 되었는지 확인할 수 있습니다.

![콘솔 출력](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a>참조

* Azure Friday 비디오: [Azure VM 에이전트를 사용하여 Jenkins와 연속 통합](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)(영문)
* 지원 정보 및 구성 옵션: [Azure VM 에이전트 Jenkins 플러그 인 Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin) 


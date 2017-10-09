---
title: "가상 컴퓨터 클러스터로 aaaMATLAB | Microsoft Docs"
description: "Microsoft Azure 가상 컴퓨터 toocreate MATLAB Distributed Computing Server 클러스터 toorun 계산 집약적인 병렬 MATLAB 작업 사용"
services: virtual-machines-windows
documentationcenter: 
author: mscurrell
manager: timlt
editor: 
ms.assetid: e9980ce9-124a-41f1-b9ec-f444c8ea5c72
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Windows
ms.workload: infrastructure-services
ms.date: 05/09/2016
ms.author: markscu
ms.openlocfilehash: 266749dbdcfefac42c94b74aa612bfee18075a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-matlab-distributed-computing-server-clusters-on-azure-vms"></a>Azure VM에 MATLAB 분산 컴퓨팅 서버 클러스터 만들기
사용 하 여 Microsoft Azure 가상 컴퓨터 하나 toocreate 하거나 더 많은 MATLAB Distributed Computing Server 클러스터 toorun 계산 집약적인 병렬 MATLAB 작업 합니다. 에 기본 이미지로 VM toouse MATLAB Distributed Computing Server 소프트웨어를 설치 하 고 Azure 빠른 시작 템플릿 또는 Azure PowerShell 스크립트 사용 (에서 사용할 수 있는 [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster)) toodeploy hello 클러스터를 관리 하 고 있습니다. 배포 후 toohello 클러스터 toorun 작업 연결 합니다.

## <a name="about-matlab-and-matlab-distributed-computing-server"></a>MATLAB 및 MATLAB 분산 컴퓨팅 서버 정보
hello [MATLAB](http://www.mathworks.com/products/matlab/) 플랫폼 엔지니어링 및 과학 문제를 해결 하기 위해 최적화 됩니다. 대규모 시뮬레이션 및 데이터 처리 태스크에 MATLAB 사용자 MathWorks 병렬 계산 클러스터 및 눈금 서비스 이용 하 여 제품 toospeed의 계산 집약적인 작업을 컴퓨팅을 사용할 수 있습니다. [병렬 컴퓨팅 도구 상자](http://www.mathworks.com/products/parallel-computing/) 는 MATLAB 사용자가 응용 프로그램을 병렬화하여 멀티 코어 프로세서, GPU 및 계산 클러스터의 이점을 활용할 수 있도록 합니다. [MATLAB Distributed Computing Server](http://www.mathworks.com/products/distriben/) MATLAB 사용자 tooutilize 계산 클러스터에서 많은 컴퓨터를 사용 합니다.

Azure 가상 컴퓨터를 사용 하 여 모든 MATLAB Distributed Computing Server 클러스터를 만들 수 있습니다 hello 온-프레미스 클러스터와 같은 대화형 작업, 일괄 처리 작업, 독립적인 작업으로 동일한 메커니즘이 사용 가능한 toosubmit 병렬 작업 및 작업을 통신 합니다. Hello MATLAB 플랫폼와 함께에서 Azure를 사용 하 여 많은 보다 나은 점은 tooprovisioning 개이고 기존 사용 하 여 온-프레미스 하드웨어: 가상 컴퓨터의 범위 크기, 클러스터에서 요청을 사용 하는 hello 계산 리소스에 대해서만 비용을 지불 하므로 생성 하 고 hello 배율로 tootest 모델의 기능입니다.  

## <a name="prerequisites"></a>필수 조건
* **클라이언트 컴퓨터** -Azure 및 hello MATLAB Distributed Computing Server 클러스터는 Windows 기반 클라이언트 컴퓨터 toocommunicate 배포 후 필요 합니다.
* **Azure PowerShell** -참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) tooinstall 클라이언트 컴퓨터에 해당 합니다.
* **Azure 구독** - 구독이 없는 경우 몇 분 만에 [무료 계정](https://azure.microsoft.com/free/) 을 만들 수 있습니다. 대규모 클러스터의 경우, 종량제 구독이나 다른 구매 옵션을 고려하세요.
* **코어 할당량** -대규모 클러스터 또는 둘 이상의 MATLAB Distributed Computing Server 클러스터 tooincrease hello 코어 할당량 toodeploy 할 수 있습니다. 할당량 tooincrease [온라인 고객 지원 요청을 개시](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) 비용 없이 합니다.
* **MATLAB, 병렬 컴퓨팅 도구 상자 및 MATLAB Distributed Computing Server 라이선스** -hello 스크립트에서는 해당 hello 가정 [라이선스 관리자를 호스트 하는 MathWorks](http://www.mathworks.com/products/parallel-computing/mathworks-hosted-license-manager/) 모든 라이선스가 사용 됩니다.  
* **MATLAB Distributed Computing Server 소프트웨어** -hello 클러스터 Vm에 대 한 hello 기본 VM 이미지로 사용할 수 있는 VM에 설치 됩니다.

## <a name="high-level-steps"></a>대략적인 단계
toouse Azure 가상 컴퓨터 여 MATLAB Distributed Computing Server 클러스터에 대 한 hello 다음과 같은 개략적인 단계를 수행 해야 합니다. 자세한 지침은 hello 퀵 스타트 서식 파일 및 스크립트에 포함 된 hello 설명서에 있는 [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster)합니다.

1. **기본 VM 이미지 만들기**  

   * MATLAB 분산 컴퓨팅 서버 소프트웨어를 VM에 다운로드하여 설치합니다.

     > [!NOTE]
     > 이 프로세스에는 2 시간을 걸릴 수 있지만 toodo를 하나만 사용 하면 MATLAB의 각 버전에 대 한 것입니다.   
     >
     >
2. **하나 이상의 클러스터 만들기**  

   * Hello 제공 된 PowerShell 스크립트를 사용 하거나 hello 퀵 스타트 템플릿 toocreate hello 기본 VM 이미지에서 클러스터를 사용 합니다.   
   * Toolist, 일시 중지, 재시작, 및 delete 클러스터 수 있는 PowerShell 스크립트를 제공 하는 hello를 사용 하 여 hello 클러스터를 관리 합니다.

## <a name="cluster-configurations"></a>클러스터 구성
현재 hello 클러스터 만들기 스크립트 및 템플릿을 사용 하면 단일 MATLAB Distributed Computing Server 토폴로지 toocreate 있습니다. 원한다면, 하나 이상의 클러스터를 추가적으로 만들고, 각 클러스터마다 작업자 VM의 수를 다르게 지정하고, 다른 VM 크기를 사용하는 등의 작업이 가능합니다.

### <a name="matlab-client-and-cluster-in-azure"></a>Azure의 MATLAB 클라이언트 및 클러스터
hello MATLAB 클라이언트 노드, MATLAB 작업 스케줄러 노드 및 MATLAB Distributed Computing Server "작업자" 노드는 모든 구성 된 Azure Vm에 가상 네트워크 hello 다음과 같이 그림입니다.


* toouse hello 클러스터의 경우 원격 데스크톱 toohello 클라이언트 노드에 연결 합니다. hello 클라이언트 노드는 hello MATLAB 클라이언트를 실행합니다.
* hello 클라이언트 노드는 모든 작업자에서 액세스할 수 있는 파일 공유 합니다.
* 라이선스 관리자를 호스트 하는 MathWorks 모든 MATLAB 소프트웨어에 대 한 hello 라이선스 확인에 사용 됩니다.
* 기본적으로 코어 당 하나의 MATLAB Distributed Computing Server 작업자 hello 작업자 Vm에서 만들어지지만 숫자를 지정할 수 있습니다.

## <a name="use-an-azure-based-cluster"></a>Azure 기반 클러스터 사용
다른 유형의 MATLAB Distributed Computing Server 클러스터와 마찬가지로 hello MATLAB (hello 클라이언트 VM)에 클라이언트 toocreate MATLAB 작업 스케줄러 클러스터 프로필에에서 대 한 클러스터 프로필 관리자 toouse hello를 해야 합니다.

![클러스터 프로필 관리자](./media/matlab-mdcs-cluster/cluster_profile_manager.png)

## <a name="next-steps"></a>다음 단계
* 자세한 지침은 toodeploy에 대 한 Azure에서 MATLAB Distributed Computing Server 클러스터를 관리 하 고 hello를 참조 하십시오 [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster) hello 서식 파일 및 스크립트를 포함 하는 저장소입니다.
* Toohello 이동 [MathWorks 사이트](http://www.mathworks.com/) MATLAB과 MATLAB Distributed Computing Server에 대 한 자세한 설명서에 대 한 합니다.

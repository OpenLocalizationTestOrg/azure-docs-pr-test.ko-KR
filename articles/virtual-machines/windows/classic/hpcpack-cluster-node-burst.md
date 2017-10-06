---
title: "aaaAdd 버스트 노드 tooan HPC Pack 클러스터 | Microsoft Docs"
description: "Tooexpand HPC Pack 요청 시 Azure에서 클라우드 서비스에서 실행 되는 작업자 역할 인스턴스를 추가 하 여 클러스터링 하는 방법에 대해 알아봅니다"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 24b79a8a-24ad-4002-ae76-75abc9b28c83
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 7ec40ffe76485742c9e458ec49e11805990974e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-on-demand-burst-nodes-tooan-hpc-pack-cluster-in-azure"></a>Azure의 주문형 "전환" 노드 tooan HPC Pack 클러스터를 추가 합니다.
설정 하는 경우는 [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) 클러스터에 Azure를 위 또는 아래로 tooquickly 눈금 hello 클러스터 용량 집합을 유지 하지 않고 미리 구성 된 계산 노드 Vm 하는 방법을 수도 있습니다. 이 문서에서는 어떻게 주문형 tooadd "전환" 노드 (클라우드 서비스에서 실행 중인 작업자 역할 인스턴스)로 계산 리소스 tooa Azure에서 헤드 노드에 있습니다. 

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

![버스트 노드][burst]

이 문서의 단계 hello Azure 노드를 신속 하 게 추가 하는 데 도움이 tooa 클라우드 기반 HPC Pack 헤드 노드 VM 테스트 또는 개념 증명 배포에 대 한 합니다. hello 대략적인 단계는 hello tooadd 클라우드 계산 용량 tooan 온-프레미스 HPC Pack 클러스터 hello 단계 너무 "전환" tooAzure 동일 합니다. 자습서를 보려면 [Microsoft HPC 팩을 사용하여 하이브리드 계산 클러스터 설정](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)을 참조하세요. 자세한 지침 및 프로덕션 배포에 대 한 고려 사항에 대 한 참조 [Microsoft HPC Pack을 사용한 tooAzure 버스트](https://technet.microsoft.com/library/gg481749.aspx)합니다.

## <a name="prerequisites"></a>필수 조건
* **Azure VM에 배포된 HPC Pack 헤드 노드** - 독립 실행형 헤드 노드 VM 또는 더 큰 클러스터의 일부인 VM을 사용할 수 있습니다. 독립 실행형 헤드 노드 toocreate 참조 [Azure VM에서 HPC Pack 헤드 노드 배포](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 자동화 된 HPC 팩 클러스터 배포 옵션에 대 한 참조 [toocreate 옵션 및 Microsoft HPC Pack을 사용 하 여 Azure에서 Windows HPC 클러스터를 관리할](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
  
  > [!TIP]
  > Hello를 사용 하는 경우 [HPC Pack IaaS 배포 스크립트](hpcpack-cluster-powershell-script.md) toocreate hello Azure에서 클러스터의 경우 자동화 된 배포에 Azure 버스트 노드를 포함할 수 있습니다. 해당 아티클에 있는 hello 예를 참조 하십시오.
  > 
  > 
* **Azure 구독** -Azure tooadd 선택할 수 노드를 동일한 사용 되는 구독 toodeploy hello 헤드 노드 VM 또는 다른 구독 (또는 구독) hello 합니다.
* **코어 할당량** -toodeploy 멀티 코어 크기에 따라 여러 Azure 노드를 선택 하는 경우에 특히 tooincrease hello 할당량의 코어를 할 수 있습니다. 할당량 tooincrease [온라인 고객 지원 요청을 개시](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) 비용 없이 합니다.

## <a name="step-1-create-a-cloud-service-and-a-storage-account-for-hello-azure-nodes"></a>1 단계: 클라우드 서비스 및 hello에 대 한 저장소 계정을 Azure 노드 만들기
Azure 클래식 포털 hello 또는 다음 리소스를 필요한 toodeploy 상응 하는 도구 tooconfigure hello Azure 노드를 사용 합니다.

* 새 Azure 클라우드 서비스
* 새 Azure 저장소 계정

> [!NOTE]
> 구독에서 기존 클라우드 서비스를 다시 사용하지 마세요. 
> 
> 

**고려 사항**

* 각 Azure 노드 템플릿 toocreate 계획에 대 한 별도 클라우드 서비스를 구성 합니다. 사용할 수 있습니다 hello 여러 노드 템플릿에 동일한 저장소 계정입니다.
* Hello 클라우드 서비스 및 hello 배포에 사용할 저장소 계정을 hello hello에서 찾는 것이 좋습니다 동일한 Azure 지역에 있습니다.

## <a name="step-2-configure-an-azure-management-certificate"></a>2단계: Azure 관리 인증서 구성
tooadd Azure 노드를 계산 리소스를 toohello hello 배포에 사용 되는 Azure 구독에 인증서를 해당 hello 헤드 노드 및 업로드에 관리 인증서가 필요 합니다.

이 시나리오에 대 한 hello를 선택할 수 있습니다 **기본 HPC Azure 관리 인증서** HPC Pack을 설치 하 고 헤드 노드에서 자동으로 구성 합니다. 이 인증서는 테스트 목적 및 개념 증명 배포에 사용됩니다. toouse 인증서이 hello 헤드 노드 VM toothe 구독에서에서 파일 C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer 업로드 합니다. hello에 tooupload hello 인증서 [Azure 클래식 포털](https://manage.windowsazure.com), 클릭 **설정** > **관리 인증서**합니다.

추가 옵션 tooconfigure hello 관리 인증서에 대 한 참조 [시나리오 tooConfigure hello Azure 버스트 배포용 Azure 관리 인증서](http://technet.microsoft.com/library/gg481759.aspx)합니다.

## <a name="step-3-deploy-azure-nodes-toohello-cluster"></a>3 단계: Azure 노드 toohello 클러스터 배포
단계 tooadd hello 및 Azure를 시작 합니다. 온-프레미스 헤드 노드를 사용 하 여 hello 단계와 동일를이 시나리오에서는 노드는 hello 일반적으로 합니다. 자세한 내용은 다음 섹션에는 hello 참조 [tooDeploy Microsoft HPC Pack을 사용한 Azure 노드 단계](https://technet.microsoft.com/library/gg481758.aspx):

* Azure 노드 템플릿 만들기
* Azure 노드 toohello Windows HPC 클러스터를 추가 합니다.
* 시작 (프로 비전) hello Azure 노드

추가 하 고 hello 노드를 시작 하면 toouse toorun 클러스터 작업 상태가 됩니다.

Azure 노드를 배포할 때 문제가 발생할 경우 [Microsoft HPC Pack을 사용하여 Azure 노드 배포 시 문제 해결](http://technet.microsoft.com/library/jj159097.aspx)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* hello에 대 한 계산 집약적인 인스턴스 크기 toouse 버스트 노드의 hello 고려 사항을 참조 [VM 크기를 계산 하는 고성능](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
* 컴퓨팅 리소스 hello 클러스터 워크 로드에 따라 Azure hello, 참조를 자동으로 확대 하거나 축소 하려면 [자동으로 증가 하 고 HPC Pack 클러스터에서 Azure 계산 리소스를 축소](hpcpack-cluster-node-autogrowshrink.md)합니다.

<!--Image references-->
[burst]: ./media/hpcpack-cluster-node-burst/burst.png

---
title: "HPC 및 일괄 처리에 대 한 Azure 클라우드 hello에 aaaResources | Microsoft Docs"
description: "대규모 병렬, 일괄 처리 및 고성능 컴퓨팅 Azure에서 (HPC) 작업을 실행 하는 기술 리소스 toohelp를 나열 합니다."
services: batch, cloud-services, virtual-machines
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 6f8be911-c841-41ae-88d3-3bcfc029eb7f
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 03/17/2017
ms.author: danlep
ms.openlocfilehash: ab8ba24678bd7ec090306b501d29ca63c4fb83ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a>Azure에서의 큰 계산: 배치 및 고성능 컴퓨팅에 대한 기술 리소스
Azure에서 대규모 병렬, 일괄 처리 및 HPC ()를 계산 하는 고성능 워크 로드를 실행 하는 가이드 tootechnical 리소스 toohelp입니다. 기존 일괄 처리 또는 HPC 작업 toohello Azure 클라우드 늘리거나 한 Azure 서비스를 사용 하 여 새 큰 계산 솔루션을 빌드하십시오.

## <a name="solutions-options"></a>솔루션 옵션
Azure의 큰 계산 옵션에 대 한 확인 하 고 hello 적합 한 접근 방식을 작업 및 비즈니스 요구 사항에 대 한 선택 키를 누릅니다.

* [배치 및 HPC 솔루션](batch-hpc-solutions.md)
* [비디오: Azure 및 HPC hello 클라우드에서 큰 계산](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a>Azure 배치
[일괄 처리](https://azure.microsoft.com/services/batch/) 는 Linux 및 Windows 응용 프로그램 및 실행된 작업을 설정 하 고 클러스터 및 작업 스케줄러를 관리 하지 않고 쉽게 toocloud 사용 하는 플랫폼 서비스입니다. Azure 일괄 처리와 hello SDK toointegrate 클라이언트 응용 프로그램을 사용 하 여 다양 한 언어, 단계 데이터 tooAzure 통해 및 파이프라인을 실행 하는 작업입니다.

* [설명서](https://azure.microsoft.com/documentation/services/batch/)
* [.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/) 및 [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API 참조
* [배치 관리 .NET 라이브러리](https://msdn.microsoft.com/library/mt463120.aspx) 참조
* 자습서: [.NET용 Azure 배치 라이브러리](batch-dotnet-get-started.md) 및 [배치 Python 클라이언트](batch-python-tutorial.md) 시작하기
* [배치 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [배치 비디오](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a>HPC 클러스터 솔루션
배포 또는 사용자 기존 Windows 또는 Linux HPC 클러스터 tooAzure toorun 계산 집약적인 작업을 확장 합니다.  

### <a name="microsoft-hpc-pack"></a>Microsoft HPC 팩
HPC Pack은 Microsoft Azure 및 Windows Server 기술로 구축된 무료 HPC 솔루션으로, Windows와 Linux HPC 작업을 모두 실행할 수 있습니다.  

* [HPC Pack 2016 R2 다운로드](https://www.microsoft.com/download/details.aspx?id=54507)
* [HPC 팩 2012 R2 업데이트 3 다운로드(영문)](https://www.microsoft.com/download/details.aspx?id=49922)
* [설명서](https://technet.microsoft.com/library/jj899572.aspx)
* Azure의 HPC Pack 클러스터 옵션: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 및 [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 
* [HPC Pack을 사용한 tooAzure 작업자 인스턴스 버스트](https://technet.microsoft.com/library/gg481749.aspx)
* [버스트 tooAzure HPC Pack을 사용한 일괄 처리](https://technet.microsoft.com/library/mt612877.aspx)
* [Windows HPC 포럼](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a>Linux 및 OSS 클러스터 솔루션
이러한 Azure 템플릿 toodeploy Linux HPC 클러스터를 사용 합니다.

* [SLURM 클러스터 스핀업](https://azure.microsoft.com/documentation/templates/slurm/) 및 [블로그 게시물](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)
* [토크 클러스터 스핀업](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [PBS Professional을 사용한 계산 그리드 템플릿](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a>HPC 저장소
* [Azure의 HPC 저장소를 위한 병렬 파일 시스템](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [Lustre 소프트웨어용 Intel 클라우드 버전 - Eval](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [CentOS 7.2 템플릿의 BeeGFS](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a>Microsoft MPI
[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) hello 메시지 전달 인터페이스 표준을 개발 하 고 hello Windows 플랫폼에서 실행 중인 병렬 응용 프로그램의 Microsoft 구현입니다.

* [MS-MPI 다운로드](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [MS-MPI 참조(영문)](https://msdn.microsoft.com/library/dn473458.aspx)
* [MPI 포럼](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a>계산 집약적 인스턴스
Azure 제안의 [VM의 범위 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 포함 하 여 [계산 집약적인 H 시리즈](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 인스턴스 tooa 백 엔드 RDMA 네트워크 toorun Linux 및 Windows HPC 작업을 연결할 수 있습니다. 

* [Linux RDMA 클러스터 toorun MPI 응용 프로그램 설정](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Microsoft HPC Pack toorun MPI 응용 프로그램을 사용 하 여 Windows RDMA 클러스터 설정](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

GPU가 많이 사용되는 워크로드의 경우 [NC 및 NV 크기](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/)를 참조하세요.

## <a name="samples-and-demos"></a>샘플 및 데모
* [Azure 배치 C# 및 Python 코드 샘플](https://github.com/Azure/azure-batch-samples)
* [대형 조선소 일괄 처리](https://azure.github.io/batch-shipyard/) 일괄 처리 스타일 Dockerized 작업 tooAzure 일괄 처리의 간편한 배포를 위해 도구 키트
* Azure Batch를 기반으로 구축된 [doAzureParallel](http://www.github.com/Azure/doAzureParallel) R 패키지
* [HPC용 SUSE Linux Enterprise Server 시험 사용](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a>관련 Azure 서비스
* [데이터 팩터리](https://azure.microsoft.com/documentation/services/data-factory/)
* [기계 학습](https://azure.microsoft.com/documentation/services/machine-learning/)
* [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)
* [가상 컴퓨터](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [가상 컴퓨터 확장 집합](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [클라우드 서비스](https://azure.microsoft.com/documentation/services/cloud-services/)
* [앱 서비스](https://azure.microsoft.com/documentation/services/app-service/)
* [미디어 서비스](https://azure.microsoft.com/documentation/services/media-services/)
* [함수](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a>아키텍처 청사진
* [Azure Batch 및 Azure Data Factory를 사용하여 HPC 및 데이터 오케스트레이션](http://go.microsoft.com/fwlink/?linkid=717686)(PDF) 및 [문서](../data-factory/data-factory-data-processing-using-batch.md)

## <a name="industry-solutions"></a>업계 솔루션
* [뱅킹 및 자금 시장](https://finance.azure.com/)
* [엔지니어링 시뮬레이션](https://simulation.azure.com/) 

## <a name="customer-stories"></a>고객 사례
* [ANEO](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [d3View](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [Ludwig Institute of Cancer Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [Microsoft Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [Milliman](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [Mitsubishi UFJ Securities International](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [Schlumberger](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [UberCloud](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a>다음 단계
* 에 대 한 hello 최신 알림을 참조 hello [Microsoft HPC 및 일괄 처리 팀 블로그](http://blogs.technet.com/b/windowshpc/) 및 hello [Azure 블로그](https://azure.microsoft.com/blog/tag/hpc/)합니다.
* 또한 참조 [일괄 처리의 새로운 기능](https://azure.microsoft.com/updates/?service=batch) toohello 구독 또는 [RSS 피드](https://azure.microsoft.com/updates/feed/?service=batch)합니다.


---
title: "서비스 패브릭 이미지 저장소 연결 문자열 aaaAzure | Microsoft Docs"
description: "Hello 이미지 저장소 연결 문자열을 이해"
services: service-fabric
documentationcenter: .net
author: alexwun
manager: timlt
editor: 
ms.assetid: 00f8059d-9d53-4cb8-b44a-b25149de3030
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: alexwun
ms.openlocfilehash: 83f5ad75b5df07726997da3173722028255b8cae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-imagestoreconnectionstring-setting"></a>Hello ImageStoreConnectionString 설정 이해

설명서의 일부 간략하게 언급 hello 존재 "ImageStoreConnectionString" 매개 변수의 의미를 설명 하지 않고 합니다. 와 같은 문서가 완료 된 후 [PowerShell을 사용 하 여 배포 및 제거 응용 프로그램][10], 하기만 하면 같이 hello 대상의 hello 클러스터 매니페스트에 표시 된 대로 복사/붙여넣기 hello 값은 클러스터입니다. 클러스터당 구성 가능한 hello 설정할 수 있지만 hello 통해 클러스터를 만들 때 [Azure 포털][11], 없습니다 옵션 tooconfigure이 설정 및 해당 항상 "fabric: ImageStore"는 합니다. 이 설정은 다음의 hello 목적은 이란?

![클러스터 매니페스트][img_cm]

서비스 패브릭 내부 Microsoft 소비 하기 위한 플랫폼으로 의해 시작 많은 다양 한 팀의 일부 측면은 고도로 사용자 지정 가능한-hello "Image Store"는 이러한 한 가지 측면인 하므로 있습니다. 기본적으로, hello 이미지 저장소는 응용 프로그램 패키지를 저장 하기 위한 플러그형 리포지토리입니다. Hello 클러스터의 노드에 배포 된 tooa 응용 프로그램을 사용 하는 경우 해당 노드는 응용 프로그램 패키지의 hello 내용을 hello 이미지 저장소에서에서 다운로드 합니다. hello ImageStoreConnectionString은 클라이언트와 노드 toofind hello 올바른 이미지 저장소에 지정된 된 클러스터에 대 한 모든 hello 필요한 정보를 포함 하는 설정입니다.

현재 세 가지 종류의 가능한 이미지 저장소 공급자가 있고 해당하는 연결 문자열은 다음과 같습니다.

1. 이미지 저장소 서비스: "fabric:ImageStore"

2. 파일 시스템: "file:[file system path]"

3. Azure Storage: "xstore:DefaultEndpointsProtocol=https;AccountName=[...];AccountKey=[...];Container=[...]"

프로덕션 환경에서 사용 하는 hello 공급자 유형은 hello 이미지 저장소 서비스를 상태 저장 지속형된 시스템 서비스는 서비스 패브릭 탐색기에서 볼 수 있습니다. 

![이미지 저장소 서비스][img_is]

Hello 패키지 저장소에 대 한 외부 종속성을 제거 하 고 hello 집약성이 저장소를 보다 상세하게 제공 하는 hello 클러스터 자체 내에서 시스템 서비스에서 호스팅 hello 이미지 저장소. Hello 이미지 저장소 주위 향후 개선 사항도 하지 않은 경우 단독으로 가능성이 tootarget hello 이미지 저장소 공급자를 먼저는 합니다. hello 이미지 저장소 서비스 공급자에 대 한 연결 문자열 hello hello 클라이언트는 이미 연결 된 toohello 대상 클러스터 고유 정보가 되어 있지 않습니다. 클라이언트 hello는 hello 시스템 서비스를 대상으로 하는 프로토콜을 사용 해야 함을 tooknow만 필요 합니다.

hello 파일 시스템 공급자 대신 사용 됩니다 hello 이미지 저장소 서비스가 로컬 하나 상자 클러스터에 대 한 개발 toobootstrap hello 클러스터 하는 동안 약간 더 빠르게. hello 차이점은 일반적으로 짧지만 이지만 개발 하는 동안 대부분 사람들에 대 한 유용한 최적화 합니다. 가능한 toodeploy 인 클러스터를 로컬 하나 상자도 다른 저장소 공급자 유형을 hello 하지만 없는 이유는 일반적으로 toodo 하므로 hello 개발/테스트 워크플로 하 게 유지 되므로 hello 동일한 공급자에 관계 없이 합니다. 이 사용법 이외의 hello Azure 저장소 및 파일 시스템 공급자만 레거시 지원에 존재합니다.

따라서 hello ImageStoreConnectionString 구성 가능한 이지만, 일반적으로 방금 hello 기본 설정을 사용 합니다. TooAzure를 통해 게시할 때 [Visual Studio][12], hello 매개 변수는 자동으로 설정 하면 적절 하 게 합니다. Azure에서 호스트 되는 프로그래밍 방식 배포를 tooclusters, hello 연결 문자열은 항상 "fabric: ImageStore"입니다. 의문이 있는 경우 해당 값 항상 확인할 수 있습니다 하 여 hello 클러스터 매니페스트를 검색 하 여 있지만 [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx), 또는 [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest)합니다. 온-프레미스 테스트 및 프로덕션 클러스터에서 구성 된 toouse hello 이미지 저장소 서비스 공급자도 항상 있어야 합니다.

### <a name="next-steps"></a>다음 단계
[PowerShell을 사용하여 응용 프로그램 배포 및 제거][10]

<!--Image references-->
[img_is]: ./media/service-fabric-image-store-connection-string/image_store_service.png
[img_cm]: ./media/service-fabric-image-store-connection-string/cluster_manifest.png

[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-cluster-creation-via-portal.md
[12]: service-fabric-publish-app-remote-cluster.md

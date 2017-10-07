---
title: "Azure CLI 2.0을 사용 하 여 aaaManage Azure 서비스 패브릭 응용 프로그램"
description: "Azure CLI 2.0을 사용 하 여 Azure 서비스 패브릭에서 toodeploy 및 제거 하는 응용 프로그램을 클러스터링 하는 방법을 알아봅니다."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ae1ba19513978b0f95ffb65d5f1f7a21ed5f2894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a>Azure CLI 2.0을 사용하여 Azure Service Fabric 응용 프로그램 관리

자세한 내용은 방법 Azure 서비스 패브릭 클러스터에서 실행 되는 toocreate 및 delete 응용 프로그램입니다.

## <a name="prerequisites"></a>필수 조건

* Azure CLI 2.0을 설치합니다. 그런 다음, Service Fabric 클러스터를 선택합니다. 자세한 내용은 [Azure CLI 2.0 시작](service-fabric-azure-cli-2-0.md)을 참조하세요.

* 서비스 패브릭 응용 프로그램 패키지 준비 toobe를 배포 했습니다. 방법에 대 한 자세한 내용은 tooauthor 및 응용 프로그램 패키지에 대해 알아보세요 hello [서비스 패브릭 응용 프로그램 모델](service-fabric-application-model.md)합니다.

## <a name="overview"></a>개요

toodeploy 새 응용 프로그램을 다음이 단계를 완료 합니다.

1. 응용 프로그램 패키지 toohello 서비스 패브릭 이미지 저장소를 업로드 합니다.
2. 응용 프로그램 유형을 프로비전합니다.
3. 응용 프로그램을 지정하고 만듭니다.
4. 서비스를 지정하고 만듭니다.

tooremove 기존 응용 프로그램에 다음이 단계를 완료 합니다.

1. Hello 응용 프로그램을 삭제 합니다.
2. 해제 hello 응용 프로그램 종류를 연결 합니다.
3. Hello 이미지 저장소 콘텐츠를 삭제 합니다.

## <a name="deploy-a-new-application"></a>새 응용 프로그램 배포

toodeploy 새 응용 프로그램을 완전 hello 작업을 수행 합니다.

### <a name="upload-a-new-application-package-toohello-image-store"></a>새 응용 프로그램 패키지 toohello 이미지 저장소에 업로드

응용 프로그램을 만들기 전에 hello 응용 프로그램 패키지 toohello 서비스 패브릭 이미지 저장소를 업로드 합니다. 

예를 들어, 응용 프로그램 패키지 hello에 있으면 `app_package_dir` 디렉터리를 사용 하 여 hello 다음 명령을 tooupload hello 디렉터리:

```azurecli
az sf application upload --path ~/app_package_dir
```

대형 응용 프로그램 패키지에 대 한 hello를 지정할 수 있습니다 `--show-progress` hello 업로드의 toodisplay hello 진행률 옵션입니다.

### <a name="provision-hello-application-type"></a>프로 비전 hello 응용 프로그램 종류

Hello 업로드가 완료 되 면 hello 응용 프로그램을 프로 비전 합니다. tooprovision hello 응용 프로그램, 다음 명령을 사용 하 여 hello:

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

값에 대 한 hello `application-type-build-path` hello 응용 프로그램 패키지의 업로드 위치 hello 디렉터리 이름입니다.

### <a name="create-an-application-from-an-application-type"></a>응용 프로그램 유형에서 응용 프로그램 만들기

Hello 응용 프로그램을 프로 비전 한 후 사용 하 여 hello 다음 tooname 명령 하 고 응용 프로그램을 만듭니다.

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name`hello 응용 프로그램 인스턴스에 대해 toouse 되도록 hello 이름이입니다. Hello 이전에 프로 비전 된 응용 프로그램 매니페스트에서 추가 매개 변수를 얻을 수 있습니다.

hello 응용 프로그램 이름은 hello 접두사로 시작 `fabric:/`합니다.

### <a name="create-services-for-hello-new-application"></a>Hello 새 응용 프로그램에 대 한 서비스 만들기

응용 프로그램을 만든 후 hello 응용 프로그램에서 서비스를 만듭니다. 다음 예제는 hello, 응용 프로그램에서 새 상태 비저장 서비스를 만듭니다. 응용 프로그램을 만들 수 있는 hello 서비스는 서비스 매니페스트의 hello 이전에 프로 비전 된 응용 프로그램 패키지에 정의 됩니다.

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>응용 프로그램 배포 및 상태 확인

응용 프로그램 및 서비스가 성공적으로 배포 되었는지, tooverify hello 응용 프로그램 및 서비스가 나열 되어 있는지 확인 합니다.

```azurecli
az sf application list
az sf service list --application-list TestApp
```

hello 서비스가 정상 임을 tooverify hello 서비스와 hello 응용 프로그램의 유사한 명령 tooretrieve hello 상태를 사용 합니다.

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

정상 서비스 및 응용 프로그램은 `HealthState` 값이 `Ok`입니다.

## <a name="remove-an-existing-application"></a>기존 응용 프로그램 제거

tooremove 응용 프로그램 전체 hello 작업을 수행 합니다.

### <a name="delete-hello-application"></a>Hello 응용 프로그램 삭제

toodelete hello 응용 프로그램, 다음 명령을 사용 하 여 hello:

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a>응용 프로그램 종류 hello를 프로 비전 해제

Hello 응용 프로그램을 삭제 하면 응용 프로그램 종류 hello를 프로 비전 해제 필요 없는 경우 수 없습니다. toounprovision hello 응용 프로그램 종류, 다음 명령을 사용 하 여 hello:

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

hello 이름과 hello 이전에 프로 비전 된 응용 프로그램 매니페스트에서 버전 hello 형식 이름 및 형식 버전이 일치 해야 합니다.

### <a name="delete-hello-application-package"></a>Hello 응용 프로그램 패키지를 삭제 합니다.

응용 프로그램 종류 hello를 프로 비전 해제가, 후에 필요 없는 경우 hello 이미지 저장소에서 hello 응용 프로그램 패키지를 삭제할 수 없습니다. 응용 프로그램 패키지를 삭제하면 디스크 공간을 확보하는 데 도움이 됩니다. 

다음 명령을 사용 하 여 hello hello 이미지 저장소에서 toodelete hello 응용 프로그램 패키지:

```azurecli
az sf application package-delete --content-path app_package_dir
```

`content-path`hello 응용 프로그램을 만들 때 업로드 된 hello 디렉터리의 hello 이름 이어야 합니다.

## <a name="related-articles"></a>관련 문서

* [Service Fabric 및 Azure CLI 2.0 시작](service-fabric-azure-cli-2-0.md)
* [Service Fabric XPlat CLI 시작](service-fabric-azure-cli.md)

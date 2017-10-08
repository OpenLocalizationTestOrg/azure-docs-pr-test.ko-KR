---
title: "서비스 패브릭 응용 프로그램 배포 aaaAzure | Microsoft Docs"
description: "Hello FabricClient Api toodeploy 방법과 서비스 패브릭에서 응용 프로그램을 제거 합니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: b2986b71c461f3e785ba16ec1b827fe47ad852fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a>FabricClient를 사용하여 응용 프로그램 배포 및 제거
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [FabricClient API](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

일단 [응용 프로그램 형식이 패키지화되면][10] Azure Service Fabric 클러스터에 배포될 준비가 된 것입니다. 배포에는 세 단계를 수행 하는 hello 포함 됩니다.

1. Hello 응용 프로그램 패키지 toohello 이미지 저장소에 업로드
2. Hello 응용 프로그램 형식 등록
3. Hello 응용 프로그램 인스턴스 만들기

한 후 응용 프로그램이 배포 된 hello 클러스터에서 실행 중인 인스턴스를 hello 응용 프로그램 인스턴스 및 해당 응용 프로그램 종류를 삭제할 수 있습니다. hello 클러스터에서 응용 프로그램 toocompletely 제거 단계를 수행 하는 hello 포함 됩니다.

1. 응용 프로그램 인스턴스를 실행 하는 hello 제거 (또는 삭제)
2. 필요 없는 hello 응용 프로그램 종류를 등록 취소
3. Hello 이미지 저장소에서 hello 응용 프로그램 패키지를 제거 합니다.

사용 하는 경우 [배포 및 응용 프로그램 디버깅에 대 한 Visual Studio](service-fabric-publish-app-remote-cluster.md) 앞의 단계를 hello 모든 로컬 개발 클러스터에는 PowerShell 스크립트를 통해 자동으로 처리 됩니다.  이 스크립트는 hello에서 발견 되 *스크립트* hello 응용 프로그램 프로젝트의 폴더입니다. 이 문서에서는 수행할 수 있도록 해당 스크립트가 수행 하는 작업에 배경 제공 hello Visual Studio 외부에서 이와 동일한 작업을 합니다. 
 
## <a name="connect-toohello-cluster"></a>Toohello 클러스터에 연결
Toohello 클러스터를 생성 하 여 연결 된 [FabricClient](/dotnet/api/system.fabric.fabricclient) 이 문서의 코드 예제는 hello 실행 하기 전에 인스턴스. 원격 클러스터 연결 tooa 로컬 개발 클러스터 또는 클러스터 X509 Azure Active Directory를 사용 하 여 보안의 예제를 보려면 인증서 또는 Windows Active Directory 참조 [연결 tooa 보안 클러스터](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis)합니다. tooconnect toohello 로컬 개발 클러스터 hello 다음 실행:

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a>Hello 응용 프로그램 패키지 업로드
Visual Studio에서 *MyApplication*이라는 응용 프로그램을 빌드하고 패키지한다고 가정해 보겠습니다. 기본적으로 hello 응용 프로그램 유형 이름은 ApplicationManifest.xml hello에 나열 된 "MyApplicationType"는 합니다.  hello hello 필요한 응용 프로그램 매니페스트, 서비스 매니페스트 및 코드/config/데이터 패키지를 포함 하는 응용 프로그램 패키지에 있는 *C:\Users\&lt; username&gt;\Documents\Visual Studio 2017\Projects\ MyApplication\MyApplication\pkg\Debug*합니다.

Hello 응용 프로그램 패키지 업로드 hello 내부 서비스 패브릭 구성 요소에서 액세스할 수 있는 위치에 배치 됩니다. 서비스 패브릭 hello 응용 프로그램 패키지의 hello 등록 하는 동안 hello 응용 프로그램 패키지를 확인합니다. 그러나 tooverify hello 응용 프로그램 패키지를 로컬로 (즉, 업로드 하기 전에) 하려는 경우 사용할 hello [테스트 ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.

hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API hello 응용 프로그램 패키지 toohello 클러스터 이미지 저장소에 업로드 합니다. 

Hello 응용 프로그램 패키지 큰 많은 파일의 경우, 다음을 할 수 있습니다 [압축](service-fabric-package-apps.md#compress-a-package) PowerShell을 사용 하 여 toohello 이미지 저장소를 복사 합니다. hello 압축 hello 크기와 파일 hello 수가 줄어듭니다.

참조 [hello 이미지 저장소 연결 문자열을 이해](service-fabric-image-store-connection-string.md) 보충 정보에 대 한 hello 이미지 저장소 및 이미지 연결 문자열을 저장 합니다.

## <a name="register-hello-application-package"></a>Hello 응용 프로그램 패키지를 등록 합니다.
hello 응용 프로그램 유형 및 버전 hello 응용 프로그램 패키지를 등록 하면 사용 하기 위해 사용할 수 있게 하는 hello 응용 프로그램 매니페스트에 선언 합니다. hello 시스템 hello 이전 단계에서 업로드 된 hello 패키지가, hello 패키지를 확인, hello 패키지 내용 처리 읽고 처리 하는 hello 패키지 tooan 내부 시스템 위치에 복사 합니다.  

hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API 레지스터 hello hello 클러스터에서 응용 프로그램 종류와 배포에 사용할 수 있도록 합니다.

hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API는 모든 성공적으로 등록 된 응용 프로그램 종류에 대 한 정보를 제공 합니다. 이 API toodetermine hello 등록 수행 되는 경우 사용할 수 있습니다.

## <a name="create-an-application-instance"></a>응용 프로그램 인스턴스 만들기
Hello를 사용 하 여 성공적으로 등록 된 모든 응용 프로그램 종류에서 응용 프로그램을 인스턴스화할 수 [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API입니다. 각 응용 프로그램의 hello 이름 hello로 시작 해야 *"패브릭:"* 구성표 및 각 응용 프로그램 인스턴스의 (클러스터) 내에서 고유 해야 합니다. Hello 대상 응용 프로그램 종류의 응용 프로그램 매니페스트 hello에에서 정의 된 기본 서비스 만들어집니다.

등록된 응용 프로그램 형식의 주어진 어떤 버전에 대해서도 여러 개의 응용 프로그램 인스턴스를 만들 수 있습니다. 각 응용 프로그램 인스턴스는 자체 작업 디렉터리 및 프로세스 집합과는 별도로 실행됩니다.

hello를 실행 하는 hello 클러스터에서 실행 하는 응용 프로그램 및 서비스 이라는 toosee [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) 및 [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) Api입니다.

## <a name="create-a-service-instance"></a>서비스 인스턴스 만들기
Hello를 사용 하 여 서비스 유형에 서 서비스를 인스턴스화할 수 [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API입니다.  Hello 서비스 hello 응용 프로그램 매니페스트에서 기본 서비스로 선언 된 경우에 hello 서비스 hello 응용 프로그램 인스턴스화될 때 인스턴스화됩니다.  호출 hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) 인스턴스화된 이미 서비스에 대 한 API FabricException FabricErrorCode.ServiceAlreadyExists 값으로는 오류 코드가 포함 된 형식의 예외를 반환 합니다.

## <a name="remove-a-service-instance"></a>서비스 인스턴스 제거
서비스 인스턴스를 더 이상 필요 하면 hello를 호출 하 여 응용 프로그램 인스턴스를 실행 하는 hello에서 제거할 수 없습니다 [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API입니다.  

> [!WARNING]
> 이 작업은 되돌릴 수 없으며 서비스 상태는 복구할 수 없습니다.

## <a name="remove-an-application-instance"></a>응용 프로그램 인스턴스 제거
응용 프로그램 인스턴스가 필요 하지 않은 경우 제거할 수 없습니다 영구적으로 hello를 사용 하 여 이름 [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API입니다. [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) 도, 영구적으로 모든 서비스 상태를 제거 하는 toohello 응용 프로그램에 포함 된 모든 서비스를 자동으로 제거 합니다.

> [!WARNING]
> 이 작업은 되돌릴 수 없으며 응용 프로그램 상태는 복구할 수 없습니다.

## <a name="unregister-an-application-type"></a>응용 프로그램 유형 등록 취소
특정 버전의 hello를 사용 하 여 hello 응용 프로그램 종류를 등록 취소 해야 응용 프로그램 종류의 특정 버전은 더 이상 필요 없는, [등록 취소 ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API입니다. 응용 프로그램 종류 버전 저장소 공간의 hello 이미지 저장소에서 사용 하는 사용 하지 않는 버전의 등록을 취소 합니다. 응용 프로그램 종류의 버전으로 응용 프로그램이 없습니다. 해당 버전의 hello 응용 프로그램 종류에 대해 인스턴스화되고 없는 보류 중인 응용 프로그램 업그레이드 hello 응용 프로그램 종류의 해당 버전을 참조 하는 등록 취소할 수 있습니다.

## <a name="remove-an-application-package-from-hello-image-store"></a>Hello 이미지 저장소에서 응용 프로그램 패키지를 제거 합니다.
응용 프로그램 패키지를 더 이상 필요 hello를 사용 하 여 시스템 리소스를 hello 이미지 저장소 toofree에서 삭제할 수 [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API입니다.

## <a name="troubleshooting"></a>문제 해결
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a>Copy-ServiceFabricApplicationPackage가 ImageStoreConnectionString을 요청함
서비스 패브릭 SDK 환경 hello hello 기본값을 설정 하 고 올바른 이미 있어야 합니다. 하지만 해당 hello 서비스 패브릭 클러스터를 사용 하 여 모든 명령에 대 한 hello ImageStoreConnectionString 해야 hello 값 필요한 경우 일치 합니다. Hello ImageStoreConnectionString hello 클러스터 매니페스트에서 찾을 수 있습니다 hello를 사용 하 여 검색 [Get ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) 및 Get ImageStoreConnectionStringFromClusterManifest 명령:

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

hello **Get ImageStoreConnectionStringFromClusterManifest** hello 서비스 패브릭 SDK PowerShell 모듈의 일부인 cmdlet을 사용 하는 tooget hello 이미지인 연결 문자열을 저장 합니다.  tooimport hello SDK 모듈을 실행 합니다.

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


hello ImageStoreConnectionString은 hello 클러스터 매니페스트에 있습니다.

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

참조 [hello 이미지 저장소 연결 문자열을 이해](service-fabric-image-store-connection-string.md) 보충 정보에 대 한 hello 이미지 저장소 및 이미지 연결 문자열을 저장 합니다.

### <a name="deploy-large-application-package"></a>대형 응용 프로그램 패키지 배포
문제: 대형 응용 프로그램 패키지(GB 단위)에 대한 [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API 시간이 초과되었습니다.
다음을 시도해 보세요.
- [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) 메서드에 `timeout` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다. 기본적으로 hello 제한 시간 30 분입니다.
- 원본 컴퓨터와 클러스터 간에 hello 네트워크 연결을 확인 합니다. Hello 연결이 느린 경우에 컴퓨터를 사용 하 여 더 나은 네트워크 연결을 사용 하는 것이 좋습니다.
Hello 클라이언트 컴퓨터가 hello 클러스터와 다른 지역에 있는 경우에 hello 클러스터와 가깝거나 동일한 지역에 클라이언트 컴퓨터를 사용 하는 것이 좋습니다.
- 외부 제한에 도달하고 있는지 확인합니다. 예를 들어 hello 이미지 저장소에 구성 된 toouse azure 저장소가, 업로드 제한 될 수 있습니다.

문제: 패키지 업로드가 성공적으로 완료되었지만 [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API 시간이 초과되었습니다. 다음을 시도해 보세요.
- [Hello 패키지를 압축](service-fabric-package-apps.md#compress-a-package) toohello 이미지 저장소를 복사 하기 전에.
hello 압축 hello 크기가 줄어들고에 hello 트래픽 양이 감소 하 고 해당 서비스 패브릭 작업 hello 수의 파일을 수행 해야 합니다. hello 업로드 작업 (특히 포함 하는 경우 hello 압축 시간)에 속도가 느려질 수 있습니다, 하지만 등록 및 등록을 취소할 hello 응용 프로그램 종류는 더 빠릅니다.
- [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API에 `timeout` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다.

### <a name="deploy-application-package-with-many-files"></a>많은 파일이 있는 응용 프로그램 패키지 배포
문제: 많은 파일(1,000개 단위)이 있는 응용 프로그램 패키지에 대한 [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync)가 시간이 초과되었습니다.
다음을 시도해 보세요.
- [Hello 패키지를 압축](service-fabric-package-apps.md#compress-a-package) toohello 이미지 저장소를 복사 하기 전에. hello 압축 hello 파일 수를 줄입니다.
- [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync)에 `timeout` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다.

## <a name="code-example"></a>코드 예제
hello 다음 예제에서는 응용 프로그램 패키지 toohello 이미지 저장소에 복사, 응용 프로그램 종류 hello를 프로 비전, 응용 프로그램 인스턴스, 만들어집니다에서 서비스 인스턴스를 제거 hello 응용 프로그램 인스턴스 취소를 프로 비전 hello 응용 프로그램 종류 및 hello 이미지 저장소에서 hello 응용 프로그램 패키지를 삭제합니다.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect toohello cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy hello application package tooa location in hello image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied too{0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy tooImage Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision hello application.  "MyApplicationV1" is hello folder in hello image store where hello application package is located. 
    // hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) 
    // is now registered in hello cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create hello application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create hello stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create hello service instance.  If hello service is declared as a default service in hello ApplicationManifest.xml,
    // hello service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from hello application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision hello application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete hello application package from a location in hello image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a>다음 단계
[서비스 패브릭 응용 프로그램 업그레이드](service-fabric-application-upgrade.md)

[서비스 패브릭 상태 소개](service-fabric-health-introduction.md)

[서비스 패브릭 서비스 진단 및 문제 해결](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[서비스 패브릭에서 응용 프로그램 모델링](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md

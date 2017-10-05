---
title: "Azure Service Fabric의 신뢰할 수 있는 컬렉션 개체 serialization | Microsoft Docs"
description: "Azure Service Fabric 신뢰할 수 있는 컬렉션 개체 serialization"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 9d35374c-2d75-4856-b776-e59284641956
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/8/2017
ms.author: mcoskun
ms.openlocfilehash: c14794b71ce7340d9e90a56d781c712e247ded06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="1e3b3-103">Azure Service Fabric의 신뢰할 수 있는 컬렉션 개체 serialization</span><span class="sxs-lookup"><span data-stu-id="1e3b3-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="1e3b3-104">신뢰할 수 있는 컬렉션은 해당 항목을 복제하고 유지하여 컴퓨터 장애 및 정전이 발생해도 지속되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-104">Reliable Collections' replicate and persist their items to make sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="1e3b3-105">항목을 복제하고 유지하기 위해 신뢰할 수 있는 컬렉션에서 항목을 직렬화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-105">Both to replicate and to persist items, Reliable Collections' need to serialize them.</span></span>

<span data-ttu-id="1e3b3-106">신뢰할 수 있는 컬렉션은 Reliable State Manager로부터 지정된 형식에 적합한 직렬 변환기를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-106">Reliable Collections' get the appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="1e3b3-107">Reliable State Manager에는 기본 제공 직렬 변환기가 포함되어 있으며, 지정된 형식에 대한 사용자 지정 직렬 변환기를 등록할 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-107">Reliable State Manager contains built-in serializers and allows custom serializers to be registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="1e3b3-108">기본 제공 직렬 변환기</span><span class="sxs-lookup"><span data-stu-id="1e3b3-108">Built-in Serializers</span></span>

<span data-ttu-id="1e3b3-109">Reliable State Manager에는 일부 공용 형식에 대한 기본 제공 직렬 변환기가 포함되어 있으므로 기본적으로 해당 형식을 효율적으로 직렬화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="1e3b3-110">다른 형식의 경우 Reliable State Manager에서 [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-110">For other types, Reliable State Manager falls back to use the [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="1e3b3-111">기본 제공 직렬 변환기는 해당 형식이 변경될 수 없음을 알고 있으며 형식 이름 등의 형식 정보를 포함할 필요가 없으므로 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-111">Built-in serializers are more efficient since they know their types cannot change and they do not need to include information about the type like its type name.</span></span>

<span data-ttu-id="1e3b3-112">Reliable State Manager에는 다음 형식에 대한 기본 제공 직렬 변환기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="1e3b3-113">Guid</span><span class="sxs-lookup"><span data-stu-id="1e3b3-113">Guid</span></span>
- <span data-ttu-id="1e3b3-114">bool</span><span class="sxs-lookup"><span data-stu-id="1e3b3-114">bool</span></span>
- <span data-ttu-id="1e3b3-115">byte</span><span class="sxs-lookup"><span data-stu-id="1e3b3-115">byte</span></span>
- <span data-ttu-id="1e3b3-116">sbyte</span><span class="sxs-lookup"><span data-stu-id="1e3b3-116">sbyte</span></span>
- <span data-ttu-id="1e3b3-117">byte[]</span><span class="sxs-lookup"><span data-stu-id="1e3b3-117">byte[]</span></span>
- <span data-ttu-id="1e3b3-118">char</span><span class="sxs-lookup"><span data-stu-id="1e3b3-118">char</span></span>
- <span data-ttu-id="1e3b3-119">string</span><span class="sxs-lookup"><span data-stu-id="1e3b3-119">string</span></span>
- <span data-ttu-id="1e3b3-120">decimal</span><span class="sxs-lookup"><span data-stu-id="1e3b3-120">decimal</span></span>
- <span data-ttu-id="1e3b3-121">double</span><span class="sxs-lookup"><span data-stu-id="1e3b3-121">double</span></span>
- <span data-ttu-id="1e3b3-122">float</span><span class="sxs-lookup"><span data-stu-id="1e3b3-122">float</span></span>
- <span data-ttu-id="1e3b3-123">int</span><span class="sxs-lookup"><span data-stu-id="1e3b3-123">int</span></span>
- <span data-ttu-id="1e3b3-124">uint</span><span class="sxs-lookup"><span data-stu-id="1e3b3-124">uint</span></span>
- <span data-ttu-id="1e3b3-125">long</span><span class="sxs-lookup"><span data-stu-id="1e3b3-125">long</span></span>
- <span data-ttu-id="1e3b3-126">ulong</span><span class="sxs-lookup"><span data-stu-id="1e3b3-126">ulong</span></span>
- <span data-ttu-id="1e3b3-127">short</span><span class="sxs-lookup"><span data-stu-id="1e3b3-127">short</span></span>
- <span data-ttu-id="1e3b3-128">ushort</span><span class="sxs-lookup"><span data-stu-id="1e3b3-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="1e3b3-129">사용자 지정 serialization</span><span class="sxs-lookup"><span data-stu-id="1e3b3-129">Custom Serialization</span></span>

<span data-ttu-id="1e3b3-130">사용자 지정 직렬 변환기는 성능 향상이나 네트워크 및 디스크의 데이터 암호화에 주로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-130">Custom serializers are commonly used to increase performance or to encrypt the data over the wire and on disk.</span></span> <span data-ttu-id="1e3b3-131">무엇보다, 사용자 지정 직렬 변환기는 형식 정보를 직렬화해야 할 필요가 없기 때문에 일반적으로 제네릭 직렬 변환기보다 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need to serialize information about the type.</span></span> 

<span data-ttu-id="1e3b3-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__)는 지정된 형식 T에 대한 사용자 지정 직렬 변환기를 등록하는 데 사용됩니다. 이 등록은 StatefulServiceBase 생성 시 수행되어 복구가 시작되기 전에 신뢰할 수 있는 모든 컬렉션이 적절한 직렬 변환기에 액세스하여 영구 데이터를 읽을 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used to register a custom serializer for the given type T. This registration should happen in the construction of the StatefulServiceBase to ensure that before recovery starts, all Reliable Collections have access to the relevant serializer to read their persisted data.</span></span>

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed to set OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> <span data-ttu-id="1e3b3-133">사용자 지정 직렬 변환기가 기본 제공 직렬 변환기보다 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="1e3b3-134">예를 들어 int에 대한 사용자 지정 직렬 변환기를 등록하면 int에 대한 기본 제공 직렬 변환기 대신 이 직렬 변환기가 정수 직렬화에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-134">For example, when a custom serializer for int is registered, it is used to serialize integers instead of the built-in serializer for int.</span></span>

### <a name="how-to-implement-a-custom-serializer"></a><span data-ttu-id="1e3b3-135">사용자 지정 직렬 변환기를 구현하는 방법</span><span class="sxs-lookup"><span data-stu-id="1e3b3-135">How to implement a custom serializer</span></span>

<span data-ttu-id="1e3b3-136">사용자 지정 직렬 변환기는 [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) 인터페이스를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-136">A custom serializer needs to implement the [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="1e3b3-137">IStateSerializer<T>에는 기준 값이라는 추가 T를 사용하는 쓰기 및 읽기 오버로드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="1e3b3-138">이 API는 차등 serialization에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-138">This API is for differential serialization.</span></span> <span data-ttu-id="1e3b3-139">현재 차등 serialization 기능은 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="1e3b3-140">따라서 이러한 두 오버로드는 차등 serialization이 노출되고 사용될 때까지 호출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="1e3b3-141">다음은 4가지 속성을 포함하는 OrderKey라는 사용자 지정 형식 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-141">Following is an example custom type called OrderKey that contains four properties</span></span>

```C#
public class OrderKey : IComparable<OrderKey>, IEquatable<OrderKey>
{
    public byte Warehouse { get; set; }

    public short District { get; set; }

    public int Customer { get; set; }

    public long Order { get; set; }

    #region Object Overrides for GetHashCode, CompareTo and Equals
    #endregion
}
```

<span data-ttu-id="1e3b3-142">다음은 IStateSerializer<OrderKey>의 구현 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="1e3b3-143">baseValue를 사용하는 읽기 및 쓰기 오버로드는 이후 버전과의 호환성을 위해 해당 오버로드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

```C#
public class OrderKeySerializer : IStateSerializer<OrderKey>
{
  OrderKey IStateSerializer<OrderKey>.Read(BinaryReader reader)
  {
      var value = new OrderKey();
      value.Warehouse = reader.ReadByte();
      value.District = reader.ReadInt16();
      value.Customer = reader.ReadInt32();
      value.Order = reader.ReadInt64();

      return value;
  }

  void IStateSerializer<OrderKey>.Write(OrderKey value, BinaryWriter writer)
  {
      writer.Write(value.Warehouse);
      writer.Write(value.District);
      writer.Write(value.Customer);
      writer.Write(value.Order);
  }
  
  // Read overload for differential de-serialization
  OrderKey IStateSerializer<OrderKey>.Read(OrderKey baseValue, BinaryReader reader)
  {
      return ((IStateSerializer<OrderKey>)this).Read(reader);
  }

  // Write overload for differential serialization
  void IStateSerializer<OrderKey>.Write(OrderKey baseValue, OrderKey newValue, BinaryWriter writer)
  {
      ((IStateSerializer<OrderKey>)this).Write(newValue, writer);
  }
}
```

## <a name="upgradability"></a><span data-ttu-id="1e3b3-144">업그레이드 가능성</span><span class="sxs-lookup"><span data-stu-id="1e3b3-144">Upgradability</span></span>
<span data-ttu-id="1e3b3-145">[롤링 응용 프로그램 업그레이드](service-fabric-application-upgrade.md)에서는 한번에 하나의 업그레이드 도메인에서 노드의 하위 집합에 업그레이드가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), the upgrade is applied to a subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="1e3b3-146">이 과정에서 일부 업그레이드는 응용 프로그램의 최신 버전에, 일부 업그레이드 도메인은 응용 프로그램의 이전 버전에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-146">During this process, some upgrade domains will be on the newer version of your application, and some upgrade domains will be on the older version of your application.</span></span> <span data-ttu-id="1e3b3-147">롤아웃 동안 최신 버전의 응용 프로그램에서 이전 버전의 데이터를 읽을 수 있고 이전 버전의 응용 프로그램에서 최신 버전의 데이터를 읽을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-147">During the rollout, the new version of your application must be able to read the old version of your data, and the old version of your application must be able to read the new version of your data.</span></span> <span data-ttu-id="1e3b3-148">데이터 서식이 최신 버전과 이전 버전에서 호환되지 않으면 업그레이드가 실패하거나 데이터가 손실되거나 손상될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-148">If the data format is not forward and backward compatible, the upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="1e3b3-149">기본 제공 직렬 변환기를 사용하는 경우 호환성에 대해 염려할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-149">If you are using  built-in serializer, you do not have to worry about compatibility.</span></span>
<span data-ttu-id="1e3b3-150">그러나 사용자 지정 직렬 변환기 또는 DataContractSerializer를 사용하는 경우 데이터가 이전 버전 및 이후 버전과 무기한 호환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-150">However, if you are using a custom serializer or the DataContractSerializer, the data have to be infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="1e3b3-151">즉, 각 버전의 직렬 변환기가 해당 형식의 모든 버전을 직렬화 및 deserialize할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-151">In other words, each version of serializer needs to be able to serialize and de-serialize any version of the type.</span></span>

<span data-ttu-id="1e3b3-152">데이터 계약 사용자는 필드의 추가, 제거 및 변경에 대해 잘 정의된 버전 관리 규칙을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-152">Data Contract users should follow the well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="1e3b3-153">데이터 계약은 알 수 없는 필드를 처리하는 기능, serialization 및 deserialization 프로세스에 연결하는 기능, 클래스 상속을 처리하는 기능도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-153">Data Contract also has support for dealing with unknown fields, hooking into the serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="1e3b3-154">자세한 내용은 [데이터 계약 사용](https://msdn.microsoft.com/library/ms733127.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="1e3b3-155">사용자 지정 직렬 변환기 사용자는 이전 버전 및 이후 버전과의 호환성을 유지하기 위해 사용 중인 직렬 변환기의 지침을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-155">Custom serializer users should adhere to the guidelines of the serializer they are using to make sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="1e3b3-156">모든 버전을 지원하는 일반적인 방법은 시작 부분에 크기 정보를 추가하고 선택적 속성만 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-156">Common way of supporting all versions is adding size information at the beginning and only adding optional properties.</span></span>
<span data-ttu-id="1e3b3-157">그러면 각 버전이 가능한 양만큼 읽고 스트림의 나머지 부분을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-157">This way each version can read as much it can and jump over the remaining part of the stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e3b3-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e3b3-158">Next steps</span></span>
  * [<span data-ttu-id="1e3b3-159">serialization 및 업그레이드</span><span class="sxs-lookup"><span data-stu-id="1e3b3-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="1e3b3-160">신뢰할 수 있는 컬렉션에 대한 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="1e3b3-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="1e3b3-161">[Visual Studio를 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial.md) 에서는 Visual Studio를 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="1e3b3-162">[Powershell을 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial-powershell.md) 에서는 PowerShell을 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="1e3b3-163">[업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md)를 사용하여 응용 프로그램 업그레이드 방법을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="1e3b3-164">[고급 항목](service-fabric-application-upgrade-advanced.md)을 참조하여 응용 프로그램을 업그레이드하는 동안 고급 기능을 사용하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-164">Learn how to use advanced functionality while upgrading your application by referring to [Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="1e3b3-165">[응용 프로그램 업그레이드 문제 해결](service-fabric-application-upgrade-troubleshooting.md)의 단계를 참조하여 응용 프로그램 업그레이드 중 발생하는 일반적인 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="1e3b3-165">Fix common problems in application upgrades by referring to the steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>

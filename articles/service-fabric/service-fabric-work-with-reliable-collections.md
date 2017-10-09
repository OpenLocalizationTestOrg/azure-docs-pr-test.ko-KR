---
title: "신뢰할 수 있는 컬렉션을 사용한 aaaWorking | Microsoft Docs"
description: "Hello 신뢰할 수 있는 컬렉션 작업을 위한 모범 사례에 알아봅니다."
services: service-fabric
documentationcenter: .net
author: rajak
manager: timlt
editor: 
ms.assetid: 39e0cd6b-32c4-4b97-bbcf-33dad93dcad1
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rajak
ms.openlocfilehash: 41ba0b257da8493c1fc2e99ad7565593dc7cbcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-reliable-collections"></a>신뢰할 수 있는 컬렉션 작업
서비스 패브릭 상태 저장 신뢰할 수 있는 컬렉션을 통해 사용할 수 있는 too.NET 개발자 모델 프로그래밍을 제공 합니다. 즉, 서비스 패브릭은 신뢰할 수 있는 사전 및 신뢰할 수 있는 큐 클래스를 제공합니다. 이러한 클래스를 사용하는 경우 상태가 분할되고(확장성의 경우) 복제되며(가용성의 경우) 파티션 내에서 트랜잭션 처리됩니다(ACID 의미 체계의 경우). 신뢰할 수 있는 사전 개체의 일반적인 사용을 살펴보고 실제로 어떤 역할을 하는지 확인하겠습니다.

```csharp

///retry:

try {
   // Create a new Transaction object for this partition
   using (ITransaction tx = base.StateManager.CreateTransaction()) {
      // AddAsync takes key's write lock; if >4 secs, TimeoutException
      // Key & value put in temp dictionary (read your own writes),
      // serialized, redo/undo record is logged & sent to
      // secondary replicas
      await m_dic.AddAsync(tx, key, value, cancellationToken);

      // CommitAsync sends Commit record toolog & secondary replicas
      // After quorum responds, all locks released
      await tx.CommitAsync();
   }
   // If CommitAsync not called, Dispose sends Abort
   // record toolog & all locks released
}
catch (TimeoutException) {
   await Task.Delay(100, cancellationToken); goto retry;
}
```

신뢰할 수 있는 사전 개체에 대한 모든 작업(취소할 수 없는 ClearAsync 실행 제외)은 ITransaction 개체를 필요로 합니다. 이 개체 및 모든 변경 내용을 toomake tooany 신뢰할 수 있는 사전 및/또는 단일 파티션 내에서 신뢰할 수 있는 큐 개체를 시도 중인 연결 되어 있습니다. ITransaction 획득 hello 파티션을 호출 하 여 개체의 StateManager의 CreateTransaction 메서드.

위의 hello 코드 hello ITransaction 개체 tooa 신뢰할 수 있는 사전 AddAsync 메서드에 전달 됩니다. 내부적으로 키를 허용 하는 사전 메서드 hello 키와 관련 된 판독기/작성기 잠금을 수행 합니다. Hello 방법은 hello 키에 쓰기 잠금을 활용 hello 메서드 hello 키의 값을 수정 하는 경우 고 hello 키의 값에서 읽기만 hello 메서드 읽기 잠금이 hello 키에 사용 됩니다. AddAsync hello 키의 값 toohello 새를 수정 하 고 있으므로 전달 된 값, hello 키의 쓰기 잠금을 사용 합니다. 따라서 2 (또는 그 이상) 스레드 시도 hello 사용 하 여 tooadd 값 동일 키 hello에 동일 time, 하나의 스레드는 hello 쓰기 잠금을 얻고 hello 다른 스레드가 차단 됩니다. 기본적으로 too4 초 tooacquire hello 잠금; 구성에 대 한 메서드 블록 hello 메서드 4 초가 지난 후 TimeoutException를 throw 합니다. 메서드 오버 로드 하려는 경우 가능 하면 toopass 명시적 시간 제한 값 존재 합니다.

일반적으로 catch 하 고 (hello 코드 에서처럼 위의) hello 전체 작업을 다시 시도 하 여 코드 tooreact tooa TimeoutException를 작성 합니다. 간단한 코드에서 매번 100밀리초를 전달하는 Task.Delay를 호출하려 합니다. 그러나 실제로는 대신 일종의 지수 백오프 지연을 사용하는 것이 좋습니다.

Hello 잠금이 획득 되 면 AddAsync hello 키를 추가 하 고 값 개체 hello ITransaction 개체와 연결 된 임시 사전을 내부 tooan를 참조 합니다. 이 작업은 수행 tooprovide 읽기 / your-소유-쓰기를 의미 체계에 있습니다. 즉, AddAsync, 이후 호출 tooTryGetValueAsync를 호출 하 고 나면 (동일한 ITransaction 개체 hello를 사용 하 여) hello 트랜잭션이 커밋되지 않은 경우에 hello 값을 반환 합니다. 다음으로, AddAsync 직렬화 키 및 값 toobyte 배열 개체 하 고 hello 로컬 노드에서 이러한 바이트 배열 tooa 로그 파일을 추가 합니다. 마지막으로, AddAsync hello 바이트 배열 tooall hello 보조 복제본은 동일한 hello가 있으므로 키/값 정보를 보냅니다. Hello 키/값 정보를 작성 한 tooa 로그 파일에도 연결 되어 있는 hello 트랜잭션을 커밋 했습니다 될 때까지 hello 정보 hello 사전의 일부로 간주 되지 않습니다.

위의 hello 코드 hello 호출 tooCommitAsync hello 트랜잭션 작업 모두를 커밋합니다. 특히, 커밋 hello 로컬 노드에서 toohello 로그 파일 정보를 추가 하 고도 hello 커밋 레코드 tooall hello 보조 복제본을 보냅니다. 모든 데이터 변경 내용을 다른 스레드/트랜잭션이 조작할 수 있도록 영구 및 hello ITransaction 개체를 통해 조작 된 키와 연결 된 모든 잠금 해제 됩니다 것으로 간주 됩니다 동일한 키 hello hello 복제본의 쿼럼 (주) 회신 한 후 및 해당 값입니다.

CommitAsync (일반적으로 인해 발생 하는 tooan 예외)를 호출 하지 않은 경우 hello ITransaction 개체가 삭제를 가져옵니다. 커밋되지 않은 ITransaction 개체를 삭제, 서비스 패브릭 중단 정보 toohello 로컬 노드의 로그 파일 추가 보낼 시기 및 toobe 필요 없습니다 tooany hello의 보조 복제본입니다. 고 그런 다음 hello 트랜잭션을 통해 조작 된 키와 연결 된 모든 잠금이 해제 됩니다.

## <a name="common-pitfalls-and-how-tooavoid-them"></a>일반적인 문제 및 방법을 tooavoid에
신뢰할 수 있는 컬렉션 hello 내부적으로 작동 하는 방식 이해 했으므로 살펴보겠습니다는 몇 가지 일반적인에서 그 중입니다. Hello 코드 아래를 참조 하십시오.

```csharp
using (ITransaction tx = StateManager.CreateTransaction()) {
   // AddAsync serializes hello name/user, logs hello bytes,
   // & sends hello bytes toohello secondary replicas.
   await m_dic.AddAsync(tx, name, user);

   // hello line below updates hello property’s value in memory only; the
   // new value is NOT serialized, logged, & sent toosecondary replicas.
   user.LastLogin = DateTime.UtcNow;  // Corruption!

   await tx.CommitAsync();
}
```

일반.NET 사전을 사용 하 여 작업을 하는 경우 키/값 toohello 사전을 추가할 수 있으며 (예: LastLogin) 속성의 hello 값을 변경 합니다. 그러나 이 코드는 신뢰할 수 있는 사전으로 제대로 작동하지 않습니다. 기억 hello에서 이전 설명 tooAddAsync hello 키/값 또는 그 반대로 serialize 하는 hello 호출 개체 toobyte 배열 하 고 저장 hello tooa 로컬 파일 배열은 toohello 보조 복제본도 보냅니다. 나중에 속성을 변경 하면이 메모리에만; hello 속성의 값 변경 hello 로컬 파일이 나 toohello 복제본에 전송 되는 hello 데이터는 영향을 주지 않습니다. Hello 프로세스의 작동이 중단 하는 경우 메모리에 포함 된 내용 자리를 비울 throw 됩니다. 새 프로세스가 시작 되거나 다른 복제본이 주, 하는 경우 이전 속성 값을 다음 hello 것은 사용할 수 있습니다.

강조 해도 지나치지 충분히 얼마나 쉬운지 toomake hello 유형의 위에 표시 된 실수입니다. 와 배웁니다 hello 실수에 대 한 경우 hello 프로세스의 작동이 중지 합니다. hello 올바른 방법은 toowrite hello 코드는 단순히 tooreverse hello 선을 두 선입니다.


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

일반적인 실수를 보여주는 또 다른 예는 다음과 같습니다.

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> user =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (user.HasValue) {
      // hello line below updates hello property’s value in memory only; the
      // new value is NOT serialized, logged, & sent toosecondary replicas.
      user.Value.LastLogin = DateTime.UtcNow; // Corruption!
      await tx.CommitAsync();
   }
}
```

다시 일반.NET 사전 위의 hello 코드에서 제대로 작동 하 고는 일반적인 패턴: hello 개발자가 값을 키 toolook 사용 합니다. Hello 값이 있으면 hello 개발자는 속성의 값을 변경 합니다. 그러나 신뢰할 수 있는 컬렉션으로이 코드를 보여 동일한 문제가 설명한 바와 같이 hello: **지정 하면 해당 tooa 신뢰할 수 있는 컬렉션 개체를 수정 하지 해야 합니다.**

신뢰할 수 있는 컬렉션에 있는 값 방식으로 tooupdate tooget 참조 toohello 기존 값 이며 hello 개체가 참조 tooby 변경할 수 없는이 참조 하는 것이 좋습니다. 올바른 번호입니다. 그런 다음 hello 원래 개체의 정확한 복사본 인 새 개체를 만듭니다. 이제이 새 개체의 hello 상태를 수정할 수 있으며 hello 새 개체에 쓸 hello 컬렉션 serialize 되는 것을 toobyte 배열 추가 toohello 로컬 파일 및 toohello 복제본 전송 수 있습니다. Hello 커밋 변경 내용, hello 메모리 내 개체 hello 로컬 파일 및 모든 hello 복제본 있음 hello 후 상태를 정확히 동일 합니다. 모두 정상입니다.

hello 코드 아래 신뢰할 수 있는 컬렉션의 올바른 방법은 tooupdate hello 값을 보여 줍니다.

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> currentUser =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (currentUser.HasValue) {
      // Create new user object with hello same state as hello current user object.
      // NOTE: This must be a deep copy; not a shallow copy. Specifically, only
      // immutable state can be shared by currentUser & updatedUser object graphs.
      User updatedUser = new User(currentUser);

      // In hello new object, modify any properties you desire
      updatedUser.LastLogin = DateTime.UtcNow;

      // Update hello key’s value toohello updateUser info
      await m_dic.SetValue(tx, name, updatedUser);

      await tx.CommitAsync();
   }
}
```

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a>변경 불가능 한 데이터 형식을 tooprevent 프로그래머 오류를 정의 합니다.
이상적으로 실수로 한다는 tooconsider 변경할 수 없는 개체의 상태를 변경 하는 코드를 생성할 경우 hello 컴파일러 tooreport 오류 같은 합니다. 하지만 hello C# 컴파일러에 없는 hello 기능 toodo이 있습니다. 따라서 tooavoid 잠재적인 프로그래머 버그를 신뢰할 수 있는 컬렉션 toobe 변경할 수 없는 형식을 사용 하는 hello 형식을 정의 하는 것이 좋습니다. 즉, toocore 값 형식 (예: [Int32, UInt64, 등]는 숫자, DateTime, Guid, TimeSpan 및 같은 hello)는 그대로 유지 합니다. 물론 문자열도 사용할 수 있습니다. 직렬화 하는 작업으로 최상의 tooavoid 컬렉션 속성 이며을 역직렬화 하는 동안 자주 수 성능이 떨어질 수 있습니다. 그러나 toouse 컬렉션 속성을 사용 하도록 하려는 경우 매우 hello 사용을 좋습니다. NET의 변경할 수 없는 컬렉션 라이브러리 ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)). 이 라이브러리는 http://nuget.org에서 다운로드할 수 있습니다. 또한 클래스를 봉인하고 가능한 경우 읽기 전용 필드를 만드는 것이 좋습니다.

hello 아래에서 사용자 정보 유형에는 변경할 수 없는 toodefine 앞에서 언급 한 권장 사항 활용을 입력 하는 방법을 보여 줍니다.

```csharp

[DataContract]
// If you don’t seal, you must ensure that any derived classes are also immutable
public sealed class UserInfo {
   private static readonly IEnumerable<ItemId> NoBids = ImmutableList<ItemId>.Empty;

   public UserInfo(String email, IEnumerable<ItemId> itemsBidding = null) {
      Email = email;
      ItemsBidding = (itemsBidding == null) ? NoBids : itemsBidding.ToImmutableList();
   }

   [OnDeserialized]
   private void OnDeserialized(StreamingContext context) {
      // Convert hello deserialized collection tooan immutable collection
      ItemsBidding = ItemsBidding.ToImmutableList();
   }

   [DataMember]
   public readonly String Email;

   // Ideally, this would be a readonly field but it can't be because OnDeserialized
   // has tooset it. So instead, hello getter is public and hello setter is private.
   [DataMember]
   public IEnumerable<ItemId> ItemsBidding { get; private set; }

   // Since each UserInfo object is immutable, we add a new ItemId toohello ItemsBidding
   // collection by creating a new immutable UserInfo object with hello added ItemId.
   public UserInfo AddItemBidding(ItemId itemId) {
      return new UserInfo(Email, ((ImmutableList<ItemId>)ItemsBidding).Add(itemId));
   }
}
```

hello ItemId 유형을 다음과 같이 변경할 수 없는 형식 이기도 합니다.

```csharp

[DataContract]
public struct ItemId {

   [DataMember] public readonly String Seller;
   [DataMember] public readonly String ItemName;
   public ItemId(String seller, String itemName) {
      Seller = seller;
      ItemName = itemName;
   }
}
```

## <a name="schema-versioning-upgrades"></a>스키마 버전 관리(업그레이드)
내부적으로 신뢰할 수 있는 컬렉션은 .NET에 있는 DataContractSerializer를 사용하여 개체를 직렬화합니다. hello 직렬화 된 개체는 지속형된 toohello 주 복제본의 로컬 디스크 이며도 전송 된 toohello 보조 복제본입니다. 서비스에 완성 되어 감에 toochange hello 유형의 서비스에 필요한 데이터 (스키마)를 할 가능성이 높습니다. 데이터의 버전 관리에 주의를 기울여서 접근해야 합니다. 무엇 보다도, 항상 수 toodeserialize 오래 된 데이터 여야 합니다. 특히, 즉 deserialization 코드를 무한히 이전 버전과 호환성: 서비스 코드의 버전 333 5 년 전에 서비스 코드의 버전 1에 의해 신뢰할 수 있는 컬렉션에 있는 데이터에 수 toooperate 이어야 합니다.

또한 서비스 코드는 한 번에 하나의 업그레이드 도메인을 업그레이드합니다. 따라서 업그레이드하는 동안 다른 두 버전의 서비스 코드를 동시에 실행합니다. Hello 새 버전이 서비스 코드의 이전 버전의 서비스 코드 수 toohandle hello 새 스키마가 아닐 수 대로 hello 새 스키마를 사용 하지 않도록 해야 합니다. 가능 하면 1 버전에 의해 프로그램 서비스 toobe 더 높은 버전과 호환의 각 버전을 디자인 해야 합니다. 즉, 서비스 코드의 V1 수 있어야 한다는 toosimply 명시적으로 처리 하지 않는 모든 스키마 요소를 무시 합니다. 그러나 모든 데이터에 대해 명시적으로 알고 하 고 단순히 작성 하지 않는 사전 키 또는 값을 업데이트할 때 다시 수 toosave 이어야 합니다.

> [!WARNING]
> 키의 hello 스키마를 수정할 수 있는 동안 키의 해시 코드와 equals 알고리즘은 안정성을 확인 해야 합니다. 이러한 알고리즘 중 하나가 작동을 바꾸면 됩니다 수 toolook hello 신뢰할 수 있는 사전 내의 hello 키를 다시 적이 있습니다.
>
>

또는 작업은 일반적으로 참조 tooas 2 단계 업그레이드를 수행할 수 있습니다. 2 단계 업그레이드에서 업그레이드 하는 서비스 V1 tooV2: V2 hello 새 스키마 변경만이 코드는 toodeal 없습니다 실행 되는 방법을 알고 있는 hello 코드를 포함 합니다. Hello V2 코드 V1 데이터를 읽는 경우의 동작을 V1 데이터 씁니다. 그런 다음 업그레이드 도메인 전체에 걸쳐 hello 업그레이드가 완료 되 면 알릴 수 있습니다 어떻게 하 든 V2 인스턴스를 실행 하는 toohello 해당 hello 업그레이드가 완료 되었습니다. (한 가지 방법은 toosignal 구성 업그레이드 아웃 tooroll 이며이이 2 단계 업그레이드를 사용 합니다.) 이제 hello V2 인스턴스 수 V1 데이터를 읽을, tooV2 데이터 변환, 작업 및 V2 데이터로 작성 합니다. Tooconvert 필요 하지 않은 다른 인스턴스에서 V2 데이터를 읽을 때, 방금이 경우에 작동 하며 V2 데이터를 작성 합니다.

## <a name="next-steps"></a>다음 단계
toolearn 정방향 호환 되는 데이터 계약을 만드는 방법에 대 한 참조 [이후 버전과 호환 데이터 계약](https://msdn.microsoft.com/library/ms731083.aspx)합니다.

데이터 계약 버전 관리에서 모범 사례 toolearn 참조 [데이터 계약 버전 관리](https://msdn.microsoft.com/library/ms731138.aspx)합니다.

toolearn tooimplement 버전 허용 데이터 계약 참조 [버전 독립적 Serialization 콜백](https://msdn.microsoft.com/library/ms733734.aspx)합니다.

tooprovide 여러 버전 간 상호 운용할 수 있는 데이터 구조를 확인 하려면 어떻게 toolearn [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx)합니다.

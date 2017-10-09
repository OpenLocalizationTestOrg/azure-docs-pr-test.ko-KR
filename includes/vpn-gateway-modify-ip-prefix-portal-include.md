### <a name="noconnection"></a>toomodify 로컬 네트워크 게이트웨이 IP 주소 접두사 게이트웨이 연결 없음

#### <a name="tooadd-additional-address-prefixes"></a>tooadd 추가 주소 접두사:

1. 로컬 네트워크 게이트웨이 리소스 hello에 hello에 **설정** 섹션에서 클릭 **구성**합니다.
2. Hello에 hello IP 주소 공간 추가 *추가 주소 범위 추가* 상자입니다.
3. 클릭 **저장** toosave 설정 합니다.

#### <a name="tooremove-address-prefixes"></a>tooremove 주소 접두사:

1. 로컬 네트워크 게이트웨이 리소스 hello에 hello에 **설정** 섹션에서 클릭 **구성**합니다.
2. Hello 클릭 **'...'** tooremove hello 접두사를 포함 하는 hello 줄에 원하는 합니다.
3. **제거**를 클릭합니다.
4. 클릭 **저장** toosave 설정 합니다.

### <a name="withconnection"></a>toomodify 로컬 네트워크 게이트웨이 IP 주소 접두사-기존 게이트웨이 연결

게이트웨이 연결 하 고 원하는 tooadd 또는 로컬 네트워크 게이트웨이에 포함 된 hello IP 주소 접두사를 제거 하는 경우 toodo hello 순서에 단계를 수행 해야 합니다. 이로 인해 VPN 연결에 약간의 가동 중지 시간이 발생합니다. IP 주소 접두사를 수정할 때 toodelete hello VPN 게이트웨이 필요는 없습니다. Tooremove hello 연결을 하기만 하면 됩니다.

#### <a name="1-remove-hello-connection"></a>1. Hello 연결을 제거 합니다.

1. 로컬 네트워크 게이트웨이 리소스 hello에 hello에 **설정** 섹션에서 클릭 **연결**합니다.
2. Hello 클릭 **...**  각 연결에 대 한 hello 선에 클릭 **삭제**합니다.
3. 클릭 **저장** toosave 설정 합니다.

#### <a name="2-modify-hello-address-prefixes"></a>2. Hello 주소 접두사를 수정 합니다.

tooadd 추가 주소 접두사:

1. 로컬 네트워크 게이트웨이 리소스 hello에 hello에 **설정** 섹션에서 클릭 **구성**합니다.
2. Hello IP 주소 공간을 추가 합니다.
3. 클릭 **저장** toosave 설정 합니다.

tooremove 주소 접두사:

1. 로컬 네트워크 게이트웨이 리소스 hello에 hello에 **설정** 섹션에서 클릭 **구성**합니다.
2. Hello 클릭 **...**  tooremove hello 접두사를 포함 하는 hello 줄에 원하는 합니다.
3. **제거**를 클릭합니다.
4. 클릭 **저장** toosave 설정 합니다.

#### <a name="3-recreate-hello-connection"></a>3. Hello 연결을 다시 만드십시오.

1. VNet에 대 한 가상 네트워크 게이트웨이 toohello를 이동 합니다. (하지 hello 로컬 네트워크 게이트웨이입니다.)
2. Hello에 가상 네트워크 게이트웨이 hello에 **설정** 섹션에서 클릭 **연결**합니다.
3. Hello 클릭 **+ 추가** tooopen hello **연결 추가** 블레이드입니다.
4. 연결을 다시 만듭니다.
5. 클릭 **확인** toocreate hello 연결 합니다.

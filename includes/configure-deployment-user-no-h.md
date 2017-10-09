Hello로 배포 자격 증명을 만들어 [az webapp 배포 사용자 집합](/cli/azure/webapp/deployment/user#set) 명령입니다.

배포 사용자가 FTP 및 로컬 Git 배포 tooa 웹 앱 필요 합니다. hello 사용자 이름 및 암호는 계정 수준입니다. _Azure 구독 자격 증명과 다릅니다._

Hello에서 다음 명령을, 대체  *\<사용자 이름 >* 및  *\<암호 >* 새 사용자 이름 및 암호. hello 사용자 이름은 고유 해야 합니다. hello 암호 최소 8 자 이어야, hello 세 요소 다음의 두 개의: 문자, 숫자, 기호입니다. 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

발생 하는 경우는 ` 'Conflict'. Details: 409` 오류, hello 사용자 이름을 변경 합니다. ` 'Bad Request'. Details: 400` 오류가 발생하면 더 강력한 암호를 사용합니다.

이 배포 사용자는 한 번만 만들며, 모든 Azure 배포에 사용할 수 있습니다.

> [!NOTE]
> 레코드 hello 사용자 이름 및 암호를 제공 합니다. 원하는 toodeploy hello 웹 앱 나중입니다.
>
>
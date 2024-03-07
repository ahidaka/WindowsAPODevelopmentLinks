# Training.md

Windows APO Development Links / Training.md

## Windows 11 APO 開発セミナー 演習 補足情報

### Windows の開発者向け 設定

![開発者 設定](va-0dev.png)

### 3. サンプルコードAPO 演習

#### SYSVAD フォルダーのコピー（コピー元フォルダー）

![SYSVAD フォルダーのコピー](va-00.png)

#### sysvad.sln ソリューションファイル（Visual Studio で開く）

![画面](va-0.png)

#### ビルド対象プロジェクト（DelayAPO, PropPageExt, SwapAPO）

![画面](va-1.png)

#### ビルドのプルダウンメニュー（ソリューション エクスプローラー）

![画面](va-2.png)

#### ビルドしたオブジェクト（dll）の場所

DelayAPO.dll, PropPageExt.dll, SwapAPO.dll のコピーが必要。

![画面](va-3.png)

#### コピー先： C:\SYSVAD フォルダー

![画面](va-4.png)


#### OCXを登録

```sh
Regsvr32 DelayAPO.dll
Regsvr32 SwapAPO.dll
Regsvr32 PropPageExt.dll
```
<br/>

#### 操作前のレジストリ

![画面](va-5.png)
<br/>

#### レジストリの操作（）

APOを登録するためのレジストリを編集します。 RegEditを開き、ActiveRenderコマンドで確認しておいた、 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\MMDevices\Audio 以下のデバイスGUID以下の「FxProperties」を参照して次の操作します。

**古い値の削除**

以下のプロジェクトキーがある場合は、全て削除します。

    {d04e05a6-594b-4fb6-a80d-01af5eed7d1d},3
    {d04e05a6-594b-4fb6-a80d-01af5eed7d1d},5
    {d04e05a6-594b-4fb6-a80d-01af5eed7d1d},6
    {d04e05a6-594b-4fb6-a80d-01af5eed7d1d},7

**新しいAPO値登録**

次の操作でビルドした新しいAPOのCLSIDを設定します。 CLSIDのGUIDは、ビルドした各ソースコード中のIDLファイル等に記述されているので、それを探してコピーすることが可能です。

    {d04e05a6-594b-4fb6-a80d-01af5eed7d1d},3

に

    {19166F23-5F08-47F9-BB57-9F57A977D88E}

を設定します。（CPL: コントロールパネルのダイアログ）
無い場合は、値をREG_SZ型で作成します。

    {d04e05a6-594b-4fb6-a80d-01af5eed7d1d},13

に

    {B48DEA3F-D962-425a-8D9A-9A5BB37A9904}
    {77802b45-a5a0-455a-8204-3dba30eee7b4}

を設定します。無い場合は、値をREG_MULTI_SZ型で作成します。


    {d04e05a6-594b-4fb6-a80d-01af5eed7d1d},14

に

    {06687E71-F043-403A-BF49-CB591BA6E103}
    {b6c7032b-1f17-4cc6-bcdb-fd96deabc8a9}

を設定します。無い場合は、値をREG_MULTI_SZ型で作成します。

REG_MULTI_SZ値は改行コードで区切ります。


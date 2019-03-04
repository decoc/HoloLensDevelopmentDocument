# Unityの設定
Unityでアプリケーションを作成する際には，どのプラットフォーム向けのアプリケーションを作成するか指定します。<b>File->Build Settings</b>からプラットフォームを指定してSwitch Platformで切り替えます。  
HoloLensでは，<b> Universal Windows Platform </b>を選択します。このUWPとは，様々なデバイス上で動作するアプリケーションを単一のフレームワーク上に統合する仕組みです。ただ，System.IOなど一部UWPでは使い方が異なるAPIがあったり，そもそもUWPでは存在しないAPIがあるなどくせ者であり，このような背景からAssetStoreで購入したAssetが他のプラットフォームでは動くが，<b>UWPでは動かないなんてことがよくあります。</b>

- [Build Settings](##BuildSettings)
    - [Target Device](##TargetDevice)
    - [BuildType](###BuildType)
    - [SDK](###SDK)

- [Player Setting](###PlayerSettings)
    - [Other Settings](###OtherSettings)
        - [Scripting Runtime Version](####ScriptingRuntimeVersion)
        - [Scripting Backend](####ScriptingBackend)

- [Publish Setting](###PublishSetting)
    - [Capabilities](###Capabilities)
    - [XRSettings](###XRSettings)

---
## BuildSettings
アプリケーションのビルドに必要な項目です。File->Build Settings もしくは Ctr + Shift + B(Buildの意) で開きます

### TargetDevice
HoloLensを指定しても，そのままのAnyPlatformでも特に問題はありません。

### BuildType
3Dのアプリケーションを作る際にはD3Dを，Edgeのような2Dのアプリケーションを作る際にはXAMLを指定します。

### SDK
Windows 10 SDK のことです。基本的には新しいSDKが入っていれば特に問題ありません。プルダウンからSDKが入っているかどうか確認してください。

### Visual Studio Version
2017または2019を選択してください。

### Unity C# Projects
.NETを指定している場合のみ選択できます。(※Unity2018.4まで可能です。) slnファイルをC#で書き出せるので，Unityから都度ビルドしなくとも，こちらのslnファイルからコードの編集ができます。また，UWPのコードを書く際には生成したslnファイルから編集するのが楽です。

---
## PlayerSettings
さまざまなオプションを設定します。

### OtherSettings
#### ScriptingRuntimeVersion
.NET Frameworkサポートと同等のバージョンが利用できます。2017までは.Net3.5が標準で，.Net4.6は試験的に利用可能でした。2018からは.Net4.6が標準になります。

[C#6.0時代のUnity](https://qiita.com/divideby_zero/items/71a38acdbaa55e88e2d9)

#### ScriptingBackend
UWPのアプリケーション開発ではこの[Scripting backend](https://docs.unity3d.com/ja/current/Manual/windowsstore-scriptingbackends.html)を.NETかIL2CPPを選択する必要があります。  
(※.NETはUnity2018.4まで可能です。2019以降はIL2CPPのみになります。)  

.NET環境とIL2CPP環境のそれぞれで，利用できるAPIやGCの仕組みなどが異なります。  
あまり解説記事も見当たらずおまじない的な扱いで使われている気もしますが，表面的な違いで言えば以下の違いになります。

||ビルド速度|実行速度|C#プロジェクト出力の可否|サポート|
|:---:|:---:|:---:|:---:|:---:|
|.NET|(IL2CPPと比較して)早い|(IL2CPPと比較して)早くはない|可|2018.4まで|
|IL2CPP|遅い|速い|不可|2019以降標準|

これらの違いはJITコンパイルとAOTコンパイルの仕組み，違いをまず理解する必要があります。

【参考】
- [IL2CPPのしくみ](https://docs.unity3d.com/ja/current/Manual/IL2CPP-HowItWorks.html)
- [IL2CPPに関する軽い話](https://www.google.co.jp/url?sa=t&rct=j&q=&esrc=s&source=web&cd=6&cad=rja&uact=8&ved=2ahUKEwiKtLyY3OHcAhUEQN4KHcxdCxcQFjAFegQIBhAB&url=https%3A%2F%2Fwww.slideshare.net%2FWooramYang%2Fil2-cpp-wooramyang-49666751&usg=AOvVaw2_L54wiVpvcgtfgYa2Lqvu)
- [【Unity】Stripping Levelについて (プラットフォームによる差異の項)](https://www.f-sp.com/entry/2016/02/23/180816)

##### 導入
.NETまたはIL2CPPのいずれかが<b>アプリケーションのビルドに必要です。</b> UnityにComponentがなければビルドできません。

###### Unityを新規にインストールする場合
以下の項目をOnにしてインストールしてください。
- 2018: UWP Build Supported .Net (or IL2CPP)
- 2019: UWP Build Supported

###### 既存のUnityに追加する場合
Unityのインストーラから再度導入する形になります。新規インストールと同じ手順です。

###### UnityHubから追加する場合
Installsから追加したいUnityのバージョンからAddComponentで導入できます。
- 2018: UWP Build Supported .Net (or IL2CPP)
- 2019: UWP Build Supported

---
### PublishSettings
#### Capabilities
UnityからアプリをデプロイしてもCapabilitiesが有効になっておらず，機能が使えないという場合があります。例えば，カメラやマイクにアクセスする場合や，クライアントとしてサーバーと通信する，ファイルへアクセスする場合などはCapabilitiesでアプリケーションが利用できるように権限を与えてやる必要があります。  CapabilitiesはUnityのFile-> Build Settings -> Player Settings -> XR Settings -> Publish Settingsから設定します。

量が多いので代表的なものだけあげていきます。

|Capabilities|説明|
|:--:|:---|
|InternetClient|Sharingなどネットワークを経由して情報をやりとりする場合に必要です。|
|WebCam|VuforiaなどCameraを使う場合に必要です。|
|Microphone|音声入力などを使う場合に必要です。|
|SpatialPerception|SpatialMappingを使う場合に必要です。|
|Bluetooth|Xboxコントローラなどを使う場合に必要です。|

---
### XRSettings
<b>Virtual Reality Supported が有効でないと3DViewになりません。必ず有効にしてください。</b>  

また，Virtual Reality SDKのSettingから指定できるEnableDepthBufferSharingは，安定化平面の設置に関わります。こちらは有効にする必要はありません。詳細は[こちら](https://www.tattichan.work/entry/depthbuffer)。  

#### 注意
Virtual Reality Supportedを有効にした状態でシーンを再生すると，Mixed Reality Portal が立ち上がってしまう場合があります。そのような場合，Window -> Holographic Emulation -> Emulation Mode を None から Remote to Device に変更することでこの問題を回避することができます。

---

# アプリケーションの開発環境
HoloLensのアプリケーションを開発する上で，いくつかのツールが必要になります。インストールすれば使えるというものではなく、バージョンや設定の相性もあります。ここでは，各ツールの紹介と解説をします。

- [開発ツール](#開発ツール)
    - [Unity](##Unity)
        - [UnityHub](###UnityHub)
    - [Visual Studio](##VisualStudio)
    - [Windows10 SDK](##Windows10SDK)
    - [Mixed Reality Toolkit](##MixedRealityToolkit)

---
# 開発ツール
## Unity
HoloLensの3Dアプリケーション開発環境は，[Unity](https://unity3d.com/jp)を使った開発がスタンダードであり，ストアに並ぶHoloLens3Dアプリケーションの多くがUnityで作られたものです。  
Unity（別名:Unity3D）は、統合開発環境を内蔵し、複数の機材(platform)に対応するゲームエンジンです。
Unityのバージョンによって，HoloLensで利用できるAPIやサポートされる機能が変わってくるので注意が必要です。
また，バージョンによって対応する[bit数が異なる](https://blogs.unity3d.com/2019/02/26/hololens-2-is-coming-what-you-need-to-know/?utm_source=twitter&utm_medium=social&utm_campaign=community_global_announcement_2019-02-25_xr&utm_content=blog)ので注意が必要です。  

- 32bit-ARM: 2018.3以上
- 64bit-ARM: 2019.1以上

過去のバージョンのUnity一覧は[こちら](https://unity3d.com/jp/get-unity/download/archive)から参照できます。

### UnityHub
Unity公式から提供されている複数バージョンのUnityEditorを一括で管理するツールです。これまでのUnityは異なるバージョンをインストールする度にショートカットが生成され，それらを使い分ける形をとっていました。UnityHubでは，UnityHubから指定したバージョンでプロジェクト新規作成，プロジェクトの一覧管理，，Hub経由でインストールしたUnityに後からVuforiaなどのコンポーネントを追加するなどができます。[(UnityHubを用いて複数バージョンのUnityEditorを管理する)](https://qiita.com/k7a/items/ca4547725434580bc3a9)  

Vuforiaや後述するScriptingBackendの入れ忘れをした時に後からの導入が楽になるので，HoloLensアプリ開発でも役に立ちます。

[DownLoad](https://public-cdn.cloud.unity3d.com/hub/prod/UnityHubSetup.exe)

---
## VisualStudio
Unityで作ったアプリをビルドし，HoloLens上に展開するためには [Visual Studio 2017](https://visualstudio.microsoft.com/ja/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017&rr=https%3A%2F%2Fdocs.microsoft.com%2Fja-jp%2Fvisualstudio%2Finstall%2Finstall-visual-studio%3Fview%3Dvs-2017)、または[Visual Studio 2019](https://visualstudio.microsoft.com/ja/vs/preview/)が必要になります。  

---
## Windows10SDK
HoloLensアプリをビルドするためには，Windows 10 SDK が必要です。環境は構築できているのにビルドできないという場合，Windows 10 SDKが入っていないという事がよくありました。HoloLensのアプリ開発には10.0.14393が最低限必要でしたが，例えばImmersive向けでコントローラを扱うには最低限10.0.16299以上であったり，更に振動機能が使いたい場合は10.0.17134が必要になります。MRTKを使う時には特に引っかかるポイントだったりします。  

### インストールする
Windows 10 SDK は[Archive](https://developer.microsoft.com/en-us/windows/downloads/sdk-archive)から直接DLもできますが，Visual Studioからインストールするのが楽です。  
「Visual Studio Installer」 を立ち上げて，「詳細->変更」を押すと一覧が表示されます。「ユニバーサルWindowsプラットフォーム開発」を選択してインストールすると最新のWindows 10 SDK がインストールされます。また，この時オプションから過去のバージョンのWindows SDK も指定してDLすることができます。

---
## MixedRealityToolkit
[Mixed Reality Toolit](https://github.com/Microsoft/MixedRealityToolkit-Unity)は，HoloLensのアプリケーション開発をサポートするコンポーネント群です。よく勘違いがあるのですが，MRTKはHoloLensアプリの開発に必ずしも必要ではありません。

Mixed Relaity Toolkitには大きく2つのバージョンがあり，
Unity 5.6 - 2017 をサポートするバージョンと，2018以上をサポートするバージョンがあります。調べて出てくる情報の多くが前者に該当しますがHoloLens2のアプリ開発で必要なものは後者にあたります。
2018以降の大きな違いはHoloLensやIHMD以外にもOpenVR対応など，より多くのプラットフォームをカバーしている点です。HoloLens2開発ではこちらのバージョンを利用します。

先のGitHubリンクの[Release](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases)からダウンロードすることができます。HoloToolkit-Unity-XXXX.X.XがMRTKの本体で，HoloToolkit-Unity-Examples-XXXX.X.Xでその使い方を学ぶことができます。

注意点として，Mixed Reality Toolkit はUnityの多くのバージョンをサポートしてくれてはいますが，最新の環境では動作しなかったり，古いバージョンでは一部動作しなかったりします。利用したい環境に合わせた適切なパッケージを選択することが重要になりますので，<b><u>Upgrade Guide をよく読みましょう。</u></b>

詳細は，[Mixed Reality Toolkit](https://github.com/tattichan/HoloLensQuestions/blob/master/vNext.markdown) で扱います。
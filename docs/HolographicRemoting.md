# Holographic Remoting
ちょっとした変更に対して，HoloLensアプリを毎回実機にビルド，デプロイするのは時間も手間もかかります。Holographic Remoting はその確認作業の手間を大きく削減してくれます。  
Holographic Remotingを使うには，HoloLensとUnityEditor側でそれぞれ準備が必要です。  

## HoloLens: 
HoloLensのMicrosoft Storeから，[Holographic Remoting Player](https://www.microsoft.com/ja-jp/p/holographic-remoting-player/9nblggh4sv40) をDLし起動する。

## UnityEditor: 
1. File-> Build Settings -> Player Settings -> XR Settings -> Virtual Reality Settings を有効にする
2. Window -> Holographic Emulation -> Emulation Mode を None から Remote to Device に変更する
3. Remote Machine に HoloLens に表示されているIPアドレスを入力する -> Connect ボタンを押す
4. UnityEditorを再生するとHoloLensに映像が表示されるはずです。

## よくある誤解と注意点
Holographic Remotingは確かに便利機能ですがあくまで実行しているのは，PC側でHoloLens上ではありません。エアタップといった入力イベントはシミュレートできますが，HoloLensのカメラは利用できない，つまりVuforiaといったHoloLensのカメラを使ったデバッグはできません。また，UWPのコードも同様に実行されるのはEditor環境なので実行されないということに注意してください。

---
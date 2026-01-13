# 焼肉判定システム - Android APK

このディレクトリには、焼肉判定システムのAndroidアプリ版が含まれています。

## 🚀 APKのビルド方法

### 方法1: GitHub Actions（推奨）

1. このリポジトリをGitHubにプッシュ
2. GitHub Actionsが自動的にAPKをビルド
3. Actionsタブから `yakiniku-detector-debug.apk` をダウンロード

### 方法2: Android Studioでビルド

1. **Android Studioを開く**
2. **プロジェクトをインポート**
   - File → Open → `android-app` フォルダを選択
3. **ビルド**
   - Build → Build Bundle(s) / APK(s) → Build APK(s)
4. **APKの場所**
   - `android-app/app/build/outputs/apk/debug/app-debug.apk`

### 方法3: コマンドラインでビルド

```bash
cd android-app

# Gradle Wrapperの作成（初回のみ）
gradle wrapper --gradle-version 8.2

# Debug APKをビルド
./gradlew assembleDebug

# APKは以下に出力されます
# app/build/outputs/apk/debug/app-debug.apk
```

## 📱 APKのインストール

### Androidデバイスへのインストール

1. **提供元不明のアプリを許可**
   - 設定 → セキュリティ → 提供元不明のアプリ → 有効化
   
2. **APKをデバイスに転送**
   - USBケーブル、Google Drive、メール添付など

3. **APKをタップしてインストール**

### adbコマンドでインストール

```bash
adb install app-debug.apk
```

## 🏗️ プロジェクト構造

```
android-app/
├── app/
│   ├── src/main/
│   │   ├── AndroidManifest.xml      # アプリ設定
│   │   ├── java/.../MainActivity.java # メインActivity
│   │   ├── res/                      # リソース
│   │   │   ├── layout/               # レイアウトXML
│   │   │   └── values/               # 文字列・テーマ
│   │   └── assets/
│   │       └── index.html            # 検出用Webページ
│   └── build.gradle                  # アプリビルド設定
├── build.gradle                      # プロジェクト設定
├── settings.gradle                   # Gradle設定
└── gradle.properties                 # Gradleプロパティ
```

## ⚙️ 技術仕様

| 項目 | 値 |
|------|-----|
| 最小SDK | Android 7.0 (API 24) |
| ターゲットSDK | Android 14 (API 34) |
| アーキテクチャ | WebView + Roboflow API |
| 権限 | カメラ、インターネット |

## 🔧 カスタマイズ

### Roboflow APIキーの変更

`app/src/main/assets/index.html` を編集：

```javascript
const ROBOFLOW_API_KEY = "your-api-key-here";
const ROBOFLOW_MODEL = "your-model-name";
const ROBOFLOW_VERSION = 1;
```

### アプリ名の変更

`app/src/main/res/values/strings.xml` を編集：

```xml
<string name="app_name">新しいアプリ名</string>
```

## ❓ トラブルシューティング

### カメラが動作しない

- アプリの権限設定でカメラを許可してください
- 設定 → アプリ → 焼肉判定 → 権限 → カメラ → 許可

### 検出が動作しない

- インターネット接続を確認してください
- Roboflow APIキーが有効か確認してください

### ビルドエラー

- Android StudioとSDKが最新版か確認してください
- `./gradlew clean` を実行してから再ビルド

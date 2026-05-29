# 🐱 Bongo Cat 自動領取

透過反編譯並修改遊戲核心檔案 `Assembly-CSharp.dll`，實現商店道具自動領取以及自訂點擊倍率的功能。

## 🛠️ 準備工作

1. **必備工具**：請先下載並安裝 [dnSpy](https://github.com/dnSpy/dnSpy/releases)（用於編輯 C# DLL 檔案）。
2. **目標檔案路徑**：
   ```text
   Steam\steamapps\common\BongoCat\BongoCat_Data\Managed\Assembly-CSharp.dll

# 🐱 Bongo Cat 自動領取與數值修改腳本

透過反編譯並修改遊戲核心檔案 `Assembly-CSharp.dll`，實現商店道具自動領取以及自訂點擊倍率的功能。

## 🛠️ 準備工作

1. **必備工具**：請先下載並安裝 [dnSpy](https://github.com/dnSpy/dnSpy/releases)（用於編輯 C# DLL 檔案）。
2. **目標檔案路徑**：
   ```text
   Steam\steamapps\common\BongoCat\BongoCat_Data\Managed\Assembly-CSharp.dll

   ⚠️ 強烈建議： 在進行任何修改前，請務必先備份原版的 Assembly-CSharp.dll，以免修改錯誤導致遊戲無法運行。

📖 修改教學步驟
使用 dnSpy 開啟目標檔案後，請依照以下兩種功能進行修改：

功能一：商店道具自動領取
在左側 Assembly Explorer 依序展開：
Assembly-CSharp.dll ➡️ BongoCat ➡️ Shop ➡️ TimerUpdate()

在 TimerUpdate() 方法上點擊 右鍵 ➡️ 選擇 編輯方法 (Edit Method)。

在正確的邏輯位置（可參考下方截圖）寫入以下程式碼：
this._shopItem.Buy();

💡 進階技巧（延遲領取）：
如果你希望領取動作不要太快，可以加入一秒的延遲，改為以下寫法：
yield return new WaitForSeconds(1f);
this._shopItem.Buy();

<img width="1035" height="556" alt="image" src="https://github.com/user-attachments/assets/499819e7-415c-4c7a-b2a6-b233253ae030" />

功能二：自訂點擊數量 (一鍵 9999 下)
在左側 Assembly Explorer 依序展開：
Assembly-CSharp.dll ➡️ BongoCat ➡️ Cat ➡️ Tap(int)

在 Tap(int) 方法上點擊 右鍵 ➡️ 選擇 編輯方法 (Edit Method)。

找到觸發點擊事件的那行程式碼，修改 Invoke 括號內的數字（數字可隨意改成你想要的點擊量）：

// 將原有的數字改為 9999 或任意數值
onTap.Invoke(9999);

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ed4f5d2a-9465-4dd4-b5dd-67e9a552915c" />

💾 儲存與套用
以上代碼都修改完成後，點選 dnSpy 左上角選單的 File ➡️ Save Module...。

直接點擊 OK，儲存並覆蓋原本的 Assembly-CSharp.dll 檔案。

重新啟動遊戲，享受自動化的快感吧！🎉

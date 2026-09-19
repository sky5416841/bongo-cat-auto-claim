# 🐱 Bongo Cat 自動領取

修改遊戲核心檔案 `Assembly-CSharp.dll`，讓商店寶箱的倒數結束後**自動領取**，不用再手動按。

## 📥 使用方式（直接下載）

1. 到 [Releases](../../releases/latest) 下載最新的 `Assembly-CSharp.dll`。
2. 關閉遊戲，備份原本的檔案，再用下載的檔案覆蓋：
   ```text
   Steam\steamapps\common\BongoCat\BongoCat_Data\Managed\Assembly-CSharp.dll
   ```
3. 重新啟動遊戲即可。

> ⚠️ 每次遊戲更新，Steam 會把這個檔案覆蓋回原版，自動領取就會失效。遊戲更新後請重新下載最新的 Release 再覆蓋一次。
> 若 Release 的日期比遊戲更新還舊，代表還沒有對應新版的檔案，請稍等或到 Discord 詢問。

## 🛠️ 自己動手改（dnSpy）

想自己修改的話，需要 [dnSpy](https://github.com/dnSpy/dnSpy/releases)。**修改前務必先備份原版 DLL。**

1. 用 dnSpy 開啟上面路徑的 `Assembly-CSharp.dll`。
2. 在左側 Assembly Explorer 依序展開：`Assembly-CSharp.dll` ➡️ `BongoCat` ➡️ `Shop` ➡️ `TimerUpdate()`。
3. 在 `TimerUpdate()` 上按右鍵 ➡️ **編輯方法 (Edit Method)**。
4. 在寶箱準備好、呼叫 `OnChestReady()` 的那一行**後面**，加入：
   ```csharp
   this._shopItem.Buy();
   ```
5. 按編譯，再點選單 `File` ➡️ `Save Module...` ➡️ `OK` 覆蓋原檔。

<img width="1035" height="556" alt="image" src="https://github.com/user-attachments/assets/499819e7-415c-4c7a-b2a6-b233253ae030" />

## 💬 其他說明

- 冷卻時間只是遊戲本機的倒數計時，這個修改只是在倒數結束、寶箱準備好時自動呼叫一次領取，不會縮短冷卻。
- 本專案只提供 `Assembly-CSharp.dll`，不含 `.pdb`（遊戲執行不需要）。

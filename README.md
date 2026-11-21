# app-status

各 App 的「功能暫停開關」。App 會用 HTTPS 讀自己資料夾裡的 `switches.json`；讀到某個功能被關，就先不讓人用，等修好的新版。

**這個 repo 是公開的，任何人都看得到。只放開關，永遠不放秘密、金鑰、使用者資料，也不寫 App 的真實名稱（資料夾一律用代號）。**

## 檔案

| 代號 | 網址 |
|---|---|
| `a1` | `https://kbwen.github.io/app-status/a1/switches.json` |

代號對應哪個 App，只記在各 App 的私人 repo 裡。

格式：

```json
{"version": 1, "off": [{"flow": "restore_from_file", "max_build": 12}]}
```

- `off` 裡每一筆關掉一個功能；`flow` 是功能代碼（例如 `restore_from_file`、`undo_restore`）。
- `max_build` 選填：只關 build number 小於或等於它的版本；沒寫就是所有版本。
- 沒有要關的就是 `{"version": 1, "off": []}`。

## 規則（一定要守）

1. **網址永遠不換**：不改 repo 名稱、不改資料夾代號、不換網域。舊版 App 只認原本的網址；App 上線後代號也不改。
2. **有功能關著的時候，不刪檔案、不刪 repo。** 要開回來就改內容（把那一筆刪掉，或用 `max_build` 只關壞的版本）。
3. **`version` 永遠是 1**：以後要加東西只加新欄位，不升版本。
4. 改完推到 `main`，GitHub Pages 幾分鐘內更新；App 最慢約 6 小時讀到。
5. 推之前確認 JSON 格式正確（格式錯時 App 會沿用舊的值）。
6. commit 訊息和說明也不寫 App 的真實名稱。

## 怎麼關、怎麼開回來（例：某個 App 的 build 12 還原壞了）

1. 先全部關：`{"version": 1, "off": [{"flow": "restore_from_file"}]}`
2. 修好的 build 13 上架後，只關舊版：`{"version": 1, "off": [{"flow": "restore_from_file", "max_build": 12}]}`
3. 確定沒事了：`{"version": 1, "off": []}`

## 新增一個 App

開一個新的代號資料夾（`a2`、`a3`⋯），放 `switches.json`，在上面的表格加一列。

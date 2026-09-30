# drum-samples

ScrollScore 鼓組音色(大鼓、小鼓、中鼓、落地鼓)。

## 內容

| 資料夾 | 鼓件 |
|---|---|
| `DW Kick/` | DW 大鼓 |
| `Keplinger Snare/` | Keplinger 小鼓 |
| `DW Rack/` | DW 中鼓 |
| `DW Floor/` | DW 落地鼓 |

每個鼓件都有三種收音(`close` 近距離乾聲、`roomy` 含房間聲、`slam` 壓縮處理)× 三個力度層(`v3` 輕、`v4` 中、`v5` 強)× 四個 round-robin(`.01`–`.04`)。原始檔為 48kHz / 24-bit 立體聲 WAV。

## `web/`

給 ScrollScore 網頁/App 直接載入用的版本,由原始 WAV 轉出:

- 尾巴低於峰值 −54dB 之後裁掉(保留 30ms,再加 40ms 淡出),檔案裡不留多餘的靜音
- 轉成 16-bit FLAC(TPDF dither),無損壓縮,各瀏覽器(含 iOS Safari)都能解碼
- 取樣率、聲道、各力度層之間的相對音量都維持原樣

ScrollScore 目前使用 `roomy` 收音。

## 授權

(待補:音色來源與授權條款)

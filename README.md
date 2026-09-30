# drum-samples

ScrollScore 鼓組音色。

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

### 銅鈸、Hi-Hat、邊擊(`web/osdk-*.flac`)

原始 WAV 沒有銅鈸,這部分取自 [THE OPEN SOURCE DRUM KIT](https://github.com/crabacus/the-open-source-drumkit)(Real Music Media,公有領域 public domain),
跟 DW/Keplinger 一樣是錄音室單擊取樣:

| 檔名 | 內容 | round-robin |
|---|---|---|
| `osdk-hhclosed` | 閉合 Hi-Hat | 4 |
| `osdk-hhpedal` | 踩 Hi-Hat | 3 |
| `osdk-hhopen` | 半開 Hi-Hat | 3 |
| `osdk-ride` | Ride(鈸面) | 3 |
| `osdk-ridebell` | Ride 鈴心 | 2 |
| `osdk-crash` | Crash | 2 |
| `osdk-sidestick` | 小鼓邊擊(cross stick) | 4 |

處理方式:依實測峰值把原始錄音分成 `v3`/`v4`/`v5` 三個力度層(比例對齊 DW 鼓組的 v3:v4:v5 ≈ 0.36:0.64:1),
96kHz 降到 48kHz、整體音量調到 v5 峰值約 0.5(跟 DW 鼓組相同),銅鈸長尾巴裁到 1.5–2.6 秒並淡出,轉 16-bit FLAC。

## 授權

- `DW Kick/`、`Keplinger Snare/`、`DW Rack/`、`DW Floor/` 及對應的 `web/dw-*`、`web/keplinger-*`:
  indiedrums「[DW Collectors Kit + Keplinger Snare](https://www.indiedrums.com/product/dw-collectors/)」免費鼓組取樣
- `web/osdk-*`:THE OPEN SOURCE DRUM KIT by Real Music Media,公有領域

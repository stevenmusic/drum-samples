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

`dw-kick-roomy-*` 另外做過小喇叭補強:大鼓的能量幾乎都在低頻,手機/筆電喇叭放不出來,聽起來會比小鼓小聲很多。
所以在 300Hz 加 +6dB(Q 0.9,補上小喇叭聽得到的「咚」聲)、整體 ×1.5,再用快速限幅器把峰值壓回 0.5,
力度層之間的差異(v3 比 v4 約 −5 LU、v5 約 +2 LU)維持不變。

### Hi-Hat(`web/drs-*.flac`)

取自 [DRSKit](https://github.com/sfzinstruments/DrumGizmo.DRSKit)(DrumGizmo 團隊 × DRSDrums 的 Jes Eiler,
作者 Lars Muldjord / Bent Bisballe Nyeng,**CC-BY 4.0**)的 Paiste hi-hat 多麥克風錄音:

| 檔名 | 內容 | round-robin |
|---|---|---|
| `drs-hhclosed` | 閉合 Hi-Hat | 3 |
| `drs-hhpedal` | 踩 Hi-Hat | 2 |
| `drs-hhopen` | 半開 Hi-Hat(semi open) | 3 |

每一下都由 hi-hat 近距麥克風 + overhead L/R + 房間麥克風 L/R 混成立體聲(overhead、房間麥克風先依互相關時間對齊到近距麥克風,避免梳狀濾波),
左右 RMS 拉平(位置由 ScrollScore 的聲像決定),44.1k → 48k,前導靜音裁到主要擊打瞬間前 2ms,依實測響度選出三個力度層並把同層 round-robin 響度對齊。

原本用 OSDK 的 hi-hat,但那組錄音每一下的擊打瞬間差異很大(峰值忽高忽低 5–10dB、衰減 80–300ms),聽起來一下正常一下怪,所以換掉。

### 銅鈸、邊擊(`web/osdk-*.flac`)

原始 WAV 沒有銅鈸,這部分取自 [THE OPEN SOURCE DRUM KIT](https://github.com/crabacus/the-open-source-drumkit)(Real Music Media,公有領域 public domain),
跟 DW/Keplinger 一樣是錄音室單擊取樣:

| 檔名 | 內容 | round-robin |
|---|---|---|
| `osdk-ride` | Ride(鈸面) | 3 |
| `osdk-ridebell` | Ride 鈴心 | 2 |
| `osdk-crash` | Crash | 2 |
| `osdk-sidestick` | 小鼓邊擊(cross stick) | 4 |

處理方式:依實測響度(LUFS)分成 `v3`/`v4`/`v5` 三個力度層(步距 −8.5 / −3.5 / 0 LU,對齊 DW 鼓組),
優先挑擊打瞬間(crest factor)一致的錄音,同層 round-robin 響度對齊;ride/crash 左右 RMS 拉平;
96kHz 降到 48kHz、整體音量調到 v5 峰值約 0.5(跟 DW 鼓組相同),銅鈸長尾巴裁到 1.5–2.6 秒並淡出,轉 16-bit FLAC。

DW/Keplinger 各層的 round-robin 也做過響度對齊(±3dB 內),`dw-rack-roomy` 的 v5 層另外 +2.5dB(原始錄音 v5 幾乎沒有比 v4 大聲)。

## 授權

- `DW Kick/`、`Keplinger Snare/`、`DW Rack/`、`DW Floor/` 及對應的 `web/dw-*`、`web/keplinger-*`:
  indiedrums「[DW Collectors Kit + Keplinger Snare](https://www.indiedrums.com/product/dw-collectors/)」免費鼓組取樣
- `web/drs-*`:DRSKit by DrumGizmo(Lars Muldjord / Bent Bisballe Nyeng)& Jes Eiler / DRSDrums,CC-BY 4.0,sfz 版由 kinwie 整理
- `web/osdk-*`:THE OPEN SOURCE DRUM KIT by Real Music Media,公有領域

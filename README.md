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

(舊版 ScrollScore 使用 `roomy` 收音,現已改用 DRSKit 整套鼓。)

`dw-kick-roomy-*` 另外做過小喇叭補強:大鼓的能量幾乎都在低頻,手機/筆電喇叭放不出來,聽起來會比小鼓小聲很多。
所以在 300Hz 加 +6dB(Q 0.9,補上小喇叭聽得到的「咚」聲)、整體 ×1.5,再用快速限幅器把峰值壓回 0.5,
力度層之間的差異(v3 比 v4 約 −5 LU、v5 約 +2 LU)維持不變。

### ScrollScore 目前使用:DRSKit 整套鼓(`web/drs-*.flac`)

整組鼓全部取自同一套實錄 [DRSKit](https://github.com/sfzinstruments/DrumGizmo.DRSKit)(DrumGizmo 團隊 × DRSDrums 的 Jes Eiler,
作者 Lars Muldjord / Bent Bisballe Nyeng,**CC-BY 4.0**):同一場錄音、同一個房間、同一組 13 支麥克風。
之前大鼓/小鼓/中鼓(DW/Keplinger)、hi-hat、銅鈸分別來自三套不同的鼓,各自的房間與麥克風都不同,合在一起聽得出是拼起來的。

| 檔名 | DRSKit 原始擊法 | round-robin |
|---|---|---|
| `drs-kick` | Kdrum_with_contact | 4 |
| `drs-snare` | Snare | 4 |
| `drs-xstick` | Snare_rim(邊擊) | 3 |
| `drs-tom1` / `drs-tom2` / `drs-tom3` | Tom1(中鼓)/ Tom2、Tom3(落地鼓) | 3 |
| `drs-hhclosed` / `drs-hhpedal` / `drs-hhopen` | Hihat_closed / Hihat_foot / Hihat_semi_open | 3 / 2 / 3 |
| `drs-ride` / `drs-ridebell` | Ride_tip / Ride_shank_bell | 3 |
| `drs-crashl` / `drs-crashr` | Crash_left_shank / Crash_right_shank | 2 |

**同一套混音配方**:每一下 = 該鼓件近距麥克風(依鼓手視角擺左右)+ 所有鼓件共用、同音量的 overhead L/R(0.7)與房間麥克風 L/R(0.35)。
大鼓前後麥克風、小鼓上下麥克風自動檢查極性(小鼓下方麥克風反相)。銅鈸只有間隔很開的 overhead,收窄 side 到 0.5 避免手機單聲道喇叭抵消。
44.1k → 48k、前導靜音裁到主要擊打瞬間前 2ms。

**力度層**:依實測響度分 `v3`/`v4`/`v5`(−8.5 / −3.5 / 0 LU),每層用窮舉組合挑出「增益對齊後峰值差最小、亮度一致(依響度回歸)、響度最接近目標」的錄音;
錄音數不夠的輕力度層(邊擊、踩 hi-hat、ride bell)沿用上一層錄音調小聲。v5 峰值統一約 0.5。

### (舊版,已不使用)OSDK 銅鈸、邊擊(`web/osdk-*.flac`)

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

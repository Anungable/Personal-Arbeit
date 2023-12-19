## MC 鳥籠形電子圍籬

### 適用飛行模式

Position, sport

### 啟動方式

GCS上輸入以下參數，只有在兩個參數都有設定的情況下才會啟動。

- `GF_ACTION`
- `GF_MAX_HOR_DIST`

### 注意事項

1. 目前可使用的`GF_ACTION`
   - Hold：沒有真的進到hold mode，確保failsafe情況下也不會指令鎖死
   - Land：Landing模式下RC依然可以打指令，須注意超界
2. geofence啟動判定和頭向及邊界距離有關，若離邊界近時速度太快會來不急煞車導致超界：
   - 可縮小geofence設定半徑避免超出 (z.B, 期望100m，可以設95m)。
   - 軟模擬下最多超界2m (最大速度20m/s情況下)，實機狀況尚須測試。

---

geofence功能self-check：

- [x] 不同速度飛行結果 (6, 15, 20m/s)
- [ ] 不同鳥籠半徑：確認半徑太小情況＋是否限制最小半徑？
- [ ] `gf_action` 0,2,5 確認
- [x] code check & improved
- [ ] 確認是否會覆蓋failsafe action：初步check不會


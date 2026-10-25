# Traffic API Lab: 10 Most Common Vehicles by Bluetooth MAC

**Data:** `bt_log202505.csv` (May 2025): 136,711 Bluetooth sightings, 120,897 different MACs.

## Method
1. Loaded the CSV and grouped sightings by MAC address.
2. Ranked MACs by **number of different days seen** (not raw sightings), so a device parked near the sensor for one day doesn't rank high, and rotating phone addresses drop out because they never repeat.
3. For each top MAC, called `/logs` on both cameras (`109_high`, `109_low`) and kept the one with the smallest `delta_seconds`.
4. Kept only matches with `delta_seconds` ≤ 3 s, since larger gaps often showed a different car. Downloaded up to 4 photos per MAC from different days with `/images`.
5. Compared the photos by eye.

## Results

| Rank | MAC | Days seen | Sightings | Usual hour | Verdict |
|---|---|---|---|---|---|
| 1 | `a0:0b:16:04:85:16` | 28.0 | 141.0 | 11:00 | ✅ Same vehicle: dark gray Tesla Model Y (4/4 photos). Mostly ~7:15-7:40 am. |
| 2 | `80:c4:1b:7b:6a:ff` | 27.0 | 67.0 | 12:00 | ✅ Likely same: black Volvo XC90 (3/4 photos). Mismatch photo shows a dark SUV behind a dump truck. |
| 3 | `d4:ad:fc:20:f1:40` | 25.0 | 50.0 | 7:00 | ⚠️ Probably a dark SUV around 7:05 am (2-3/4 photos); one photo is a red sedan. |
| 4 | `d0:2e:ab:ef:b8:dd` | 23.0 | 51.0 | 14:00 | ✅ Likely same: dark Tesla Model Y (3/4 photos). Note #1 is also a dark Model Y - on May 7 both passed 6 minutes apart. |
| 5 | `a0:76:4e:f3:2a:39` | 21.0 | 37.0 | 8:00 | ✅ Same vehicle: white Ram pickup (4/4 photos). Mornings 7-9 am. |
| 6 | `df:ed:79:f3:7b:b0` | 20.0 | 36.0 | 12:00 | ❓ Unconfirmed: usually seen ~6:20-6:50 am when the camera recorded no vehicles (nearest detection 10-40 min away). The 2 close matches show different vehicles (gray Jeep Patriot, blue Toyota 4Runner). |
| 7 | `40:79:12:87:52:0a` | 20.0 | 33.0 | 10:00 | ✅ Likely same: white Volvo XC60 (3/4 photos). Mismatch is a Budget truck (delta 2.5 s). |
| 8 | `a2:07:00:05:38:86` | 19.0 | 26.0 | 16:00 | ✅ Likely same: dark pickup (3/4 photos). Mismatch is a red Jeep Wrangler. |
| 9 | `ef:70:09:a5:3b:ae` | 18.0 | 63.0 | 15:00 | ✅ Likely same: white Toyota Corolla hatchback (3/4 photos). |
| 10 | `dd:45:a9:90:84:41` | 18.0 | 43.0 | 13:00 | ⚠️ Possibly a delivery vehicle: white box truck at ~10:05 am on two days; other photos show a white van and a dark SUV. |

## Observations
- Most confirmed vehicles are Teslas and Volvos, which use the owner's phone as a Bluetooth key, so they likely broadcast a fixed address constantly.
- About 1 in 4 photos showed a different vehicle even when the delta was small, because the sensor can hear a car while another one is in front of the camera.
- #6 shows the camera seems to record no vehicles before about 7 am, so early commuters are hard to confirm.
- #1 and #4 are both dark Tesla Model Ys with different MACs: either two similar cars or one car with two Bluetooth radios.

## Photos

### #1 `a0:0b:16:04:85:16`

✅ Same vehicle: dark gray Tesla Model Y (4/4 photos). Mostly ~7:15-7:40 am.

<img src="images/01_a00b16048516/20250506_071617.jpg" width="300" title="2025-05-06T07:16:17 (delta 0.0 s)">
<img src="images/01_a00b16048516/20250507_073837.jpg" width="300" title="2025-05-07T07:38:37 (delta 0.5 s)">
<img src="images/01_a00b16048516/20250516_120046.jpg" width="300" title="2025-05-16T12:00:46 (delta 0.6 s)">
<img src="images/01_a00b16048516/20250520_073706.jpg" width="300" title="2025-05-20T07:37:06 (delta 1.13 s)">

### #2 `80:c4:1b:7b:6a:ff`

✅ Likely same: black Volvo XC90 (3/4 photos). Mismatch photo shows a dark SUV behind a dump truck.

<img src="images/02_80c41b7b6aff/20250504_125256.jpg" width="300" title="2025-05-04T12:52:56 (delta 0.662 s)">
<img src="images/02_80c41b7b6aff/20250505_094449.jpg" width="300" title="2025-05-05T09:44:49 (delta 0.5 s)">
<img src="images/02_80c41b7b6aff/20250506_164500.jpg" width="300" title="2025-05-06T16:45:00 (delta 0.6 s)">
<img src="images/02_80c41b7b6aff/20250516_171812.jpg" width="300" title="2025-05-16T17:18:12 (delta 0.17 s)">

### #3 `d4:ad:fc:20:f1:40`

⚠️ Probably a dark SUV around 7:05 am (2-3/4 photos); one photo is a red sedan.

<img src="images/03_d4adfc20f140/20250502_070335.jpg" width="300" title="2025-05-02T07:03:35 (delta 0.052 s)">
<img src="images/03_d4adfc20f140/20250504_101824.jpg" width="300" title="2025-05-04T10:18:24 (delta 0.04 s)">
<img src="images/03_d4adfc20f140/20250505_070501.jpg" width="300" title="2025-05-05T07:05:01 (delta 0.4 s)">
<img src="images/03_d4adfc20f140/20250506_070740.jpg" width="300" title="2025-05-06T07:07:40 (delta 0.5 s)">

### #4 `d0:2e:ab:ef:b8:dd`

✅ Likely same: dark Tesla Model Y (3/4 photos). Note #1 is also a dark Model Y - on May 7 both passed 6 minutes apart.

<img src="images/04_d02eabefb8dd/20250502_173001.jpg" width="300" title="2025-05-02T17:30:01 (delta 0.5 s)">
<img src="images/04_d02eabefb8dd/20250505_144817.jpg" width="300" title="2025-05-05T14:48:17 (delta 0.6 s)">
<img src="images/04_d02eabefb8dd/20250506_133406.jpg" width="300" title="2025-05-06T13:34:06 (delta 0.2 s)">
<img src="images/04_d02eabefb8dd/20250507_073221.jpg" width="300" title="2025-05-07T07:32:21 (delta 0.57 s)">

### #5 `a0:76:4e:f3:2a:39`

✅ Same vehicle: white Ram pickup (4/4 photos). Mornings 7-9 am.

<img src="images/05_a0764ef32a39/20250502_071035.jpg" width="300" title="2025-05-02T07:10:35 (delta 0.44 s)">
<img src="images/05_a0764ef32a39/20250503_082349.jpg" width="300" title="2025-05-03T08:23:49 (delta 0.6 s)">
<img src="images/05_a0764ef32a39/20250505_075925.jpg" width="300" title="2025-05-05T07:59:25 (delta 0.06 s)">
<img src="images/05_a0764ef32a39/20250506_085710.jpg" width="300" title="2025-05-06T08:57:10 (delta 0.052 s)">

### #6 `df:ed:79:f3:7b:b0`

❓ Unconfirmed: usually seen ~6:20-6:50 am when the camera recorded no vehicles (nearest detection 10-40 min away). The 2 close matches show different vehicles (gray Jeep Patriot, blue Toyota 4Runner).

<img src="images/06_dfed79f37bb0/20250529_155851.jpg" width="300" title="2025-05-29T15:58:51 (delta 0.0 s)">
<img src="images/06_dfed79f37bb0/20250511_135237.jpg" width="300" title="2025-05-11T13:52:37 (delta 4.5 s)">

### #7 `40:79:12:87:52:0a`

✅ Likely same: white Volvo XC60 (3/4 photos). Mismatch is a Budget truck (delta 2.5 s).

<img src="images/07_40791287520a/20250503_132921.jpg" width="300" title="2025-05-03T13:29:21 (delta 0.37 s)">
<img src="images/07_40791287520a/20250505_160642.jpg" width="300" title="2025-05-05T16:06:42 (delta 0.07 s)">
<img src="images/07_40791287520a/20250527_070230.jpg" width="300" title="2025-05-27T07:02:30 (delta 2.5 s)">
<img src="images/07_40791287520a/20250531_104253.jpg" width="300" title="2025-05-31T10:42:53 (delta 0.76 s)">

### #8 `a2:07:00:05:38:86`

✅ Likely same: dark pickup (3/4 photos). Mismatch is a red Jeep Wrangler.

<img src="images/08_a20700053886/20250501_084031.jpg" width="300" title="2025-05-01T08:40:31 (delta 0.06 s)">
<img src="images/08_a20700053886/20250502_073647.jpg" width="300" title="2025-05-02T07:36:47 (delta 0.15 s)">
<img src="images/08_a20700053886/20250507_164509.jpg" width="300" title="2025-05-07T16:45:09 (delta 1.0 s)">
<img src="images/08_a20700053886/20250508_074843.jpg" width="300" title="2025-05-08T07:48:43 (delta 0.1 s)">

### #9 `ef:70:09:a5:3b:ae`

✅ Likely same: white Toyota Corolla hatchback (3/4 photos).

<img src="images/09_ef7009a53bae/20250502_143329.jpg" width="300" title="2025-05-02T14:33:29 (delta 0.6 s)">
<img src="images/09_ef7009a53bae/20250503_150721.jpg" width="300" title="2025-05-03T15:07:21 (delta 0.0 s)">
<img src="images/09_ef7009a53bae/20250506_102550.jpg" width="300" title="2025-05-06T10:25:50 (delta 0.4 s)">
<img src="images/09_ef7009a53bae/20250507_084849.jpg" width="300" title="2025-05-07T08:48:49 (delta 0.35 s)">

### #10 `dd:45:a9:90:84:41`

⚠️ Possibly a delivery vehicle: white box truck at ~10:05 am on two days; other photos show a white van and a dark SUV.

<img src="images/10_dd45a9908441/20250501_161458.jpg" width="300" title="2025-05-01T16:14:58 (delta 0.152 s)">
<img src="images/10_dd45a9908441/20250502_100539.jpg" width="300" title="2025-05-02T10:05:39 (delta 0.83 s)">
<img src="images/10_dd45a9908441/20250505_100855.jpg" width="300" title="2025-05-05T10:08:55 (delta 0.05 s)">
<img src="images/10_dd45a9908441/20250506_102545.jpg" width="300" title="2025-05-06T10:25:45 (delta 0.6 s)">

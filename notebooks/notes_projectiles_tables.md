Unusual values in effective_range wh2_main_lzd_cav_cold_ones_feral_0_summoned



effective_range
      1
-1    1
Name: count, dtype: int64

Q: What could -1 possibly mean?

---

Practical intuition:

Higher calibration_distance = stays accurate farther out (good for guns / precise artillery).

Lower calibration_distance = starts getting “spray-y” sooner (common for crude artillery, lobbers, etc.).

Practical intuition:

Lower calibration_area = sniper-like consistency.

Higher calibration_area = wider scatter (good if you want “area suppression,” bad if you want deletes on single entities).

Rule of thumb combo

“Accurate long range” projectile: high calibration_distance + low calibration_area

“Inaccurate / lobbed / splashy” projectile: low calibration_distance + high calibration_area
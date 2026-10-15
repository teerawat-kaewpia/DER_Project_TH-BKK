# Correction: C2 poverty input builder (2026-10-09)

`Scripts/02_Preprocessing/build_c2_poverty_province.py` inside `Scripts_DER_TH_BKK.zip` (release
V1.0.0) joined NESDC Table 1.5 (poverty incidence by province, edition 2567) to GADM 4.1 on the GADM
Thai name `NL_NAME_1`. GADM 4.1 carries the wrong Thai name for two provinces:

| GADM `NAME_1` | GADM `NL_NAME_1` | C2 produced by V1.0.0 | Correct value (Table 1.5, 2565) |
|---|---|---|---|
| Bangkok Metropolis | จังหวัดเชียงใหม่ (Chiang Mai) | 3.0853% (Chiang Mai) | 1.3686% |
| Chaiyaphum | จังหวัดชัยนาท (Chai Nat) | 15.2575% (Chai Nat) | 1.1748% |

An independent join on a Thai-to-English province dictionary found these two differences and no
others among the 77 provinces.

This commit replaces the builder in the zip with a version that joins on an explicit Thai → GADM
English dictionary and asserts a one-to-one match. Run against the source workbook, it reproduces the
corrected values exactly. The compiled copy of the old builder (`__pycache__/...pyc`) is removed. All
other files in the zip are unchanged.

Results computed with V1.0.0 (the withdrawn Sustainable Cities and Society version) used the faulty
values. Main effects of the correction: equity weight 0.3325 → 0.3425, equity vs efficiency-only
ρ −0.391 → −0.394, Zone 1 6 → 7 provinces (Narathiwat added), Chaiyaphum rank 7 → 62, Bangkok rank
14 → 22.

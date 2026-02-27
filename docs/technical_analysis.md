# Technical Analysis and Design Justification

## 1. Justification for Differential Pressure Sensor

Human respiration generates small pressure variations during inhalation and exhalation. 
Typical breathing pressure ranges approximately within ±1 to ±2 kPa under normal conditions.

A differential pressure sensor (such as MPXV7002DP) is suitable because:

- It directly measures pressure difference between two ports (useful for inhale/exhale detection).
- It provides a continuous analog voltage proportional to airflow-induced pressure.
- It captures waveform dynamics required for respiratory rate calculation.
- It is more appropriate for breath waveform detection than gas sensors (e.g., MQ series), which measure gas concentration rather than airflow dynamics.

Thus, differential pressure sensing enables real-time breath pattern acquisition.

---

## 2. Justification for External ADC (ADS1115)

Although the ESP32 has an internal ADC, it has known limitations:

- Non-linearity in ADC response.
- Higher noise levels.
- Limited effective resolution in practice.

Respiratory pressure signals are small and require accurate waveform detection. 
A 16-bit external ADC such as ADS1115 offers:

- Higher resolution for small voltage changes.
- Programmable gain amplifier (PGA) for better signal scaling.
- Improved measurement stability via I2C communication.

Using an external ADC improves signal accuracy and enhances reliability of respiratory rate detection.

---

## 3. Expected Signal Estimation and Amplifier Planning

Assume a normal breathing pressure variation of approximately ±1 kPa.

For a typical differential pressure sensor:
- Sensitivity ≈ 1 V per kPa (approximate for estimation).

Therefore:
- ±1 kPa → approximately ±1 V output swing (centered around offset voltage).

To fully utilize ADC input range (0–3.3 V), amplification may be applied.

If raw signal swing ≈ 1 V,
Applying gain ≈ 2 to 3 would scale signal close to 2–3 V range,
while ensuring it does not exceed 3.3 V input limit.

This amplified signal can then be accurately digitized using a 16-bit ADC.

---

## 4. Sampling Rate Consideration

Human breathing frequency typically ranges from:
- 12–20 breaths per minute (0.2–0.33 Hz).

To capture waveform shape properly, a sampling rate of:
- 50–200 samples per second

is sufficient for reliable respiratory signal acquisition and peak detection.

---

## 5. Basic Signal Processing Plan

After ADC conversion:

- Apply low-pass filtering (cutoff ~5 Hz) to remove high-frequency noise.
- Perform peak detection to identify inhale/exhale cycles.
- Compute respiratory rate from time difference between peaks.

This approach enables real-time breath monitoring and future AI integration.

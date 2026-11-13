<img width="957" height="433" alt="image" src="https://github.com/user-attachments/assets/52833c84-1341-468f-814e-94f162783481" /># nasa-airfoil-noise-regression
Multiple Linear Regression analysis on NASA Airfoil Self-Noise dataset with domain-specific anomaly handling

Latar Belakang
Proyek ini bertujuan untuk memodelkan tingkat kebisingan (*Scaled Sound Pressure Level*) yang dihasilkan oleh sayap pesawat (*airfoil*) berdasarkan parameter aerodinamis. Dataset yang digunakan adalah dataset eksperimen NASA yang diambil dari UCI Machine Learning Repository.

## Metodologi
1. **Domain-Specific Anomaly Detection:** Mengidentifikasi kondisi *stall* (AoA > 15°) dan *early flow separation* menggunakan rasio displacement thickness.
2. **Feature Engineering:** 
   - Mengubah kondisi *stall* menjadi variabel dummy (`is_stall`).
   - Menormalkan distribusi rasio lapisan batas menggunakan log-transformation (`log_delta`).
3. **Modeling:** Menggunakan *Ordinary Least Squares* (OLS) Multiple Linear Regression.
4. **Diagnostics & Fixes:** 
   - Mengatasi *ill-conditioning* (Condition Number tinggi) dengan `StandardScaler`.
   - Mengatasi autokorelasi (Durbin-Watson rendah) dengan *data shuffling*.
   - Memastikan bebas multikolinearitas mutlak (VIF < 5).

## Key Insights
- Model akhir memiliki **R-squared sebesar 49.8%**, yang sangat baik untuk data eksperimen fisik.
- Variabel **frekuensi** dan **chord-length** memiliki pengaruh negatif paling kuat terhadap kebisingan.
- Terjadi fenomena *spectral shift*: kondisi *stall* (`is_stall`) menurunkan tingkat kebisingan pada frekuensi tinggi, mengindikasikan pergeseran energi suara ke frekuensi rendah.
- Terdapat fenomena *regression to the mean* pada prediksi, di mana model kesulitan menebak nilai ekstrem (mengindikasikan hubungan non-linear seperti hukum pangkat kecepatan (U^5).

## 🚀 Cara Menjalankan
Buka file `airfoil_regression_analysis.ipynb` menggunakan Google Colab atau Jupyter Notebook. Seluruh kode dapat dijalankan dari atas ke bawah (Run All) tanpa error

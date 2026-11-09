# PSIB2026Q2-TPS-Grupo03-Cendoya Sanchez Tobal

Trabajo Práctico de Señales (TPS) de **16.63 Procesamiento de Señales e Imágenes Biomédicas** (ITBA, 2.º cuatrimestre 2026).

**Evaluación de técnicas de filtrado para la reducción de interferencias magnetohidrodinámicas en señales de ECG adquiridas durante resonancia magnética.**

Integrantes: Cendoya, Sanchez, Tobal.

## Descripción

Durante una resonancia magnética, el flujo de sangre dentro del campo magnético genera un voltaje adicional (efecto magnetohidrodinámico, MHD) que se superpone al ECG y distorsiona sobre todo la onda T y el segmento ST. Como la interferencia ocurre en cada latido y comparte frecuencias con el ECG, no puede eliminarse con un filtro convencional.

En este trabajo se comparan filtros convencionales (FIR e IIR) con estrategias de filtrado óptimo (filtro de Wiener y resta de plantillas) y se evalúa su efecto sobre la morfología del ECG y la detección de complejos QRS (Pan–Tompkins).

## Dataset

[Influence of the MHD effect on 12-lead and 3-lead ECGs recorded in 1T to 7T MRI scanners](https://physionet.org/content/mhd-effect-ecg-mri/1.0.0/) (PhysioNet, v1.0.0):

- 53 registros de 23 sujetos sanos: 43 dentro del resonador (1 T, 3 T y 7 T) y 10 de referencia fuera del resonador.
- Frecuencia de muestreo de 1024 Hz, con ECG de 3 y 12 derivaciones.
- Cada registro tiene su señal (`.dat`), encabezado (`.hea`) y anotaciones manuales de QRS (`.qrs`).

El dataset está incluido en la carpeta `Data`. Para descargarlo de nuevo:

    python -c "import wfdb; wfdb.dl_database('mhd-effect-ecg-mri', dl_dir='Data')"

## Instalación

Requiere Python 3.10 o superior.

    python -m venv .venv
    source .venv/bin/activate        # En Windows: .venv\Scripts\activate
    pip install -r requirements.txt

## Ejecución


## Referencias

- Krug Passand, J. W. (2021). Influence of the MHD effect on 12-lead and 3-lead ECGs recorded in 1T to 7T MRI scanners (v1.0.0). PhysioNet. https://doi.org/10.13026/05td-jn37
- Krug, J. W., Schmidt, M., Rose, G., y Friebe, M. (2017). A database of electrocardiogram signals acquired in different magnetic resonance imaging scanners. *Computing in Cardiology*.
- Krug, J. W., y Rose, G. (2011). Magnetohydrodynamic distortions of the ECG in different MR scanner configurations. *Computing in Cardiology*, 38, 769–772.
- Krug, J. W., Clifford, G. D., Rose, G., y Oster, J. (2012). The limited applicability of Wiener filtering to ECG signals disturbed by the MHD effect. *20th European Signal Processing Conference (EUSIPCO)*.
- Krug, J. W., Rose, G., Clifford, G. D., y Oster, J. (2013). ECG-based gating in ultra high field cardiovascular magnetic resonance using an independent component analysis approach. *Journal of Cardiovascular Magnetic Resonance*, 15, 104.
- Gregory, T. S., Wu, K. J., Schmidt, E. J., Oshinski, J., y Tse, Z. T. (2016). Intra-MRI extraction of diagnostic electrocardiograms using dynamic feedback from carotidal magnetohydrodynamic voltages. *Journal of Cardiovascular Magnetic Resonance*, 18(Supl. 1), P214.
- Oster, J., Llinares, R., Payne, S., Tse, Z. T. H., Schmidt, E. J., y Clifford, G. D. (2015). Comparison of three artificial models of the magnetohydrodynamic effect on the electrocardiogram. *Computer Methods in Biomechanics and Biomedical Engineering*, 18(13), 1400–1417.
- Pan, J., y Tompkins, W. J. (1985). A real-time QRS detection algorithm. *IEEE Transactions on Biomedical Engineering*, 32(3), 230–236.
- Welch, P. D. (1967). The use of fast Fourier transform for the estimation of power spectra: A method based on time averaging over short, modified periodograms. *IEEE Transactions on Audio and Electroacoustics*, 15(2), 70–73. https://doi.org/10.1109/TAU.1967.1161901
- Harris, F. J. (1978). On the use of windows for harmonic analysis with the discrete Fourier transform. *Proceedings of the IEEE*, 66(1), 51–83. https://doi.org/10.1109/PROC.1978.10837
- Ishmakhametov, N., Naser, M. Y. M., Kelil, S. B., McClary, C., Metcalfe, J. S., y Bhattacharya, S. (2026). A multimodal dataset for emotional transition analysis in virtual reality. *Scientific Data*, 13, 1158. https://doi.org/10.1038/s41597-026-07456-0
- Abi-Abdallah, D., Robin, V., Drochon, A., y Fokapu, O. (2007). Alterations in human ECG due to the magnetohydrodynamic effect: A method for accurate R peak detection in the presence of high MHD artifacts. *29th Annual International Conference of the IEEE Engineering in Medicine and Biology Society*, 1842–1845. https://doi.org/10.1109/IEMBS.2007.4352673
- Yáñez de la Rivera, R., Soto-Bajo, M., y Fraguela-Collar, A. (2018). Electrocardiogram fiducial points detection and estimation methodology for automatic diagnose. *The Open Bioinformatics Journal*, 11, 208–230. https://doi.org/10.2174/1875036201811010208
- Buelga Suárez, M. L., Recas, J., González-Cabeza, S., Sanz-Guerrero, M., Diaz-Vicente, M., Rebolleda Sánchez, A., Piñuel, L., y Alonso Salinas, G. L. (2026). Performance evaluation of smartwatches: Can they match clinical standards for ECG analysis? *Biomedical Signal Processing and Control*, 115, 109373. https://doi.org/10.1016/j.bspc.2025.109373
- Task Force of the European Society of Cardiology and the North American Society of Pacing and Electrophysiology (1996). Heart rate variability: Standards of measurement, physiological interpretation, and clinical use. *European Heart Journal*, 17(3), 354–381. [PDF completo](https://motricidadehumana.org/wp-content/uploads/2016/05/guidelines-heart-rate-variability-ft-1996.pdf).
- Clifford, G. D., y Tarassenko, L. (2005). Quantifying errors in spectral estimates of HRV due to beat replacement and resampling. *IEEE Transactions on Biomedical Engineering*, 52(4), 630–638. https://doi.org/10.1109/TBME.2005.844028
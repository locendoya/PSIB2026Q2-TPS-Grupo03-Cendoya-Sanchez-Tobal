# PSIB2026Q2-TPS-Grupo03-Cendoya Sanchez Tobal

Trabajo Práctico de Señales (TPS) de **16.63 Procesamiento de Señales e Imágenes Biomédicas** (ITBA, 2.º cuatrimestre 2026).

**Evaluación de técnicas de filtrado para la reducción de interferencias magnetohidrodinámicas en señales de ECG adquiridas durante resonancia magnética.**

Integrantes: Cendoya, Sanchez, Tobal.

## Descripción

Durante una resonancia magnética, el flujo de sangre dentro del campo magnético genera un voltaje adicional (efecto magnetohidrodinámico, MHD) que se superpone al ECG y distorsiona sobre todo la onda T y el segmento ST. Como la interferencia ocurre en cada latido y comparte frecuencias con el ECG, no puede eliminarse con un filtro convencional.

En este trabajo se comparan filtros convencionales (FIR e IIR), el filtro de Wiener en frecuencia y dos correcciones latido a latido (resta de plantilla y Wiener en el tiempo). Se evalúa su efecto sobre la morfología del ECG, la detección de complejos QRS (Pan–Tompkins) y la variabilidad de la frecuencia cardíaca.

## Dataset

[Influence of the MHD effect on 12-lead and 3-lead ECGs recorded in 1T to 7T MRI scanners](https://physionet.org/content/mhd-effect-ecg-mri/1.0.0/) (PhysioNet, v1.0.0):

- 53 registros de 23 sujetos sanos: 43 dentro del resonador (1 T, 3 T y 7 T) y 10 de referencia fuera del resonador.
- Frecuencia de muestreo de 1024 Hz, con ECG de 3 y 12 derivaciones.
- Cada registro tiene su señal (`.dat`), encabezado (`.hea`) y anotaciones manuales de QRS (`.qrs`).
- Los registros de 7T04 son un duplicado de 3T01 y se excluyen. Quedan 50 registros válidos y 9 sujetos con registros dentro y fuera del resonador.

El dataset está incluido en la carpeta `Data`. Para descargarlo de nuevo:

    python -c "import wfdb; wfdb.dl_database('mhd-effect-ecg-mri', dl_dir='Data')"

## Instalación

Requiere Python 3.10 o superior.

    python -m venv .venv
    source .venv/bin/activate        # En Windows: .venv\Scripts\activate
    pip install -r requirements.txt

## Ejecución

1. Abrir `Pipeline_TPS.ipynb` en VS Code o Jupyter, con la carpeta `Data` en la misma carpeta que el notebook.
2. Seleccionar como kernel el entorno `.venv`.
3. Ejecutar todas las celdas en orden (Run All). La ejecución completa tarda unos minutos.

El notebook está organizado en nueve secciones:

1. Carga y caracterización de los registros
2. Caracterización temporal y frecuencial
3. Preprocesamiento con filtros convencionales (FIR de Kaiser e IIR Butterworth)
4. Filtro de Wiener en frecuencia
5. Detección de QRS con Pan–Tompkins y elección de la derivación
6. Correcciones latido a latido (resta de plantilla y Wiener en el tiempo)
7. Evaluación de la morfología y de la detección después de la corrección
8. Variabilidad de la frecuencia cardíaca (análisis temporal y espectral)
9. Conclusiones generales

## Resultados principales

- El pasabanda de 0,67–40 Hz no elimina el MHD: el exceso de potencia dentro del resonador se concentra en 0,67–10 Hz, la misma banda que la onda T y el ST.
- Wiener en frecuencia atenúa de más el ECG, pero mejora la detección de QRS: F1 de 0,86 contra 0,66 con FIR, en la derivación con los RR más regulares.
- Con R detectados, Wiener en el tiempo obtuvo la mejor detección después de la corrección (F1 = 0,898) y el menor error en el ST (0,033 mV en mediana).
- La resta de plantilla recupera casi todo el latido si los latidos están bien ubicados (correlación mediana de 0,974 con R anotados), pero se degrada con los R detectados.
- Los índices de variabilidad cardíaca calculados con R detectados tienen errores del mismo orden que los propios índices.

## Referencias

- Clifford, G. D., y Tarassenko, L. (2005). Quantifying errors in spectral estimates of HRV due to beat replacement and resampling. *IEEE Transactions on Biomedical Engineering*, 52(4), 630–638. https://doi.org/10.1109/TBME.2005.844028
- Goldberger, A. L., Amaral, L. A. N., Glass, L., Hausdorff, J. M., Ivanov, P. Ch., Mark, R. G., Mietus, J. E., Moody, G. B., Peng, C.-K., y Stanley, H. E. (2000). PhysioBank, PhysioToolkit, and PhysioNet: Components of a new research resource for complex physiologic signals. *Circulation*, 101(23), e215–e220.
- Gregory, T. S., Wu, K. J., Schmidt, E. J., Oshinski, J., y Tse, Z. T. (2016). Intra-MRI extraction of diagnostic electrocardiograms using dynamic feedback from carotidal magnetohydrodynamic voltages. *Journal of Cardiovascular Magnetic Resonance*, 18(Supl. 1), P214.
- Harris, F. J. (1978). On the use of windows for harmonic analysis with the discrete Fourier transform. *Proceedings of the IEEE*, 66(1), 51–83. https://doi.org/10.1109/PROC.1978.10837
- Krug, J. W., Clifford, G. D., Rose, G., y Oster, J. (2012). The limited applicability of Wiener filtering to ECG signals disturbed by the MHD effect. *20th European Signal Processing Conference (EUSIPCO)*.
- Krug, J. W., Rose, G., Clifford, G. D., y Oster, J. (2013). ECG-based gating in ultra high field cardiovascular magnetic resonance using an independent component analysis approach. *Journal of Cardiovascular Magnetic Resonance*, 15, 104. https://doi.org/10.1186/1532-429X-15-104
- Krug, J. W., y Rose, G. (2011). Magnetohydrodynamic distortions of the ECG in different MR scanner configurations. *Computing in Cardiology*, 38, 769–772.
- Krug, J. W., Schmidt, M., Rose, G., y Friebe, M. (2017). A database of electrocardiogram signals acquired in different magnetic resonance imaging scanners. *Computing in Cardiology*.
- Krug Passand, J. W. (2021). Influence of the MHD effect on 12-lead and 3-lead ECGs recorded in 1T to 7T MRI scanners (v1.0.0). PhysioNet. https://doi.org/10.13026/05td-jn37
- Pan, J., y Tompkins, W. J. (1985). A real-time QRS detection algorithm. *IEEE Transactions on Biomedical Engineering*, 32(3), 230–236.
- Task Force of the European Society of Cardiology and the North American Society of Pacing and Electrophysiology (1996). Heart rate variability: Standards of measurement, physiological interpretation, and clinical use. *European Heart Journal*, 17(3), 354–381.
- Welch, P. D. (1967). The use of fast Fourier transform for the estimation of power spectra: A method based on time averaging over short, modified periodograms. *IEEE Transactions on Audio and Electroacoustics*, 15(2), 70–73. https://doi.org/10.1109/TAU.1967.1161901
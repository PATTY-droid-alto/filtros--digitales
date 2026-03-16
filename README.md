# filtros--digitales
Implementacion de filtros,pasa bajos,pasa altos y pasa banda
Startup execution:
  loading initial environment

--> Diseño y aplicacion de filtros FIR E IIR

Undefined variable: Diseño

--> clear;

--> clf;

--> 

--> // ============================================================

--> // 1. PARÁMETROS DE LA SEÑAL

--> // ============================================================

--> fs = 1000;               // Frecuencia de muestreo (Hz)

--> t = 0:1/fs:1-1/fs;       // Vector de tiempo (1 segundo)

--> N = length(t);            // Número de muestras

--> 

--> // ============================================================

--> // 2. GENERACIÓN DE SEÑALES DE PRUEBA

--> // ============================================================

--> f1 = 50; f2 = 150; f3 = 300;

--> 

--> // Señal limpia

--> senal_limpia = sin(2*%pi*f1*t) + 0.5*sin(2*%pi*f2*t) + 0.3*sin(2*%pi*f3*t);

--> 

--> // Ruido blanco

--> ruido = 0.5*rand(1,N,'normal');

--> 

--> // Señal con ruido

--> senal_con_ruido = senal_limpia + ruido;

--> 

--> // ============================================================

--> // 3. DISEÑO DE FILTROS USANDO FUNCIONES DE SCILAB

--> // ============================================================

--> 

--> // Normalizar frecuencias

--> fc_pb = 100/(fs/2);      // Pasa bajos

--> fc_pa = 200/(fs/2);      // Pasa altos

--> fc_banda = [100 250]/(fs/2); // Pasa banda

--> 

--> // Diseño de filtros Butterworth

--> orden = 4;

--> 

--> // Pasa Bajos

--> hz_pb = iir(orden, 'lp', 'butt', [fc_pb,0], [0,0]);

--> 

--> // Pasa Altos  

--> hz_pa = iir(orden, 'hp', 'butt', [fc_pa,0], [0,0]);

--> 

--> // Pasa Banda

--> hz_pbnd = iir(orden, 'bp', 'butt', fc_banda, [0,0]);

--> 

--> // ============================================================

--> // 4. APLICACIÓN DE FILTROS

--> // ============================================================

--> senal_filtrada_pb = flts(senal_con_ruido, hz_pb(2), hz_pb(3));
at line   103 of function flts ( C:\Program Files\scilab-2026.0.1\modules\cacsd\macros\flts.sci line 115 )

flts: Wrong type for input argument #2: Linear dynamical system expected.
--> senal_filtrada_pa = flts(senal_con_ruido, hz_pa(2), hz_pa(3));
at line   103 of function flts ( C:\Program Files\scilab-2026.0.1\modules\cacsd\macros\flts.sci line 115 )

flts: Wrong type for input argument #2: Linear dynamical system expected.
--> senal_filtrada_pbnd = flts(senal_con_ruido, hz_pbnd(2), hz_pbnd(3));
at line   103 of function flts ( C:\Program Files\scilab-2026.0.1\modules\cacsd\macros\flts.sci line 115 )

flts: Wrong type for input argument #2: Linear dynamical system expected.
--> 

--> // ============================================================

--> // 5. VISUALIZACIÓN EN TIEMPO

--> // ============================================================

--> scf(0);

--> 

--> subplot(3,2,1);

--> plot(t, senal_limpia, 'b');

--> title('Señal Original');

--> xlabel('Tiempo (s)');

--> ylabel('Amplitud');

--> xgrid();

--> 

--> subplot(3,2,2);

--> plot(t, senal_con_ruido, 'r');

--> title('Señal con Ruido');

--> xlabel('Tiempo (s)');

--> ylabel('Amplitud');

--> xgrid();

--> 

--> subplot(3,2,3);

--> plot(t, senal_filtrada_pb, 'g');

Undefined variable: senal_filtrada_pb

--> title('Filtro Pasa Bajos (fc=100Hz)');

--> xlabel('Tiempo (s)');

--> ylabel('Amplitud');

--> xgrid();

--> 

--> subplot(3,2,4);

--> plot(t, senal_filtrada_pa, 'm');

Undefined variable: senal_filtrada_pa

--> title('Filtro Pasa Altos (fc=200Hz)');

--> xlabel('Tiempo (s)');

--> ylabel('Amplitud');

--> xgrid();

--> 

--> subplot(3,2,5);

--> plot(t, senal_filtrada_pbnd, 'c');

Undefined variable: senal_filtrada_pbnd

--> title('Filtro Pasa Banda (100-250Hz)');

--> xlabel('Tiempo (s)');

--> ylabel('Amplitud');

--> xgrid();

--> 

--> // ============================================================

--> // 6. ANÁLISIS EN FRECUENCIA

--> // ============================================================

--> function Y = calc_fft(senal)
  >     N = length(senal);
  >     Y = abs(fft(senal))/N;
  >     Y = Y(1:floor(N/2)+1);
  >     Y(2:$-1) = 2*Y(2:$-1);
  > endfunction

--> 

--> f = (0:floor(N/2)) * fs / N;

--> 

--> Y_original = calc_fft(senal_limpia);

--> Y_ruido = calc_fft(senal_con_ruido);

--> Y_pb = calc_fft(senal_filtrada_pb);

Undefined variable: senal_filtrada_pb

--> Y_pa = calc_fft(senal_filtrada_pa);

Undefined variable: senal_filtrada_pa

--> Y_pbnd = calc_fft(senal_filtrada_pbnd);

Undefined variable: senal_filtrada_pbnd

--> 

--> scf(1);

--> 

--> subplot(3,2,1);

--> plot(f, Y_original, 'b');

--> title('Espectro Señal Original');

--> xlabel('Frecuencia (Hz)');

--> ylabel('Magnitud');

--> xgrid();

--> 

--> subplot(3,2,2);

--> plot(f, Y_ruido, 'r');

--> title('Espectro Señal con Ruido');

--> xlabel('Frecuencia (Hz)');

--> ylabel('Magnitud');

--> xgrid();

--> 

--> subplot(3,2,3);

--> plot(f, Y_pb, 'g');

Undefined variable: Y_pb

--> title('Espectro - Pasa Bajos');

--> xlabel('Frecuencia (Hz)');

--> ylabel('Magnitud');

--> xgrid();

--> 

--> subplot(3,2,4);

--> plot(f, Y_pa, 'm');

Undefined variable: Y_pa

--> title('Espectro - Pasa Altos');

--> xlabel('Frecuencia (Hz)');

--> ylabel('Magnitud');

--> xgrid();

--> 

--> subplot(3,2,5);

--> plot(f, Y_pbnd, 'c');

Undefined variable: Y_pbnd

--> title('Espectro - Pasa Banda');

--> xlabel('Frecuencia (Hz)');

--> ylabel('Magnitud');

--> xgrid();

--> 

--> // ============================================================

--> // 7. RESPUESTA EN FRECUENCIA DE LOS FILTROS

--> // ============================================================

--> scf(2);

--> 

--> // Respuesta del filtro pasa bajos

--> [hm_pb, fr] = frmag(hz_pb(2), hz_pb(3), 512);

--> subplot(3,1,1);

--> plot(fr*fs/2, 20*log10(hm_pb), 'b');

--> title('Respuesta en Frecuencia - Pasa Bajos');

--> xlabel('Frecuencia (Hz)');

--> ylabel('Magnitud (dB)');

--> xgrid();

--> 

--> // Pasa altos

--> [hm_pa, fr] = frmag(hz_pa(2), hz_pa(3), 512);

--> subplot(3,1,2);

--> plot(fr*fs/2, 20*log10(hm_pa), 'r');

--> title('Respuesta en Frecuencia - Pasa Altos');

--> xlabel('Frecuencia (Hz)');

--> ylabel('Magnitud (dB)');

--> xgrid();

--> 

--> // Pasa banda

--> [hm_pbnd, fr] = frmag(hz_pbnd(2), hz_pbnd(3), 512);

--> subplot(3,1,3);

--> plot(fr*fs/2, 20*log10(hm_pbnd), 'g');

--> title('Respuesta en Frecuencia - Pasa Banda');

--> xlabel('Frecuencia (Hz)');

--> ylabel('Magnitud (dB)');

--> xgrid();

--> 

--> disp('✅ Simulación completada. Revisa las figuras generadas.');

  "✅ Simulación completada. Revisa las figuras generadas."
at line     2 of executed string 

save: Wrong value for input argument #2: Defined variable expected.

 ans = 

  "C:\PROGRA~1\SCILAB~1.1"
at line    26 of function main_menubar_cb ( C:\Program Files\scilab-2026.0.1\modules\gui\macros\main_menubar_cb.sci line 35 )

winopen: Cannot open file C:\Users\QUINTERO\Downloads\codigo filtros.

 ans = 

  "C:\Users\QUINTERO\AppData\Roaming\Scilab\scilab-2026.0.1"

 ans = 

  "C:\PROGRA~1\SCILAB~1.1"

 ans = 

  "C:\Users\QUINTERO"

  "Environment saved."
Scanning repository https://atoms.scilab.org/2026.0/TOOLBOXES/64 ... Done

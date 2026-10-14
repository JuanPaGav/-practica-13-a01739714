# Bitácora · Práctica 13

Fecha: 14 de octubre de 2026  
Entorno: emulador Android x86_64 (`sdk_gphone16k_x86_64`), modelo Gemma 3 1B int4, ejecución sin internet.

## B3 · Velocidad y respuesta

- Tarea: Recado → Más amable.
- Primera palabra: 1.285 s desde tocar «Redactar», medido localmente al llegar el primer fragmento.
- Una ejecución completa mostró 46 tokens y 9.5 tokens/s. Otra ejecución mostró 46 tokens y 11.0 tokens/s.
- El tono fue más cordial y conservó la petición de lavar los platos hoy. Agregó una justificación sobre «limpiar el ambiente» que no estaba en el original.
- No hice comparación con otra computadora.

## C1/C3 · Qué obedeció

- Aviso → Más corto: 20 tokens a 21.7 tokens/s. El resumen conservó la razón general del cambio, pero omitió los días 14 y 17, la presentación del miércoles 19, la hora, el salón y los 10 minutos por equipo.
- Mensaje → 3 respuestas: 21 tokens a 18.7 tokens/s. Generó «Sí, claro.» y repitió «Por supuesto.» dos veces; no ofreció tres opciones distintas.
- Conclusión: el prompt guía el formato y el tono, pero Gemma 3 1B todavía puede omitir datos o repetir opciones. Hay que revisar el resultado antes de usarlo.

## B2 · Detener

Al detener una respuesta de Recado a mitad de generación, la app conservó el fragmento recibido (10 tokens) y volvió al botón «Redactar».

## D2 · Inicialización en el hilo principal

En Logcat apareció `Skipped 496 frames` durante una carga en frío (aproximadamente 8.3 s de fotogramas omitidos a 60 Hz). En una carga posterior con la caché caliente aparecieron 98 fotogramas omitidos. Al regresar a `main`, con `withContext` y la caché caliente, se registraron 64 fotogramas omitidos. La app llegó a «Gemma 3 1B · listo» y generó respuestas; las 24 pruebas siguieron pasando en esta rama.

En un intento inicial la app mostró `tf_lite_prefill_decode not found in the model`. Después de volver a abrir la app y copiar el archivo íntegro (584417280 bytes), la carga y la generación funcionaron; no volví a reproducir ese error.


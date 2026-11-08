1# Incidente 01: Nginx no arranca por error en nginx.conf

**Fecha:** 2026-11-08
**Servicio afectado:** nginx (VM server)

## Síntoma
`systemctl restart nginx` falla y el servicio queda en estado `failed`.

## Diagnóstico
1. `journalctl -u nginx -n 6` → `invalid number "76ñ8" in /etc/nginx/nginx.conf:9`
2. `sudo nginx -t` → confirma el error de configuración en la línea 9

## Causa raíz
Valor inválido (con un carácter no numérico) en la línea 9 de `/etc/nginx/nginx.conf`.

## Solución
Corregí el valor en la línea 9, reinicié con `systemctl restart nginx`
y verifiqué con `curl localhost` (respuesta "Welcome to nginx!").

## Prevención
Ejecutar `sudo nginx -t` antes de cada reinicio o recarga.

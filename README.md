# Patrimonio Mimitos — versión GitHub

Una sola página (`index.html`) que guarda sus datos en un archivo `data.json` de un repositorio **privado** tuyo, usando la API de GitHub con un token que queda sólo en tu navegador. Sin servidores, sin cuentas nuevas, sin costo.

## Cómo queda armado

| Repositorio | Visibilidad | Contenido | Para qué |
|---|---|---|---|
| `patrimonio-app` | **público** (obligatorio para GitHub Pages gratis) | `index.html`, `README.md` | La app. No contiene ningún dato tuyo: sólo el código. |
| `patrimonio-datos` | **privado** | `data.json` | Tus números. Cada guardado desde la app es un commit: el historial es el respaldo. |

La app se abre en `https://<tu-usuario>.github.io/patrimonio-app/` desde cualquier dispositivo.

## Puesta en marcha (una vez, ~10 minutos, todo desde el navegador)

1. **Repo de datos (privado).** En GitHub: *New repository* → nombre `patrimonio-datos` → **Private** → *Create*. Después *Add file → Upload files* → subí `data.json` → *Commit changes*.
2. **Repo de la app (público).** *New repository* → nombre `patrimonio-app` → **Public** → *Create*. *Add file → Upload files* → subí `index.html` y `README.md` → *Commit changes*.
3. **Activar la página.** En `patrimonio-app`: *Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: main / (root) → Save*. En 1-2 minutos aparece la URL `https://<tu-usuario>.github.io/patrimonio-app/`.
4. **Token.** Foto de perfil → *Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token*:
   - Token name: `patrimonio-app` · Expiration: 1 año
   - Repository access: **Only select repositories** → `patrimonio-datos`
   - Permissions → Repository permissions → **Contents: Read and write** (nada más)
   - *Generate token* y copialo (se muestra una sola vez).
5. **Conectar.** Abrí la URL de la app, completá usuario, `patrimonio-datos` y el token → *Conectar*. Listo: el token queda guardado en ese navegador (repetir en el celular).

## Uso mensual

*Cargar datos* → elegís el mes → 6 números → *Guardar mes*. Cada guardado es un commit en `patrimonio-datos` con la fecha en el mensaje. Para volver atrás: en GitHub, *History* del archivo → *Browse files* en la versión anterior → copiá `data.json`.

Si preferís pedírselo a Claude: "cargá septiembre de Juncal" — Claude saca el número de Odoo y actualiza `data.json` (necesita que GitHub esté conectado en claude.ai, o te pasa el JSON para pegar).

## Seguridad

- El token sólo puede leer y escribir **ese** archivo de **ese** repo. Si lo perdés o cambiás de dispositivo, revocalo en *Developer settings* y generá otro.
- Nunca subas `data.json` al repo público ni pegues el token en el código.
- *Desconectar* (en el panel de conexión) borra el token de ese navegador.

## Estructura de `data.json`

```json
{
  "version": 1,
  "config": { "gastos_mensuales_ars": 6000000, "objetivo_usd_mes": 10000, "rendimiento_neto_pct": 5, "inmuebles": [...], "locales": [...], "otros": [...], "deudas": [], "escenarios": {...} },
  "meses": {
    "2026-09": { "mep_prom": 1536.14, "mep_cierre": 1553.16, "ipc_var": 1.7, "cartera_usd": 160000, "caja_usd": 0,
                 "ganancia": { "juncal": 4099000, "ituzaingo": -6000000 }, "nota": "" }
  }
}
```

`ganancia` va en pesos del mes (negativo si perdió). Lo que falta se rellena solo: dólar = último conocido; inflación = supuesto; rentas y gastos = valores fijos.

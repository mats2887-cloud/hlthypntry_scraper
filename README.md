# Healthy Pantry Price Intelligence v2

MVP operativo para recolectar precios públicos de frutas y verduras, guardar histórico,
comparar contra Central de Abasto y generar un reporte diario para Healthy Pantry.

## Qué hace

- Consulta tiendas configuradas: Walmart, Soriana, Chedraui, La Comer, Costco, City Market, HEB.
- Respeta `robots.txt` en modo best-effort y no evade bloqueos, captchas ni autenticación.
- Guarda histórico en SQLite.
- Genera reporte diario en CSV.
- Calcula precio mínimo de supermercado, precio promedio, diferencia contra Central de Abasto y oportunidad comercial.
- Deja registro de errores por tienda/producto.

## Instalación local

```bash
python -m venv .venv
source .venv/bin/activate

pip install -r requirements.txt
playwright install chromium
cp .env.example .env
python -m app.main
```

## Ejecutar todos los días

### Mac/Linux con cron

```bash
crontab -e
```

Agregar:

```cron
0 6 * * * cd /ruta/healthy_pantry_price_intelligence_v2 && .venv/bin/python -m app.main >> logs.txt 2>&1
```

### Docker

```bash
docker build -t healthy-pantry-prices .
docker run --rm -v $(pwd)/app/reports:/app/app/reports healthy-pantry-prices
```

### GitHub Actions

Incluye `.github/workflows/daily-prices.yml`.

## Nota legal y operativa

Los retailers pueden cambiar HTML, bloquear scraping o restringir automatización.
Para operación comercial estable, la mejor práctica es usar APIs, data feeds autorizados,
acuerdos comerciales o proveedores de datos. Este MVP está diseñado para páginas públicas
permitidas y uso interno.

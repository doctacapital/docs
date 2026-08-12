# Docta API — documentación

Documentación pública de la **API de Docta**, publicada con [Mintlify](https://mintlify.com) en
**https://docs.doctacapital.com.ar**.

Cubre dos dominios del mercado argentino:

- **Bonos** (9 endpoints): catálogo e instrumentos, rendimientos intradiarios e históricos,
  flujos de fondos, valor residual, comparador y calculadora precio ↔ TIR.
- **FCI** (16 endpoints): screener del universo de fondos, ficha con composición y fees,
  series diarias, performance, benchmarks, comparaciones y analytics de industria.

> **Este repo es la fuente de verdad del alcance público de la API.** El
> [servidor MCP](https://mcp.docta.com.ar/mcp) expone una herramienta por endpoint
> documentado acá (26 herramientas ↔ 25 endpoints + `get_my_usage`). Los endpoints que
> existen en el gateway pero no están documentados acá se consideran deprecados: no se
> exponen ni se documentan sin decisión previa.

## Estructura

```
docs.json                     # navegación, tema y SEO del sitio
index.mdx                     # home
onboarding-ia.mdx             # guía para agentes de IA / LLMs
servidor-mcp.mdx              # guía del servidor MCP (Mintlify reserva /mcp)
api-reference/
  introduction.mdx            # autenticación, planes y credenciales
  openapi.json                # spec OpenAPI 3.1 — playground de cada endpoint
  endpoint/*.mdx              # una página por endpoint (frontmatter title + openapi)
```

Las páginas de endpoint combinan la spec (`openapi: 'GET /api/v1/...'` en el frontmatter,
que genera el playground) con prosa escrita a mano: `<ParamField>`, `<ResponseField>` y
ejemplos de request/response reales de producción.

## Desarrollo

```bash
npm i -g mint     # CLI de Mintlify
mint dev          # preview en http://localhost:3000
mint broken-links # chequeo de links internos
```

## Publicación

El deploy es automático al pushear a `main` (GitHub app de Mintlify). Al agregar una página
nueva, acordate de sumarla a la navegación en `docs.json` — si no, queda accesible por URL
pero no aparece en el sidebar.

## Convenciones

- Español (es-AR) en todo el contenido publicado.
- Las tasas y retornos son decimales (`0.1046` = 10,46%); las fechas, `YYYY-MM-DD`.
- Antes de documentar un endpoint, verificalo contra producción y escribí los campos a
  partir de la respuesta real, nunca del nombre del endpoint.

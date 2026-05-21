> # 📦 This repo has moved
>
> **`ai-research-skills` has been consolidated into [Growth4U-systems/growth-skills](https://github.com/Growth4U-systems/growth-skills)** — a single curated home for all our open-source Claude Code skills.
>
> ## What changed
> - `deep-research` and `qa-bot` are now maintained in [growth-skills/skills/](https://github.com/Growth4U-systems/growth-skills/tree/main/skills)
> - The new repo includes additional skills (g4u-seo, token-hygiene) and a master INDEX with skill connections
> - This repo is **archived** (read-only). No new commits, issues, or PRs here.
>
> ## Install going forward
> ```bash
> git clone https://github.com/Growth4U-systems/growth-skills.git
> # Pick the skills you want from skills/
> ```
>
> ---
>
> Below: original README, preserved for context.
>
> ---

# AI Research Skills: Investiga sin errores con IA

Un sistema de 3 capas para investigar temas complejos con inteligencia artificial, minimizando alucinaciones y errores factuales.

Estas skills funcionan con **Claude Code** / **Claude Cowork** (Anthropic). Son archivos `.md` que puedes adaptar a cualquier flujo de trabajo con LLMs.

## El problema

El 90% de la gente hace esto:

> "Oye ChatGPT, investiga sobre el mercado de banca digital en Espana"

Y se fia del resultado. **Error.**

Los LLMs no investigan. Predicen texto. Sin un proceso de verificacion, estas construyendo sobre datos que pueden ser inventados, desactualizados o sacados de contexto.

## La solucion: 3 capas que se verifican entre si

```
Last 30 Days  -->  Deep Research  -->  QA Bot
 (escucha)        (investigacion)     (verificacion)
```

### Capa 1: Last 30 Days

Escucha social en tiempo real. Escanea Reddit, X (Twitter) y YouTube para saber que dice la gente **ahora mismo** sobre tu tema.

- Pesa resultados por engagement (upvotes, likes, views)
- Identifica patrones, voces clave y herramientas mencionadas
- Output: pulso social real vs lo que dicen los informes oficiales

> **Nota:** Esta skill esta basada en [last30days de mvanhorn](https://github.com/mvanhorn/last30days-skill). He incluido una copia aqui para referencia, pero recomiendo usar el [repo original](https://github.com/mvanhorn/last30days-skill) para tener la version mas actualizada.

### Capa 2: Deep Research

Investigacion estructurada en **7 fases**. De pregunta vaga a informe verificado con fuentes.

```
SCOPE --> SOURCES --> EXTRACT --> FRAMEWORK --> DETAIL --> QA --> DELIVER
  1         2          3           4            5        6       7
```

- Minimo 10 fuentes unicas de 5 categorias (oficial, comparadores, prensa, regulacion, comunidad)
- Cada claim tiene fuente y nivel de confianza (verified / reported / inferred)
- Framework que **sorprenda al lector** con insights no obvios
- Fase 6 (QA) es **obligatoria** - invoca automaticamente al QA Bot

### Capa 3: QA Bot

Verificacion independiente usando **Chain of Verification (CoVe)** en 4 fases:

1. **Lee el documento** y genera preguntas de verificacion
2. **Investiga de forma independiente** (sin mirar el documento original)
3. **Compara** sus hallazgos con el documento
4. **Clasifica** cada claim: Verified / Discrepancy / Error / Unverifiable

No es un validador complaciente. Actua como un inversor esceptico haciendo due diligence.

## Como usarlas

### Requisitos

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) o Claude Cowork (plan Pro)
- Para Last 30 Days: Python 3, `OPENAI_API_KEY` (ver [repo original](https://github.com/mvanhorn/last30days-skill) para setup completo)

### Instalacion

1. Copia los archivos `.md` de la carpeta `skills/` a tu directorio de skills:
   - Claude Code: `~/.claude/skills/` o dentro de tu proyecto en `00-system/skills/`
   - O simplemente referencia los archivos desde tu `CLAUDE.md`

2. Para usar una skill, escribe en Claude Code:
   ```
   /deep-research [tema] para [cliente/proyecto]
   /qa-bot [archivo a revisar]
   /last30days [tema]
   ```

### Ejemplo practico

**Objetivo:** Analisis competitivo de neobancos en Espana

**Paso 1 - Plan de investigacion** (la clave esta aqui):
- Descargar memorias anuales e informes regulatorios
- Identificar fuentes oficiales (Banco de Espana, CNMV, EBA)
- Definir entidades a cubrir

**Paso 2 - Escucha social:**
```
/last30days neobancos banca digital espana
```

**Paso 3 - Investigacion estructurada:**
```
/deep-research analisis competitivo de neobancos en Espana para [cliente]
```
(Deep Research ejecutara automaticamente QA Bot en fase 6)

**Resultado:** Informe de 40+ paginas con fuentes, framework no obvio, y score de confianza 8.5/10.

## Estructura del repo

```
skills/
  deep-research/SKILL.md    -- Investigacion estructurada 7 fases
  qa-bot/SKILL.md            -- Verificacion CoVe 4 fases
  last30days/SKILL.md        -- Escucha social (referencia)
```

## Creditos

- **Deep Research** y **QA Bot**: Creados por [Alfonso Sainz de Baranda](https://www.linkedin.com/in/alfonsosbla/) (Growth4U)
- **Last 30 Days**: Basado en [last30days-skill](https://github.com/mvanhorn/last30days-skill) de [mvanhorn](https://github.com/mvanhorn)

## Licencia

MIT - Usa, modifica y comparte libremente.

---

*Hecho con Growth4U - [growth4u.io](https://growth4u.io)*

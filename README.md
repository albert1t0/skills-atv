# Skills-ATV (Alberto Torreblanca V.)

Colección personal de **skills para agentes CLI** ([opencode](https://opencode.ai), Claude Code, etc.). Cada skill vive en su propia carpeta con un archivo `SKILL.md` que define su comportamiento, triggers y herramientas permitidas.

## Skills

| Skill                                 | Descripción                                                                                                                                |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| [obsidian-slides](obsidian-slides/)   | Crea presentaciones como archivos Markdown compatibles con el plugin Obsidian Advanced Slides (reveal.js). Incluye referencia de sintaxis. |
| [tesis-ingenieria](tesis-ingenieria/) | Asistente académico para tesis de maestría en Ingeniería. Especializado en MCP, arquitectura de agentes y redacción formal en español.     |
| [text-refiner](text-refiner/)         | Mejora textos en español o inglés: corrige gramática, aumenta claridad, ajusta tono y preserva la voz personal del autor.                  |

## Estructura

```
skills-atv/
├── obsidian-slides/
│   ├── SKILL.md
│   └── syntax-reference.md
├── tesis-ingenieria/
│   └── SKILL.md
├── text-refiner/
│   └── SKILL.md
└── README.md
```

## Uso

Copia la carpeta de la skill que necesites al directorio de skills de tu agente CLI. Por ejemplo, para **opencode**:

```bash
cp -r obsidian-slides/ ~/.agents/skills/
```

## Licencia

MIT

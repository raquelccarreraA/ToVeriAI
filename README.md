<div align="center">

# toVeriAI

**La IA que te dice cuánto puedes fiarte de una noticia, y por qué.**

[**▶ Pruébala en toveriai.com**](https://www.toveriai.com)

![Java 17](https://img.shields.io/badge/Java-17-orange)
![Spring Boot 3.5](https://img.shields.io/badge/Spring%20Boot-3.5-6DB33F)
![React 19](https://img.shields.io/badge/React-19-61DAFB)
![MySQL 8](https://img.shields.io/badge/MySQL-8-4479A1)
![LLMs](https://img.shields.io/badge/IA-5%20LLMs%20%2B%20modelo%20propio-2D6A4F)

![Página de inicio de toVeriAI](docs/toveriai-home.png)

</div>

Pegas un texto, una URL o una captura de una noticia y, en menos de 30 segundos, toVeriAI devuelve un **índice de credibilidad de 0 a 100** con la explicación de cada nota y citas literales del artículo. Sin cajas negras.

Es mi proyecto: la creé desde cero y la sigo evolucionando como un producto **en producción**.

| 9 | 3 | 5 | 5 | v2 |
|:---:|:---:|:---:|:---:|:---:|
| dimensiones de análisis | modos: texto, URL e imagen | proveedores de IA en rotación | idiomas | de mi propio modelo de IA |

---

## Lo más destacado

**🧠 Mi propio modelo de IA: VeriAI.**
Cada análisis en producción alimenta un dataset de entrenamiento. Lo exporto, hago fine-tuning en local y cada 6.000 análisis sale una versión nueva: va por la **v2 (Qwen 2.5 7B)**, con una variante sobre **Qwen 3.5 7B** en marcha. Pasará a producción cuando iguale o supere a las APIs comerciales.

**⚡ Cinco LLMs que nunca la dejan caer.**
Un orquestador propio reparte el trabajo entre **Cerebras, Gemini, Mistral, SambaNova y Cloudflare**, con failover automático. Elijo los proveedores con datos: Groq quedó fuera de la puntuación porque, en pruebas con noticias falsas, detectaba peor que el resto.

**🔍 Explicable, no un veredicto.**
El Índice de Métricas Interpretativas (IMI) se basa en los criterios de NewsGuard, IFCN y The Trust Project. Puntúa la verificación factual, las fuentes, el sesgo o el tono, y cada nota viene con citas del artículo.

**👥 Más que una herramienta: una comunidad.**
Feed público donde los usuarios votan si coinciden con la IA, ranking de fiabilidad de los medios, avisos cuando un medio que sigues cambia, rachas con recompensa e informe PDF Premium.

## Qué demuestra este proyecto

- **Full stack de verdad:** API REST con Spring Boot y frontend en React, del modelo de datos al despliegue.
- **IA aplicada:** integración de varios LLMs, ingeniería de prompts, generación de datasets y fine-tuning.
- **Pensar en producción:** caché por hash para no gastar llamadas, cupos por usuario, tareas programadas y despliegue continuo en Vercel y Render con Docker.
- **Seguridad:** Spring Security con JWT, roles, login con Google y verificación por email.
- **Calidad:** tests con JUnit, API documentada con Swagger y colección de Postman.
- **Producto:** interfaz en 5 idiomas, panel de administración completo y modelo freemium.

## Arquitectura

```mermaid
flowchart LR
    U[Usuario] --> F["React 19 + Vite<br/>(Vercel)"]
    F -- REST + JWT --> B["Spring Boot 3.5<br/>(Render · Docker)"]
    B --> DB[(MySQL 8)]
    B --> O{{Orquestador IA}}
    O -- rotación + failover --> C["Cerebras · Gemini · Mistral<br/>SambaNova · Cloudflare"]
    B -- dataset --> L["VeriAI<br/>fine-tuning en local"]
```

**Stack:** Java 17 · Spring Boot · Spring Security · JWT · JPA/Hibernate · MySQL · React 19 · Vite · Recharts · jsPDF · Docker · Ollama · Qwen · JUnit

---

El código es privado, pero te lo enseño encantada en una entrevista. Si quieres más detalle técnico, aquí está la [documentación técnica](Documentacion/documentacion-tecnica.html).

## Sobre mí

Soy **Raquel Comesaña Carrera**, desarrolladora full stack (Java · Spring Boot · React) en A Coruña, especializándome en IA y Big Data. **Busco trabajo como desarrolladora, con disponibilidad inmediata.**

[Portfolio](https://raquelccarreraa.github.io/Porfolio-raquelcarrera/) · [LinkedIn](https://www.linkedin.com/in/raquel-comesa%C3%B1a-carrera-1646ba195) · raquel.ccarrera@gmail.com

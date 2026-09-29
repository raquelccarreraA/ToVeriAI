# toVeriAI

Plataforma web de análisis de credibilidad de noticias mediante inteligencia artificial, desarrollada como Trabajo de Fin de Ciclo del Grado Superior en Desarrollo de Aplicaciones Web. El sistema evalúa cualquier texto informativo en siete dimensiones independientes y genera un índice de credibilidad IMI (Índice de Métricas Interpretativas) de 0 a 100. Permite el uso anónimo con límite diario y ofrece historial, perfil y estadísticas a los usuarios registrados.

Autora: Raquel C. — IES Fernando Wirtz Suárez · Tutor: Fernando Prado

Autor : Álvaro García Graña - Senior fullstack developer.

---

## Tecnologías utilizadas

**Backend**
- Java 17 + Spring Boot 3.x
- Spring Security con autenticación JWT
- Spring Data JPA / Hibernate
- MySQL 8
- Lombok
- Maven

**Frontend**
- React 18 + Vite
- React Router v6
- Axios
- Recharts
- i18n propio (ES, GL, CA, EU)

**Inteligencia Artificial**
- Rotacion de APIS para fine tunning.
- AI Local VeriNewsAI entrenada por los diferentes provedores.

---

## Requisitos previos

- Java 17 o superior
- Node.js 18 o superior
- MySQL 8
- Cuentas en los diferentes modelos y sus api keys.

---

## Configuración del entorno

El proyecto requiere un fichero de propiedades local que **no está incluido en el repositorio**. Antes de arrancar el backend, crea el fichero:

```
backend/src/main/resources/application-dev.properties
```

Con el siguiente contenido (sustituye los valores):

```properties
spring.datasource.username=tu_usuario_mysql
spring.datasource.password=tu_contraseña_mysql
modelo.api.key=tu_api_key_de_modelo
jwt.secret=una_clave_secreta_de_minimo_32_caracteres
```

> El fichero `application-dev.properties` está incluido en `.gitignore` y nunca debe commitearse. Contiene credenciales sensibles.

---

## Instalación y arranque

### Backend

```bash
cd backend
mvn spring-boot:run
```

El servidor arranca en `http://localhost:9000`.

### Frontend

```bash
cd frontend
npm install
npm run dev
```

La aplicación arranca en `http://localhost:5173`.

---

## Estructura del proyecto

```
VeriNews_AI/
├── backend/
│   └── src/main/java/com/verinews/backend/
│       ├── conf/           # Configuración de seguridad (Spring Security, CORS)
│       ├── config/         # Beans auxiliares (Messages, DataInitializer)
│       ├── controller/     # Endpoints REST
│       ├── dto/            # Objetos de transferencia de datos
│       ├── models/         # Entidades JPA y enums
│       ├── repositories/   # Interfaces Spring Data JPA
│       ├── security/       # JWT (JwtUtil, JwtFilter, UserDetailsServiceImpl)
│       └── service/        # Lógica de negocio
│
└── frontend/
    └── src/
        ├── components/     # Componentes reutilizables (Navbar, Footer, rutas protegidas)
        ├── context/        # AuthContext, TranslationContext
        ├── i18n/           # Ficheros de traducción JSON (es, gl, ca, eu)
        ├── pages/          # Vistas principales
        ├── services/       # Cliente Axios
        └── utils/          # Utilidades (colores IMI, etc.)
```

---

## Dimensiones del índice IMI

El índice IMI se calcula ponderando siete métricas basadas en el marco NewsGuard, complementado con criterios IFCN y The Trust Project:

| Dimensión             | Peso |
|-----------------------|------|
| Verificación Factual  | 26 % |
| Consistencia Interna  | 24 % |
| Fuentes               | 15 % |
| Sesgo                 | 12 % |
| Tono General          | 12 % |
| Semántica             | 6 %  |
| Cifras                | 5 %  |

Cada dimensión recibe entre 0 y 5 alertas. La puntuación final (0–100) penaliza proporcionalmente según el peso de cada métrica. Una puntuación alta en Verificación Factual actúa como techo global del índice.

---

## Seguridad

El fichero `application-dev.properties` contiene credenciales de base de datos y claves de API. Está listado en `.gitignore` y no debe incluirse en ningún commit ni repositorio público.

# Bautista-post2-u7
Unidad 7: Patrones Arquitectónicos I Post-Contenido 2

Este proyecto implementa un sistema de gestión de productos utilizando **arquitectura hexagonal**, separando el dominio de la infraestructura mediante puertos y adaptadores.

---

##  Objetivo

Aplicar el patrón arquitectónico **Hexagonal (Ports & Adapters)** para garantizar:

* Separación de responsabilidades
* Independencia del dominio
* Facilidad de pruebas
* Bajo acoplamiento

---

##  Estructura del Proyecto

```
com.example.hexagonal
│
├── domain/
│   ├── model/
│   │   └── Producto.java
│   ├── port/
│   │   ├── in/
│   │   │   ├── CrearProductoUseCase.java
│   │   │   ├── ListarProductosUseCase.java
│   │   │   └── ActualizarStockUseCase.java
│   │   └── out/
│   │       └── ProductoRepositoryPort.java
│   └── service/
│       └── ProductoDomainService.java
│
├── adapter/
│   ├── in/
│   │   └── web/
│   │       └── ProductoController.java
│   └── out/
│       └── persistence/
│           ├── ProductoJpaEntity.java
│           ├── ProductoJpaRepository.java
│           └── ProductoRepositoryAdapter.java
│
├── config/
│   └── BeanConfiguration.java
│
└── HexagonalApplication.java
```

---

##  Diagrama de Arquitectura

```
            ┌───────────────────────┐
            │   Cliente (HTTP)      │
            └─────────┬─────────────┘
                      │
                      ▼
         ┌──────────────────────────┐
         │   ProductoController     │
         │   (Adaptador Web)        │
         └─────────┬────────────────┘
                   │
                   ▼
         ┌──────────────────────────┐
         │  Puertos de Entrada      │
         │ (Use Cases - Interfaces) │
         └─────────┬────────────────┘
                   │
                   ▼
         ┌──────────────────────────┐
         │ ProductoDomainService    │
         │ (Lógica de negocio)      │
         └─────────┬────────────────┘
                   │
                   ▼
         ┌──────────────────────────┐
         │ Puerto de Salida         │
         │ (Repository Port)        │
         └─────────┬────────────────┘
                   │
                   ▼
         ┌──────────────────────────┐
         │ Adaptador JPA            │
         │ (Base de datos H2)       │
         └──────────────────────────┘
```

---

##  Tecnologías Utilizadas

* Java 17+
* Spring Boot 3.x
* Spring Web
* Spring Data JPA
* Base de datos H2 (en memoria)
* Maven

---

##  Ejecución del Proyecto

### 1. Clonar repositorio

```
git clone https://github.com/TU-USUARIO/Bautista-post2-u7.git
cd Bautista-post2-u7/hexagonal
```

### 2. Ejecutar la aplicación

```
mvn spring-boot:run
```

Servidor disponible en:

```
http://localhost:8080
```

---

##  Endpoints disponibles

###  Listar productos

```
GET /api/productos
```

---

###  Crear producto

```
POST /api/productos
```

Body JSON:

```
{
  "nombre": "Laptop",
  "descripcion": "Gaming",
  "precio": 2500000,
  "stock": 5
}
```

---

###  Buscar por ID

```
GET /api/productos/{id}
```

---

###  Reducir stock

```
PATCH /api/productos/{id}/stock?cantidad=2
```

---

##  Pruebas con curl
<img width="1246" height="464" alt="image" src="https://github.com/user-attachments/assets/b4e832a8-660e-48eb-a359-5e4e9239fcb2" />


###  Listar (vacío)

```
curl http://localhost:8080/api/productos
```

### ✔ Crear producto

```
curl -X POST http://localhost:8080/api/productos \
-H "Content-Type: application/json" \
-d "{\"nombre\":\"Laptop\",\"descripcion\":\"Gaming\",\"precio\":2500000,\"stock\":5}"
```

### ✔ Buscar por ID

```
curl http://localhost:8080/api/productos/1
```

### ✔ Reducir stock

```
curl -X PATCH "http://localhost:8080/api/productos/1/stock?cantidad=2"
```

### ✔ Error (stock insuficiente)

```
curl -X PATCH "http://localhost:8080/api/productos/1/stock?cantidad=100"
```

---

##  Evidencias (Capturas)
<img width="1246" height="464" alt="image" src="https://github.com/user-attachments/assets/6f93384c-3191-4215-83a7-f827a3506a65" />


Se incluyen capturas de:

* ✔ GET lista vacía
* ✔ POST creación de producto
* ✔ GET por ID
* ✔ PATCH reducción de stock
* ✔ Error por stock insuficiente

---

##  Checkpoints cumplidos

* ✔ Dominio sin dependencias de Spring ni JPA
* ✔ Uso de puertos de entrada y salida
* ✔ Adaptadores separados (Web y Persistencia)
* ✔ Inyección de dependencias mediante configuración
* ✔ Proyecto compila correctamente
* ✔ Endpoints funcionales
* ✔ Persistencia con H2

---

##  Autor

Jahir Duran
Ingeniería de Sistemas - 2026

---

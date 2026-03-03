<div align="center">

# ODXIS — Tu negocio, bajo control

> Un producto de **[Cosmocratores SAS](https://cosmocratores.github.io)** · Soporte: help@odxis.com · [odxis.com](https://odxis.com)

### La plataforma que administra todos los aspectos de tu negocio en un solo lugar

[![Status](https://img.shields.io/badge/Estado-En_Desarrollo-blue?style=for-the-badge)]()
[![Modules](https://img.shields.io/badge/17_Módulos-Integrados-22543d?style=for-the-badge)]()
[![Compliance](https://img.shields.io/badge/DIAN-Certificado-e53e3e?style=for-the-badge)]()

</div>

---

## ¿Qué es Odxis?

Odxis es un **sistema completo de administración empresarial** diseñado para negocios colombianos — comercios, restaurantes, hoteles y empresas de servicios.

En vez de usar 5 programas diferentes (uno para facturas, otro para inventario, otro para nómina...), Odxis lo integra **todo en una sola plataforma**:

- Llevas tus **facturas electrónicas** como la DIAN lo exige
- Controlas tu **inventario** sin sorpresas de faltantes
- Administras tu **nómina** con todo lo que la ley colombiana pide
- Manejas las **reservas del hotel** o las **mesas del restaurante**
- Y al final del mes tienes **reportes financieros reales**, no suposiciones

> **Menos estrés de papeleo. Más tiempo para hacer crecer tu negocio.**

---

## ¿Qué puedes hacer con Odxis?

### Operación del día a día

| Módulo | Qué hace por ti |
|--------|----------------|
| **Inventario** | Sabes exactamente qué tienes, dónde está, y cuánto vale. Incluye recetas y transferencias entre bodegas. |
| **Punto de Venta (POS)** | Tu caja registradora digital: toma pedidos, aplica descuentos, controla el efectivo. |
| **Pantalla de Cocina (KDS)** | El cocinero ve los pedidos en tiempo real, sin papeles ni gritos. |
| **CRM** | Tu lista de clientes organizada: desde el primer contacto hasta la venta cerrada. |
| **Ventas** | Seguimiento de oportunidades comerciales y pipeline de ventas. |
| **Aliados Comerciales** | Gestión de revendedores y distribuidores. |

### Finanzas y cumplimiento legal

| Módulo | Qué hace por ti |
|--------|----------------|
| **Contabilidad** | Plan Único de Cuentas (PUC), asientos automáticos, conciliación bancaria. |
| **Facturación Electrónica** | Facturas válidas ante la DIAN (UBL 2.1). Todo automático: CUFE, notas crédito/débito, resoluciones. |
| **Reportes** | Estado de resultados, balance general, flujo de caja. Los números reales de tu negocio. |

### Personal y operaciones

| Módulo | Qué hace por ti |
|--------|----------------|
| **Nómina y RRHH** | Nómina colombiana completa: seguridad social, prestaciones, horas extra, vacaciones, dotación. Actualizado al CST 2024. |
| **Hotel (PMS)** | Habitaciones, reservas, check-in/out, cargos a habitación, ama de llaves, historial de huéspedes. |
| **Academia (LMS)** | Capacita a tu equipo: cursos, lecciones, seguimiento de progreso. |
| **Soporte** | Sistema de tickets para atención al cliente con categorías y tiempos de respuesta. |
| **Servicios** | Catálogo de servicios, profesionales, citas y agendamiento. |

### Plataforma

| Módulo | Qué hace por ti |
|--------|----------------|
| **Seguridad y Roles** | Cada empleado ve solo lo que necesita. 10 roles predefinidos (dueño, cajero, mesero, recepcionista...) con 35 permisos específicos. |
| **Blog** | Publica contenido desde tu panel. |
| **Suscripciones** | Planes EMPRENDEDOR, CRECIMIENTO y EMPRESA según el tamaño de tu negocio. |

---

## ¿Cómo funciona por dentro? (para técnicos)

Odxis está construido con tecnologías modernas y probadas:

| Componente | Tecnología | Para qué sirve |
|------------|-----------|----------------|
| Aplicación web | Next.js 15 con TypeScript | Interfaz rápida y confiable |
| Comunicación | tRPC 11 | Los datos viajan seguros entre pantalla y servidor |
| Base de datos | PostgreSQL 16 en Azure | Almacenamiento confiable y escalable |
| ORM | Prisma 6 | 68 modelos de datos organizados |
| Autenticación | Auth.js v5 + 2FA | Acceso seguro con verificación en dos pasos |
| Interfaz | Tailwind CSS + shadcn/ui | Diseño limpio y profesional |
| Pagos | Wompi | Pagos con tarjeta y PSE para Colombia |
| Facturación DIAN | Dataico API | Envío oficial de facturas electrónicas |
| Seguridad | Rate limiting, audit trail | Protección contra abuso y registro de todo lo que pasa |

### Cada negocio, aislado

Los datos de tu negocio **nunca se mezclan** con los de otros clientes. Cada registro está identificado con tu `organizationId` y verificado automáticamente en cada operación.

---

## Cumplimiento colombiano

### Facturación electrónica DIAN
- Formato UBL 2.1 (el que exige la DIAN)
- Código CUFE generado automáticamente
- Notas crédito y débito electrónicas
- Validación de resoluciones (prefijo, rango, vigencia)
- Integración directa con Dataico para envío oficial

### Nómina — CST 2024
Todo lo que la ley laboral colombiana exige:
- Seguridad social (EPS, pensión, ARL)
- Parafiscales (SENA, ICBF, caja de compensación)
- Prestaciones (cesantías, intereses, prima, vacaciones)
- Horas extra (diurna 125%, nocturna 175%, dominical 200%)
- Auxilio de transporte para salarios ≤2 SMLMV
- Fondo de solidaridad para salarios >4 SMLMV
- Licencias: vacaciones, incapacidad, maternidad/paternidad
- Retención en la fuente

### Impuestos
- IVA: 19%, 5%, exento, excluido
- INC: 8% impuesto al consumo
- Retenciones automáticas (renta, IVA, ICA)
- Validación de RUT en línea con la DIAN

---

## Roles de usuario

Cada persona en tu negocio tiene acceso solo a lo que necesita:

| Rol | Lo que puede hacer |
|-----|--------------------|
| **Dueño** | Todo, incluyendo facturación |
| **Administrador** | Todo excepto facturación |
| **Contador** | Contabilidad, facturación, nómina, reportes |
| **Cajero** | Punto de venta, caja, consultar inventario |
| **Mesero** | Tomar pedidos, ver pantalla de cocina |
| **Recepcionista** | Reservas de hotel, CRM, punto de venta |
| **RRHH** | Empleados, turnos, nómina |
| **Chef** | Pantalla cocina, recetas, consultar inventario |
| **Miembro** | Ver dashboard, inventario y ventas |
| **Observador** | Solo ver el dashboard |

---

## Documentación técnica

| Documento | Contenido |
|-----------|-----------|
| [ARCHITECTURE.md](ARCHITECTURE.md) | Diseño del sistema con diagramas |
| [MODULES.md](MODULES.md) | Detalle de cada módulo |
| [SECURITY.md](SECURITY.md) | Modelo de seguridad y cumplimiento |
| [TECH_STACK.md](TECH_STACK.md) | Tecnologías y razones de elección |

---

<div align="center">

**Código fuente:** [github.com/Cosmocratores/odxis](https://github.com/Cosmocratores/odxis) (privado)
·
**Web:** [odxis.com](https://odxis.com)
·
**Contacto:** help@odxis.com

</div>

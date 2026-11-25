# trace-M.R.D — Plataforma de Trazabilidad Aduanera y Logística en Tiempo Real

> **© 2026 Marcelo Rubén Damas — M.R.D Technology.** Todos los derechos reservados.  
> *Este repositorio funciona como vitrina técnica y de arquitectura. El código fuente del motor servidor se mantiene privado bajo propiedad intelectual registrada.*

---

## Descripción Ejecutiva
**trace-M.R.D** es una plataforma web y motor API desarrollado desde cero bajo una arquitectura **Zero-Dependencies** (biblioteca estándar de Python 3.8+ y SQLite) para el monitoreo en tiempo real de guías de cargas, aforos físicos y estados de internación logística.

Diseñada bajo principios de **Security by Design**, permite recibir eventos operativos desde sistemas ERP externos de forma verificable, auditada y estrictamente aislada por empresa cliente.

---

## Arquitectura del Sistema

```text
[ Sistema ERP Externo ]
         │
         ▼  POST Webhook (Firma HMAC-SHA256 + Timestamp Anti-Replay)
┌──────────────────────────────────────────────────────────┐
│                  API Core trace-M.R.D                    │
│  • Validación Criptográfica & Idempotencia (event_id)    │
│  • Control de Acceso RBAC (Admin / Usuario Cliente)      │
│  • Bitácora Forense Inmutable (Auditoría de Eventos)     │
└────────────────────────┬─────────────────────────────────┘
                         │
                         ▼  Server-Sent Events (SSE Tiempo Real)
            [ Panel de Control Web Segregado ]

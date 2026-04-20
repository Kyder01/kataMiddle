# 🧪 Reto Técnico – Procesamiento de Transacciones Core Banking
### Batch (COBOL + JCL) | Online (COBOL + CICS)

Este repositorio contiene una **simulación de un sistema core bancario**, desarrollada como parte de una **kata técnica semisenior**, cuyo objetivo es demostrar conocimientos en:

- Procesamiento **Batch**
- Operación **Online (CICS)**
- Validaciones de negocio
- Diseño de flujos típicos de **Core Banking**

---

## 🎯 Objetivo General

Construir una solución simple pero representativa que permita:

- Procesar transacciones bancarias de forma **batch**
- Gestionar rechazos y excepciones operativas
- Consultar y operar cuentas en **línea (CICS)**
- Simular flujos reales usados en sistemas bancarios productivos

---

## 🧭 Contexto Funcional

El sistema simula dos grandes componentes del core bancario:

### 1️⃣ Procesamiento Batch Diario
- Procesa un archivo secuencial con transacciones.
- Actualiza saldos por cuenta.
- Genera salidas operativas y de control.

### 2️⃣ Operación Online (CICS)
- Permite consultar saldos.
- Permite realizar retiros con validaciones en tiempo real.

---

## 🧩 Parte 1 – Procesamiento Batch

### 📥 Archivo de Entrada

Archivo secuencial con transacciones bancarias:

**Campos:**
- Número de cuenta
- Tipo de transacción  
  - `D` → Depósito  
  - `W` → Retiro
- Monto

---

### ⚙️ Lógica de Procesamiento (COBOL Batch)

El proceso batch realiza:

- Lectura secuencial del archivo de entrada
- Identificación y validación de la cuenta
- Aplicación de depósitos y retiros
- Control de saldos
- Clasificación de errores y excepciones

---

### 📤 Archivos Generados

#### ✅ Archivo de Saldos
Contiene las cuentas procesadas correctamente:

ACC001|SALDO|800

ACC002|SALDO|500

---

#### ❌ Archivo de Rechazos

Incluye:

- Registros con formato inválido
- Tipos de transacción no reconocidos
- Cuentas inexistentes
- Cuentas con fondos insuficientes

Este archivo permite **auditoría y control operativo**.

---

#### ⏳ Archivo de Débitos Pendientes

Contiene **retiros rechazados por fondos insuficientes**.

📌 **Importante:**  
Estos registros se almacenan en un archivo independiente para ser **procesados posteriormente por un proceso de aplicación de débitos pendientes**, simulando un flujo real del core bancario.

---

## 🧩 Parte 2 – Procesamiento Online

### 🔍 Consulta de Saldo

Permite consultar el saldo disponible de una cuenta.

**Flujo funcional:**

1. El usuario ingresa el número de cuenta.
2. El sistema valida que la cuenta exista.
3. Se consulta el saldo asociado.
4. El saldo es mostrado en pantalla.

**Ejemplo:**

CUENTA ACC001

SALDO   800.00

---

### 💸 Retiro de Fondos

Permite realizar un retiro de dinero desde una cuenta bancaria.

**Flujo funcional:**

1. El usuario ingresa el número de cuenta.
2. El usuario ingresa el monto a retirar.
3. El sistema ejecuta las validaciones de negocio.
4. Si la operación es válida:
   - Se aplica el débito
   - Se actualiza el saldo
   - Se muestra el nuevo saldo

**Ejemplo de operación exitosa:**

CUENTA ACC001

VLR RETIRO 100.00

En pantalla aparece la cuenta ya actualizada:

CUENTA ACC001

SALDO  700.00

---

## ✅ Validaciones de Negocio

El programa CICS implementa las siguientes validaciones:

- ❌ La cuenta no existe
- ❌ El monto del retiro es inválido o menor/igual a cero
- ❌ El monto del retiro es mayor al saldo disponible

Cuando una validación falla:

- El débito **no es aplicado**
- Se muestra el mensaje de error correspondiente al usuario

---

## 🧠 Consideraciones Técnicas

- Operación en **tiempo real**
- Interacción directa con el usuario
- Validaciones inmediatas
- Diseño alineado a sistemas **Core Banking**

---

**Autor:** David Esteban Restrepo Parra  
**Módulo:** Batch / Online – CICS 

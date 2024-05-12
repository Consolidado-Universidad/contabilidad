# Guía para la Creación de Archivos CSV de Contabilidad

Este documento describe cómo preparar un archivo CSV para su uso con el script de contabilidad que maneja transacciones comerciales, devoluciones, y otros movimientos financieros.

## Estructura del Archivo CSV

El archivo CSV debe tener las siguientes columnas:

| Columna     | Descripción                                                      | Ejemplos                        | Notas                                                                          |
| ----------- | ---------------------------------------------------------------- | ------------------------------- | ------------------------------------------------------------------------------ |
| Fecha       | Fecha de la transacción en formato `AAAA-MM-DD`.                 | `2012-03-03`                    | Requerido para todas las entradas.                                             |
| Descripción | Descripción breve de la transacción.                             | `Compra de mercaderías`         |                                                                                |
| Monto       | Monto de la transacción sin IVA, a menos que se especifique.     | `250000`                        | Para `CompraIVA`, el monto incluye el IVA.                                     |
| Tipo        | Tipo de transacción (ver tipos permitidos abajo).                | `Compra`, `Venta`, `CompraIVA`  |                                                                                |
| Pago        | Método de pago utilizado.                                        | `Efectivo`, `Cheque`, `Crédito` | Algunos tipos de transacciones pueden no tener método de pago, como `Capital`. |
| Cantidad    | Cantidad de items involucrados (opcional, dependiendo del tipo). | `100`                           | Usualmente usado para `Compra` y `Venta`.                                      |

## Tipos de Transacciones Permitidos

| Tipo           | Descripción                                                           | IVA Incluido | IVA Aplicado a |
| -------------- | --------------------------------------------------------------------- | ------------ | -------------- |
| `Capital`      | Transacciones de aporte de capital inicial.                           | No           | N/A            |
| `Cta Obligada` | Aportes obligados o comprometidos previamente, típicamente iniciales. | No           | N/A            |
| `Compra`       | Compra regular de bienes o servicios.                                 | No           | CF             |
| `CompraIVA`    | Compra de bienes o servicios donde el monto ya incluye IVA.           | Sí           | CF             |
| `Venta`        | Venta de bienes o servicios.                                          | No           | DF             |
| `Devolución`   | Devolución de bienes, reducción de IVA Crédito Fiscal.                | No           | CF             |
| `Pérdida`      | Pérdidas de inventario o activos, genera IVA Débito Fiscal.           | No           | DF             |
| `Retiro`       | Retiro de efectivo o equivalentes por los propietarios.               | No           | DF             |
| `RetiroM`      | Retiro de mercaderías por los propietarios, incluye IVA.              | No           | DF             |
| `Gasto`        | Gastos operativos que no generan IVA Crédito Fiscal.                  | No           | N/A            |
| `Depósito`     | Depósito en bancos o cuentas financieras.                             | No           | N/A            |

## Métodos de Pago

| Método     | Descripción                                    |
| ---------- | ---------------------------------------------- |
| `Efectivo` | Pago realizado en efectivo.                    |
| `Cheque`   | Pago realizado por cheque.                     |
| `Crédito`  | Pago realizado a través de crédito o préstamo. |
| `N/A`      | No aplicable o no se realiza pago directo.     |

## Ejemplo de Entrada CSV

```
Fecha,Descripción,Monto,Tipo,Pago,Cantidad
2012-03-03,Aporte inicial Juan Castro (Efectivo),2000000,Cta Obligada,Efectivo,
2012-03-10,Compra de mobiliario,250000,CompraIVA,Crédito,
2012-03-15,Venta de mercaderías,2500,Venta,Efectivo,425
2012-03-30,Retiro personal Juan Castro (Mercaderia),250,RetiroM,Cheque,50
```
Este archivo CSV puede ser utilizado para

 procesar transacciones utilizando el script de contabilidad. Asegúrese de que todas las entradas estén correctamente formateadas y cumplan con los tipos y métodos de pago especificados.

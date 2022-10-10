# Mango API documentation


### Entrada de diario

#### Registrar Entrada de diario


```
POST https://amipharma.dyndns.org:{port}/api/Contabilidad/RegistrarEntrada
```

Ejemplo del la solicitud:

```
POST /api/Contabilidad/RegistrarEntrada
Host: amipharma.dyndns.org
Authorization: N/A
Content-Type: application/json
Accept: application/json
Accept-Charset: utf-8

[
  {
   "numEntrada": 1501,
    "compania": 101,
    "sucursal": 101,
    "referencia": "11-08",
    "fechaDocum": "2020-12-30",
    "diarioCnt": "NOM",
    "concepto": "ENTRADA DE NOMINA - OCTUBRE 2022",
    "modulo": "NOM",
    "usuario": "ADMIN",
    "reqFolder": 0,
    "reqCdc": 0,
    "cuenta": "11030102",
    "decripcion": "Cuentas por Cobrar Empleados",
    "origen": 1,
    "monto": 600
  },
  {....},
  {....}
]
```

Con los siguientes campos:

| Parameter       | Type         | Required?  | Description                                     |
| -------------   |--------------|------------|-------------------------------------------------|
| `numEntrada`    | int          | required   | Numero de la entrada de diario en el Origen. |
| `compania`      | int          | required   | Código de la CIA a la que se registrara la entrada - 101 AMIPHARMA. |
| `sucursal`      | int          | required   | Código de la Sucursal: 101 Sucursal Principal. |
| `referencia`    | string       | optional   | Referencia a utilizar para la entrada de Diario. |
| `FechaDocum`    | datetime     | required   | Fecha para la que sera registrada la Entrada. |
| `diarioCnt`     | string       | required   | The status of the post. Valid values are “public”, “draft”, or “unlisted”. The default is “public”.  |
| `concepto`      | string       | required   | Texto explicativo que justifica el registro de la entrada. |
| `modulo`        | string       | required   | Código que representa el origen de la entrada de diario: NOM - Modulo de Nomina. |
| `usuario`       | string       | required   | Representa el código del usuario que esta haciendo el registro y a nombre de quien se hará la auditoria. |
| `cuenta`        | string       | required   | Código de la Cuenta contable a ser afectada. |
| `decripcion`    | string       | required   | Texto que describe el uso de la cuenta que se afecta: puede usar el nombre de la misma. |
| `origen`        | int          | required   | Representa la posición a considerar el valor de cuenta: 1 - Débito, -1 - Crédito. |
| `monto`         | decimal      | required   | Valor con el que sera afectada la cuenta antes señalada |


Possible errors:

| Error code           | Description                                                                                                          |
| ---------------------|----------------------------------------------------------------------------------------------------------------------|
| 400 Bad Request      | Required fields were invalid, not specified.                                                                         |
| 401 Unauthorized     | The access token is invalid or has been revoked.                                                                     |
| 403 Forbidden        | The user does not have permission to publish, or the authorId in the request path points to wrong/non-existent user. |



### Obtener Catalogo de cuentas

```
GET https://amipharma.dyndns.org:{port}/api/Contabilidad/catalogo?Compania=101
```
Ejemplo de respuesta

```
[
   {
    "codigoCuenta": "1",
    "nombreCuenta": "ACTIVOS"
  },
  {
    "codigoCuenta": "11",
    "nombreCuenta": "ACTIVOS CORRIENTES"
  },
  {
    "codigoCuenta": "1100",
    "nombreCuenta": "EFECTIVO EN CAJA Y BANCOS"
  },
  {
    "codigoCuenta": "1101",
    "nombreCuenta": "Efectivo en Caja y Bancos"
  },
  {
    "codigoCuenta": "110101",
    "nombreCuenta": "Caja General RD$"
  },
  {
    "codigoCuenta": "110102",
    "nombreCuenta": "Fondo Fijo Caja"
  },
  {...}
]
```

Con los siguientes campos:

| Parameter       | Type         | Required?  | Description                                     |
| -------------   |--------------|------------|-------------------------------------------------|
| `compania`    | int          | required   |  Código de la CIA de donde se cargara el catalogo de cuentas - 101 AMIPHARMA. 



Possible errors:

| Error code           | Description                                                                                                          |
| ---------------------|----------------------------------------------------------------------------------------------------------------------|
| 400 Bad Request      | Required fields were invalid, not specified.                                                                         |
| 401 Unauthorized     | The access token is invalid or has been revoked.                                                                     |
| 403 Forbidden        | The user does not have permission to publish, or the authorId in the request path points to wrong/non-existent user. |






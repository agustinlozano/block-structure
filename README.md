# Bimtrazer blocks
Esta documentación corresponde a la nueva estructura de bloques parseada desde los modelos en IFC utilizando la librería IFC.js

## Block structure

Nuestros bloques son representados con objetos que contienen los siguientes campos, **btzCode**, **elements**, **labels**.

```JS
{
	btzCode :: String,
	elements :: Array<Object>,
	labels :: Array<Object>,
}
```
- btzCode, es un identificador único afanumérico generado desde el cliente.
- elements, es un conjunto de objetos que contiene todo los elementos IFC.
- labels, las etiquetas que están ligadas a ese bloque.  

### - Element field
Cada uno de los elementos en el array **elements** tiene un conjunto de objetos, actualmente esos objetos tienen la siguiente estructura.

```JS
{
	"expressID" :: Number,
	"btzDescription" :: String,
	"type" :: Number,
	"GlobalId": {
		"type":  1,
		"value" :: String
	},
	"OwnerHistory": {
		"type":  5,
		"value" :: Number
	},
	"Name": {
		"type":  1,
		"value" :: String
	},
	"Description":  null,
	"HasProperties": [
		{
			"type":  5,
			"value" :: Number
		},
		{
			"type":  5,
			"value" :: Number
		}
   ]
}
```
Campos como, _**OwnerHistory**_,  _**Name**_, _**Description**_, son devueltos por la librería y al día de hoy están bajo revisión, muy probablemnte sean discriminados en el futuro. Lo mismo aplica para subcampos _**description**_ y _**type**_.

Los más importantes actualmente son:
- **expressID**: Es un identificador de IFC (no es confiable debido a que es propenso a colisión). Es útil desde el mapeo que se realiza del lado del cliente.

- **btzDescription**: Es un parámetro que los modeladores BIM nos facilitan desde herramientas como Revit.

- **hasProperties**: Es un array que contiene los expressID de las clases IFC ligadas a un bloque.

- **type**: Es un número que IFC.js utiliza para referenciar a la clase IFC.

### - label field

Son etiquetas tales como, **brickwork**, **structure**, **electricity**, etc.

```JS
{
	"alias" :: String,
	"weight" :: Number
}
```
